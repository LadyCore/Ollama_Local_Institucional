# Control de red del servicio Ollama

Sesión: 18–19 de octubre de 2026. Consolidación: 2026-10-19. Fuente de resultados: bitácora de sesión aportada por la administradora; no constituye una nueva inspección remota de la VM. Confirmación posterior: ambos adaptadores quedaron conectados al cierre.

## Configuración aplicada

Entorno comprobado: systemd 252 (252-67.el9), cgroups v2 (`cgroup2fs`) y `CONFIG_CGROUP_BPF=y`. La existencia de `/sys/fs/bpf` se comprobó, pero por sí sola no acredita aplicación del filtro. `systemd-run` no estaba disponible; se utilizó una unidad temporal para el ensayo comparativo.

Se conservó respaldo de la unidad original en `/etc/systemd/system/ollama.service.bak`. Se creó `/etc/systemd/system/ollama.service.d/network.conf` con:

```ini
[Service]
IPAddressDeny=any
IPAddressAllow=localhost
```

Se verificó el archivo, se validó la unidad sin errores visibles, se recargó systemd y se reinició Ollama. `systemctl cat ollama` mostró la unidad original y el archivo adicional. La unidad original mantiene cuenta dedicada, escucha loopback, nube deshabilitada, un modelo cargado, paralelismo uno y límites de memoria y CPU.

El filtro está configurado para tráfico IP entrante y saliente de los procesos de la unidad, con excepción loopback. No representa una política de red de toda la VM ni cubre otros servicios o intermediarios locales. Referencia: [control de recursos de systemd](https://www.freedesktop.org/software/systemd/man/latest/systemd.resource-control.html).

## Verificación local posterior al reinicio

```bash
systemctl is-active ollama
curl -sS http://127.0.0.1:11434/api/tags
```

Resultados informados: servicio `active`; respuesta JSON con `qwen3-lab:latest` y `qwen3:1.7b`; registro de GET /api/tags con HTTP 200. Esto acredita acceso local al listado, no una nueva inferencia posterior al filtro.

La consulta de propiedades mostró `IPAddressAllow=::1/128 127.0.0.0/8`, pero no imprimió IPAddressDeny, incluso con --all. Los contadores IPIngressBytes e IPEgressBytes informaron `[no data]`. Estas salidas no se utilizaron como prueba suficiente de bloqueo.

## Ensayo comparativo con red conectada

Ambos adaptadores virtuales fueron reconectados. Una consulta HTTPS inicial a example.com agotó el plazo; no se dedujo ausencia general de conectividad. Una consulta IPv4 HTTP al destino público de ensayo respondió 301, acreditando salida exterior disponible para esa conexión.

Unidad temporal `/etc/systemd/system/ollama-nettest.service`:

```ini
[Service]
Type=oneshot
User=ollama
ExecStart=/usr/bin/curl -4 -I --connect-timeout 5 --max-time 10 http://1.1.1.1
IPAddressDeny=any
IPAddressAllow=localhost
```

Se validó antes de ejecutar. Un primer error Missing = por salto de línea en ExecStart fue corregido; validación posterior sin errores. Se mantuvieron usuario, destino y comando entre las dos ejecuciones; para el control se comentaron únicamente las dos directivas IP, se validó y se recargó systemd.

| Condición de la misma unidad temporal | Resultado informado |
|---|---|
| Filtro habilitado | curl (28), timeout de aproximadamente 5 s; fallo de unidad por exit-code |
| Sin filtro | HTTP/1.1 301 Moved Permanently; deactivated successfully |

El contraste aporta evidencia funcional favorable al bloqueo de la conexión IPv4 HTTP ensayada. Se probó una unidad temporal con las mismas directivas y usuario, no un intento exterior originado directamente en ollama.service. No demuestra cobertura universal de IPv6, protocolos, destinos, rutas ni intermediarios.

## Limpieza y estado de cierre

Se eliminó `/etc/systemd/system/ollama-nettest.service`, se recargó systemd y se comprobó ausencia del archivo. Persisten el respaldo y network.conf. La administradora confirmó el 2026-10-19 que ambos adaptadores quedaron conectados antes de cerrar la sesión. No queda pendiente esa confirmación.

No se modificaron deliberadamente Moodle ni MySQL. El aviso de rc.local sin permiso ejecutable quedó sin intervención. Los tres avisos históricos de timeout y SIGKILL corresponden a la parada anterior al filtro: no se atribuyen al nuevo control.

## Pendientes y recuperación

- Comprobar inferencia local con el filtro aplicado y red conectada.
- Ampliar la evidencia de bloqueo efectivo del servicio real y, cuando exista conectividad de control, cobertura IPv6. Un fallo sin control positivo no acredita bloqueo.
- Revisar persistencia tras reinicio de la VM y política de arranque manual del servicio.
- Verificar integración Moodle por separado; no está instalada ni aprobada por estas pruebas.

Recuperación prevista, no ejecutada: retirar únicamente network.conf, recargar systemd y reiniciar Ollama. Esa operación elimina este filtro y requiere mantener el aislamiento de laboratorio mientras se diagnostica. El respaldo corresponde a la unidad original; no incluye el archivo adicional.
