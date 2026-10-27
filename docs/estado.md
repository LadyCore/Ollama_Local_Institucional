# Entorno y estado

Actualizado: 2026-10-26. Etapa: pausa de pruebas repetitivas de MooChat y revisión de reemplazos para consulta documental local. Rigen los [resultados offline del 25 y revisión del 26](ensayos-offline-2026-10-25.md). Los [ensayos del 20](ensayos-aero-2026-10-20.md) y la [integración del 19](integracion-aero.md) se conservan como antecedentes. Latencia, estabilidad de VM y persistencia pendientes; no aprobado para producción.

## Continuidad del 26 de octubre — prioridad actual

- Alcance: respuesta fundamentada en documentación del curso, sin convertir razonamiento general en requisito principal. Guía sintética cargada el 24, con restricción de contenido informada; respuesta correcta sobre entrega, aproximadamente un minuto según la administradora.
- Pruebas del 25 aportadas el 26: 27 capturas. TXT de guía y La farolera leídos; Word cargado sin recuperación de información; PDF fallido según informe de la administradora. No se atribuye el fallo documental a Internet.
- Código público MooChat: lector directo de PDF/texto, sin rama DOC/DOCX. PDF usa herramientas locales; disponibilidad, permisos y tipo de PDF en la VM sin comprobar. No equivale a auditoría del paquete instalado.
- Estabilidad: watchdog, reinicios de journald, soft lockup de 42 s y avisos RCU. Windows al 92–94 % de memoria en muestras. Causa no determinada; no hay benchmark limpio ni evidencia concluyente de agotamiento de RAM.
- Criterio obligatorio: primero conjunto completo dentro de 9250 MB asignados al laboratorio; después destino de 15 GiB totales/11 GiB disponibles en la muestra y 16 CPU visibles Xeon Silver 4314. No confundir ambos inventarios ni considerar la disponibilidad como reserva.
- Candidatos sin instalar: SOLA primero para revisión funcional, AnythingLLM segundo, OpenChat/Open WebUI de menor prioridad provisional. Ninguno tiene viabilidad de RAM medida aquí. Tutor AI (local_dttutor), identificado en B041, vuelve a la revisión como antecedente recuperado.
- Se suspenden repeticiones de MooChat y cambios de tokens/prompts a ciegas. Pendiente revisar formatos, dependencias offline, límites por curso/usuario y consumo de extracción, embeddings y generación; aclarar estabilidad antes de nuevos ensayos.
- Los parámetros del apartado siguiente son los últimos verificados históricamente. No hubo nueva comprobación completa de configuración ni modificación del entorno durante la actualización documental.

## Configuración y antecedentes al 20 de octubre

- Proveedor Moodle: qwen3-estudio. Perfil verificado al cierre: num_predict 1536, num_thread 2, num_ctx 2048, temperature 0.6, top_k 20, top_p 0.95, repeat_penalty 1. Inspección del modelo: qwen3, 2.0B, Q4_K_M; contexto declarado 40960, thinking predeterminado true. La referencia histórica 1.7b no reemplaza esta evidencia.
- Discrepancia resuelta operativamente: Modelfile con 1536 y creación success coexistieron con parámetros consultados en 512; se recreó y se comprobó 1536. Causa pendiente. No asumir valor efectivo desde el mensaje success.
- Prompts sin /no_think en ambos niveles. Cambio experimental del system global a español neutro falló y fue revertido; permanece instrucción original de resumen/texto plano en inglés. No se modificó el código de Moodle/MooChat.
- ProxyTimeout 240 en VirtualHost Moodle; configtest Syntax OK; recarga indicada y respuesta posterior observada. Ollama activo en muestras, sin autoinicio. Permiso httpd_can_network_connect on sin persistencia; SELinux no desactivado.
- Fallos web anteriores: registro proxy_fcgi AH01075/70007 confirma agotamiento de espera Apache/PHP. También hubo bloqueo por booleano off, corregido temporalmente. No confundir ambos incidentes.
- Calidad: prueba de lápices correcta en AERO (~48 s); prueba de clases incorrecta repetidamente (~25–60 s), incluso sin historial y después de verificar 1536. API directa: éxitos parciales y errores según variantes. Última solicitud con instrucciones AERO + User/Assistant falló en 78,812803 s, 455 tokens, stop y razonamiento presente; no agotó límite.
- No se demostró que omitir reasoning_effort desactive thinking: consulta directa sin ese campo generó reasoning. Comparación con Moodle todavía no equivalente; pendiente system global y comprobación del texto almacenado/HTML.
- Pausas espontáneas de VM y avisos clocksource interfieren con medición de tiempos; causa no determinada. No declarar un benchmark ni deterioro progresivo del modelo.
- Próximo paso propuesto el 20: banco reproducible de variantes; no implementado. La prioridad fue reemplazada por la evaluación documental indicada arriba. Descarga de Tutor AI no equivale a instalación.
- Trazabilidad: consolidación retrospectiva de avances posteriores a B035 en B036–B041 y documento de ensayos; no se registró sincronización durante cada prueba. Verificación del commit remoto requerida al publicar este cambio.

## Inventario de laboratorio confirmado

