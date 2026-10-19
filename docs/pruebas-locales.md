# Pruebas de inferencia local

Fecha: 2026-10-18. Evidencia: salidas de consola aportadas; transcripción técnica anonimizada. Datos sintéticos, sin integración Moodle.

## Incidente inicial

La primera consulta aritmética con razonamiento activado no completó una respuesta final antes de su interrupción. Durante la ejecución aparecieron avisos `clocksource: Long readout interval` y fallos por watchdog de systemd-journald. La parada de Ollama agotó el plazo y systemd terminó procesos con SIGKILL; resultado `timeout`. No se establece causalidad entre esos eventos ni se atribuyen a falta de RAM, ahorro de energía o número de hilos.

Tras detener Ollama: 7,5 GiB disponibles, swap sin uso; muestras posteriores de vmstat mostraron aproximadamente 99 % de CPU ociosa. Son mediciones posteriores, no evidencia del consumo durante el incidente. journald recuperó estado activo con NRestarts=3. Los filtros de registros no permitieron establecer los hilos utilizados originalmente.

## Ensayos progresivos

Se reinició el servicio y se abrió `ollama run qwen3:1.7b --think=false`. Los parámetros de sesión se aplicaron mediante `/set parameter`; `/set verbose` mostró métricas. Varias variables cambiaron simultáneamente: no se aisló cuál explica la mejora.

| Ensayo | Parámetros y contexto | Resultado | Tiempo total |
|---|---|---|---|
| Aritmética | num_thread=2, num_ctx=512, num_predict=32; sin razonamiento | Respuesta 4; repetición en caliente con caché | 1,53 s en repetición |
| Biblioteca, primera formulación | num_thread=2, num_ctx=2048, num_predict=256 | Mezcló preguntas; consigna ambigua, no atribuible exclusivamente al modelo | 12,73 s |
| Biblioteca, preguntas numeradas | Misma sesión y parámetros ampliados | Horario y préstamo correctos; no afirmó apertura sabatina | 10,30 s |
| Costo ausente del texto | Misma conversación | Indicó que no estaba informado; no inventó precio | 5,78 s |
| Biblioteca sin red | Ambos cables virtuales desconectados, modelo cargado y conversación previa | Siete días | 2,53 s |
| Taller sin red | Modelo previamente retirado de memoria, sesión limpiada, texto nuevo | Veinte minutos | 4,07 s, incluidos 2,33 s de carga |
| Perfil qwen3-lab sin red | Parámetros guardados, texto nuevo sobre museo | Entrada de 500 pesos | 2,27 s |

Los tiempos son muestras individuales, no promedios ni pruebas de concurrencia. La repetición numerada conserva historial previo. La prueba del taller acredita recarga del modelo, no vaciado de cachés del sistema operativo. Durante la preparación del ensayo ampliado una entrada se interpretó como consulta acerca de num_ctx y generó texto; se interrumpió y se verificaron los mensajes de aceptación de parámetros antes del ensayo.

`ollama ps` mostró 1,5 GB, procesador 100% CPU y contexto 512 en el ensayo inicial acotado. Ese porcentaje indica ubicación del cómputo, no utilización instantánea de CPU. Memoria disponible observada: 6,1 GiB, swap 0. Tras las pruebas sin red, `systemctl show systemd-journald -p ActiveState -p NRestarts` confirmó `active` y contador 3 sin incremento.

## Perfil reproducible verificado

Archivo creado en la VM: `/var/tmp/Modelfile`. Contenido final:

```text
FROM qwen3:1.7b
PARAMETER num_thread 2
PARAMETER num_ctx 2048
PARAMETER num_predict 256
```

Comandos ejecutados:

```bash
ollama create qwen3-lab -f /var/tmp/Modelfile
ollama show qwen3-lab --parameters
ollama run qwen3-lab --think=false
```

Creación terminada en success, reutilizando capas existentes. Los tres parámetros quedaron verificados. Los valores iniciales 512/32 del archivo fueron sustituidos por 2048/256 antes de crear el perfil. El modo sin razonamiento se especifica al ejecutar; no está guardado en el Modelfile. El archivo de /var/tmp no constituye archivo permanente de configuración: este documento conserva la receta reproducible. Fuente: [Modelfile oficial](https://docs.ollama.com/modelfile).

## Límites y siguiente control

Se comprobó funcionamiento sin red con ambos cables virtuales, NAT y solo anfitrión, desconectados. No acredita bloqueo persistente con red conectada, ausencia de intentos salientes ni seguridad de otros componentes. Moodle y plugins no están integrados. Respuestas de 256 tokens pueden truncarse y contexto 2048 no acredita capacidad para documentos extensos.

Al cierre de estas pruebas sin red quedó pendiente el filtro IP exclusivo de ollama.service. La sesión posterior aplicó IPAddressDeny=any e IPAddressAllow=localhost, reconectó los adaptadores y realizó un ensayo comparativo: [control de red](control-red.md). La confirmación del 2026-10-19 establece que ambos adaptadores permanecieron conectados al cierre. El filtro no controla otros servicios ni intermediarios locales y su configuración no equivale por sí sola a demostrar aislamiento completo.

Fuente consultada: [systemd.resource-control](https://www.freedesktop.org/software/systemd/man/latest/systemd.resource-control.html), 2026-10-18. Primer diagnóstico previsto: `systemd --version` y `stat -fc %T /sys/fs/cgroup`. Recuperación del filtro: retirar únicamente su futuro archivo adicional, recargar systemd y reiniciar Ollama; procedimiento pendiente de concretar antes de aplicar.
