# Entorno y estado

Actualizado: 2026-10-19. Etapa: integración AERO con MooChat y Ollama operativa en laboratorio. Evidencia y configuración vigente en [integración AERO](integracion-aero.md). Latencia y persistencia pendientes; no aprobado para producción. Las comprobaciones de recursos y contadores de reinicios siguientes corresponden a sus muestras históricas, no a mediciones continuas.

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