| Componente | Evidencia disponible | Fuente |
|---|---|---|
| Virtualización | VirtualBox sobre notebook Windows | Contexto confirmado y consulta local |
| Sistema invitado | CentOS Stream 9, x86_64 | Salida aportada de os-release y uname |
| CPU presentada al invitado | AMD Ryzen 7 7730U with Radeon Graphics | Salida aportada de lscpu |
| CPU virtuales asignadas | 6 | Configuración local de VirtualBox leída |
| RAM asignada | 9250 MB | Configuración local de VirtualBox leída |
| RAM visible / disponible | 8,5 GiB / 7,4 GiB | Muestra de free -h aportada |
| Swap total / usada | 4,5 GiB / 0 B | Misma muestra |
| Raíz | 70 GB totales, 63 GB libres; /var comparte raíz | Salida aportada de df -h |
| /home | 148 GB totales, 146 GB libres | Misma muestra |
| Base de datos | MySQL; versión pendiente de recuperar o verificar | Confirmación de la administradora |
| Moodle y PHP | Versiones exactas pendientes de recuperar o verificar | No trasladar versiones de otro laboratorio |
| GPU de cómputo | No acreditada dentro de la VM | El nombre del procesador no demuestra acceso a GPU |

La memoria disponible y el espacio libre son mediciones puntuales, no reservas garantizadas. No se conservan identificadores ni capturas originales en el repositorio.

## Situación

Los puntos siguientes conservan la situación histórica previa al día 20; para modelo, prompts, calidad y timeout rige la sección de continuidad inmediata.

- Ollama: 0.40.6 con cuenta dedicada y unidad validada. Arranque automático `disabled`. Nube deshabilitada. Incidente inicial de ejecución y parada documentado; ensayos posteriores completados con dos hilos y sin razonamiento. journald activo, NRestarts=3 sin incremento en comprobación final.
- Distribución de componentes: Moodle 4.5 incluye el subsistema IA y su conector; Ollama y sus modelos requieren instalación/descarga independientes. [Detalle](preparacion-ollama.md).
- Preparación: [comprobación previa, dependencia, descarga y extracción](preparacion-ollama.md) registradas. zstd 1.5.5-1.el9.x86_64 instalado. Paquete oficial Ollama v0.40.6 con SHA-256 coincidente. Servicio configurado y modelo descargado. SELinux Enforcing en la comprobación inicial.
- Modelos: `qwen3:1.7b`, identificador `8f68893c685c`, 1,4 GB. Perfil qwen3-lab creado y parámetros verificados: num_thread=2, num_ctx=2048, num_predict=256; ejecución con --think=false. Inferencia sintética sin red satisfactoria; no constituye selección para producción.
- Restricciones y límites: network.conf aplicado con IPAddressDeny=any e IPAddressAllow=localhost. Ensayo comparativo en unidad temporal: timeout con filtro y HTTP 301 sin filtro. Alcance limitado a conexión IPv4 HTTP ensayada; no acredita aislamiento completo. [Detalle](control-red.md).
- Servicio: escucha TCP `127.0.0.1:11434`. Propiedades verificadas: `CPUQuotaPerSecUSec=2s`, `MemoryMax=4294967296`, `User=ollama`. Activo y API funcional tras reinicio manual. Inferencia posterior al filtro y prueba exterior desde servicio real completadas. IPv6, concurrencia y auditoría integral de salida pendientes.
- Plugins: MooChat v1.8.2 / 2026042801 **Beta** instalado por ZIP y habilitado; actividad AERO ensayada con datos sintéticos sin archivos ni contenido de sección. Objetivo Moodle 4.5.8; comprobación independiente de versiones exactas de plataforma y dependencias pendiente. [Resultados](integracion-aero.md).
- Conexión: proveedor OpenAI compatible dirigido a Ollama local; generación de texto habilitada, imagen y resumen deshabilitados. SELinux Enforcing; `httpd_can_network_connect` activado sin persistencia. Seguridad HTTP global ajustada; pendiente solución de mínimo privilegio.
- Rendimiento: tres respuestas HTTP 200 de 39,99 / 13,19 / 17,99 s. API directa con `/no_think` agotó 256 tokens en razonamiento; `reasoning_effort: none` produjo contenido final en 11,57 s. Este último control todavía no se integra en Moodle.
- Uso institucional: aprobación técnica/regulatoria y definición pedagógica son caminos distintos; ambos pendientes. Ensayo local no acredita seguridad completa ni aptitud para producción.
- Documentación: referencias a las áreas del entorno expresadas mediante denominaciones genéricas; README limitado a descripción y método técnico. Reglas de actuación del asistente en AGENTS.md. Repositorio privado; revisión del historial pendiente antes de una eventual publicación.
- Antecedentes: [ChatOllama y fuentes directamente aplicables](antecedentes-github.md) registrados. Reporte de seguridad de MooChat sobre extracción PPTX contrastado con código; integración condicionada a resolución o exclusión verificable de la ruta. Sin reproducción local.

## Alcance de la primera prueba

Primera prueba pequeña y progresiva: validar Ollama local sin conexiones externas y evaluar una consulta acotada de material de curso. No habilitar múltiples funciones ni decidir usos académicos. Los demás candidatos quedan como referencias futuras. Terus RAG v1.0.9 no supera la revisión dirigida para ese objetivo: ver [hallazgos](revision-terusrag.md). No se instala ni se desarrolla un fork en este paso.

## Secuencia de trabajo definida

1. Preparación de recuperación antes de instalar; clonación anunciada, finalización pendiente de confirmación.
2. Definición de versión de Ollama, modelo, almacenamiento y límites para convivencia con Moodle/MySQL.
3. Instalación y comprobación de inferencia local con datos sintéticos.
4. Validación de restricciones de red, persistencia y consumo.
5. Comprobación de versiones efectivas del entorno, revisión final de MooChat e integración acotada.
6. Consolidación de resultados para la propuesta técnica ante la instancia jerárquica superior.

El ensayo de migración de MySQL a MariaDB previsto en otro clon constituye trabajo independiente. No se registra una migración ejecutada ni se modifica el inventario confirmado de este laboratorio.
