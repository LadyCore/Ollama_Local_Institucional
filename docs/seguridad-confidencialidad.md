# Seguridad y confidencialidad: revisión inicial

Fecha de consulta: 2026-10-18. Alcance: fundamentos documentales y requisitos de validación de seguridad del laboratorio. Versión instalada: ninguna. Implementación y ensayo de controles pendientes. La revisión documental no acredita certificación de cumplimiento.

## Fundamento de la arquitectura

Ollama permite plantear procesamiento local bajo control institucional. La confidencialidad debe demostrarse sobre el conjunto: aplicación cliente, plugin, servicio de inferencia, sistema operativo, hipervisor, almacenamiento y red. Instalarlo localmente no acredita por sí solo aislamiento ni aptitud para datos sensibles.

## Hechos documentados

- **Política del proveedor:** declara que no recibe el contenido procesado localmente. Para nube declara procesamiento transitorio y ausencia de entrenamiento con entradas/salidas; también contempla metadatos, proveedores de servicio y transferencias internacionales. Son declaraciones del proveedor, no mediciones de este laboratorio. [Política de privacidad](https://ollama.com/privacy), actualización indicada: marzo de 2026.
- **Autenticación:** la API local no la requiere. La misma API puede derivar consultas a modelos de nube autenticados; localhost no demuestra dónde se realiza la inferencia. [Autenticación](https://docs.ollama.com/api/authentication).
- **Modo local:** `OLLAMA_NO_CLOUD=1` deshabilita modelos de nube y búsqueda web; requiere reinicio y permite comprobar el mensaje `Ollama cloud disabled: true`. La escucha predeterminada es `127.0.0.1:11434`. [FAQ](https://docs.ollama.com/faq).
- **Operación Linux:** la guía describe usuario dedicado, servicio systemd, instalación de versiones concretas y consulta de registros. [Linux](https://docs.ollama.com/linux).
- **Herramientas:** la aplicación que integra el modelo ejecuta las funciones solicitadas. Esa capacidad exige revisar los permisos y efectos del integrador. [Tool calling](https://docs.ollama.com/capabilities/tool-calling).
- **Mantenimiento:** el proyecto recomienda actualizar, proteger las instancias y monitorear actividad; dispone de un canal de reporte privado de vulnerabilidades. [Seguridad del proyecto](https://github.com/ollama/ollama/security).

## Controles y pruebas de aceptación

Estos controles establecen los criterios de validación del laboratorio. Su cumplimiento requiere evidencia de ejecución. Los parámetros de configuración y las medidas condicionadas a acceso remoto o uso institucional permanecen pendientes de definición.

| Área | Criterio de validación | Evidencia requerida |
|---|---|---|
| Salida de datos | Modo local y política de salida restringida al proceso/servicio; separar descarga autorizada de operación | Inferencia sintética con salida bloqueada y observación de conexiones/DNS durante arranque, ejecución y errores; ensayo cloud rechazado |
| Exposición | Escucha solo en loopback durante la primera etapa; revisar también redirecciones y proxies | Socket efectivo y prueba desde otro equipo sin acceso directo |
| Identidad | Acceso mediante backend autorizado; si hay red, intermediario con autenticación, autorización y TLS | Accesos admitidos y rechazados; API administrativa inaccesible a usuarios finales |
| Privilegios | Usuario dedicado, permisos mínimos, sin acceso a base de datos ni archivos Moodle por defecto | Identidad efectiva y pruebas de permisos; revisar SELinux sin deshabilitarlo para resolver fallos |
| Persistencia | Inventariar historiales de cliente, tablas del plugin, logs, temporales, swap, volcados y copias | Buscar un marcador sintético tras la prueba; definir acceso, retención y eliminación en cada ubicación |
| Cifrado | Evaluar protección de disco virtual, host, swap y respaldos | Configuración verificada; recordar que cifrar el disco no impide acceso a un administrador con el sistema abierto |
| Recursos | Limitar CPU/RAM y carga; comenzar con un modelo y una solicitud a la vez | Medidas antes/durante/después y comprobación de Moodle/MySQL; parada ante degradación |
| Suministro | Descargar desde origen oficial, fijar versiones, registrar hashes y revisar licencias de cada modelo | Inventario reproducible; hash registra identidad, no certifica por sí solo origen o inocuidad |
| Actualizaciones | Ensayar cambios y recuperación antes de aplicar; revisar avisos relevantes a la versión elegida | Registro de actualización, regresión y reversión |
| Incidentes | Poder detener el servicio, bloquear acceso y conservar evidencia mínima autorizada | Procedimiento probado y responsables definidos antes del uso institucional |

Deshabilitar nube no es un firewall y no controla conexiones de plugins o aplicaciones externas. CORS tampoco sustituye autenticación. Restringir a loopback reduce exposición remota, pero no a procesos locales comprometidos o administradores del host.

La política de salida se diseñará sin cortar indiscriminadamente la conectividad que requieren Moodle/MySQL. No se aplicaron reglas durante esta revisión.

## Revisión obligatoria de cada plugin Moodle

Determinar qué información construye y envía, desde dónde llama, si tiene proveedores alternativos o fallback remoto, qué registra y cómo se elimina. Comprobar autorización por rol/curso y separación de historiales entre usuarios. Verificar que documentos recuperados respeten los permisos originales antes de incorporarlos al contexto. Los embeddings, si se usan, también deben incluirse en el inventario de datos.

Si incorpora herramientas, navegación o ejecución, evaluar instrucciones maliciosas en entradas/documentos y no otorgar acciones privilegiadas por la respuesta del modelo. Las salidas deben tratarse como contenido no confiable antes de renderizarlas o usarlas para acciones. Un prompt que diga «no revelar» no sustituye controles de acceso.

Las revisiones parciales de [MooChat](revision-moochat.md) y [Terus RAG](revision-terusrag.md) registran hallazgos específicos. El aislamiento entre usuarios y la compatibilidad efectiva permanecen pendientes de ensayo.

## Límites para la presentación institucional

Estado acreditado: arquitectura local evaluable, con controles pendientes de ensayo. No se dispone de evidencia de aislamiento efectivo ni de aptitud para datos sensibles o clasificados. Toda declaración de cumplimiento requiere correspondencia con requisitos institucionales y pruebas registradas.

El organismo correspondiente deberá determinar categorías de datos permitidas, responsables, accesos, retención, requisitos de cifrado, respuesta a incidentes y aceptación de riesgos. Esta revisión no sustituye esas políticas internas, que no se han aportado, ni acredita certificaciones, acuerdos de tratamiento o niveles de servicio.

La primera prueba utiliza texto sintético, sin cuenta cloud ni integraciones externas. El registro incluye resultados satisfactorios, fallos y limitaciones. La aprobación para datos reales corresponde a una etapa institucional posterior.
