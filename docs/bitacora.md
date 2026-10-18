# Bitácora viva

Registro cronológico del laboratorio. Zona de referencia: America/Buenos_Aires. No representa una receta completa ni una aprobación de despliegue institucional.

## 2026-10-18 — B001 — Apertura y alcance

- **Objetivo:** explorar Ollama local, configuraciones y restricciones, y compatibilidad de plugins Moodle para una futura presentación técnica ante la instancia jerárquica superior.
- **Acción:** recuperar antecedentes del trabajo anterior, consultar configuración de VirtualBox y consolidar las salidas de sistema aportadas por la administradora.
- **Evidencia:** lectura local de asignación de CPU/RAM; salidas de `cat /etc/os-release`, `uname -m`, `lscpu`, `free -h` y `df -h / /var /home`. Resumen anonimizado en [estado](estado.md).
- **Resultado verificado:** CentOS Stream 9 x86_64, 6 CPU virtuales, RAM visible 8,5 GiB y disponible 7,4 GiB; 63 GB libres en raíz y 146 GB en /home. MySQL confirmado por la administradora, sin versión exacta registrada.
- **Decisión:** evaluar primero la herramienta y sus límites técnicos. Los usos específicos serán definidos posteriormente por las áreas destinatarias.
- **Límites:** no hubo instalación de Ollama, descarga de modelos, prueba de plugins ni cambios en servicios de la VM. No se acredita GPU disponible.
- **Recuperación:** no aplica a cambios de servicios; no se realizaron.
- **Siguiente paso:** preparar instalación y controles con fuentes oficiales actuales.

## 2026-10-18 — B002 — Inicio del repositorio documental

- **Objetivo:** mantener documentación privada, reutilizable y actualizada durante el trabajo.
- **Acción:** consultar el repositorio indicado en GitHub y preparar README, reglas de continuidad, estado, plan de evaluación y matriz de compatibilidad.
- **Evidencia:** API de GitHub informó `private: true`, rama predeterminada `main` y repositorio vacío antes de esta carga inicial.
- **Resultado:** estructura documental inicial preparada; su presencia en la rama remota y el historial de Git acreditan la publicación. La comprobación posterior se comunica al cierre de la sesión.
- **Decisión:** actualizar por cada avance confirmado durante las sesiones; no implementar un monitor de la VM ni actualizaciones ficticias en segundo plano.
- **Recuperación:** restaurar una revisión anterior de documentos mediante un cambio trazable, preservando el historial.
- **Siguiente paso:** comenzar la evaluación técnica de instalación.

## 2026-10-18 — B003 — Revisión de seguridad y confidencialidad

- **Objetivo:** preparar fundamentos verificables para explicar protección de datos ante el organismo correspondiente.
- **Estado:** revisión documental verificada; controles propuestos, no ejecutados.
- **Acción:** consultar fuentes oficiales de privacidad, FAQ, autenticación, Linux, diagnóstico, herramientas y política de seguridad del proyecto.
- **Evidencia:** URLs y conclusiones en [seguridad y confidencialidad](seguridad-confidencialidad.md).
- **Resultado:** distinguir inferencia local de nube, ausencia de autenticación local y responsabilidades de plugins/host. Definir controles de red, acceso, persistencia, privilegios, recursos y mantenimiento con pruebas de aceptación.
- **Decisión propuesta:** comenzar con datos sintéticos, modo local y exposición restringida; verificar salida efectiva antes de admitir datos reales.
- **Límites:** no se instalaron componentes ni modificaron servicios; no hay certificación de cumplimiento ni plugin validado.
- **Recuperación:** no aplica a la VM; cambio exclusivamente documental.
- **Siguiente paso:** seleccionar versión y convertir los controles en un procedimiento de instalación y prueba.

## 2026-10-18 — B004 — Candidatos para Moodle 4.5.8 y Ollama

- **Objetivo:** identificar funciones disponibles para orientar la elección posterior de usos.
- **Estado:** investigación documental verificada; ensayo pendiente.
- **Acción:** consultar MoodleDocs 4.5, fichas y versiones de Marketplace y repositorios de autores.
- **Evidencia:** enlaces, releases y builds en [matriz](compatibilidad-moodle.md).
- **Resultado:** proveedor incluido y cuatro plugins con soporte declarado 4.5/Ollama; distinción de Stable/Alpha y puntos de seguridad de cada candidato.
- **Decisión propuesta:** comenzar por conexión core; escoger luego editor, chat o RAG según evaluación. No asumir compatibilidad exacta del entorno ni cadenas de datos completamente locales sin ensayo.
- **Límites:** sin instalación, auditoría completa de código o prueba funcional. No se crearon cursos.
- **Recuperación:** no aplica a VM; actualización documental.
- **Siguiente paso:** instalar y validar Ollama antes de ensayar integraciones; revisar paquete exacto y dependencias del candidato elegido.

## 2026-10-18 — B005 — Revisión dirigida de Terus RAG

- **Objetivo:** comprobar procesamiento local, alcance por curso y persistencia antes de instalar.
- **Estado:** código v1.0.9 inspeccionado; pruebas dinámicas no realizadas.
- **Resultado:** destino local configurable para generación/embeddings; índice en base Moodle. Se detecta búsqueda global, courseid no aplicado y extracción Ollama limitada a resumen/nombre del curso. También se observan valores externos por defecto y verificación TLS desactivada.
- **Evidencia:** [revisión con enlaces al código](revision-terusrag.md).
- **Decisión propuesta:** no instalar esta versión para la primera prueba de materiales por curso; mantener la validación de Ollama separada. No ampliar a desarrollo de un fork.
- **Alcance confirmado:** avance pequeño, progresivo y documentado; otros plugins son posibilidades futuras. Las decisiones académicas y de adopción corresponden a las áreas responsables.
- **Recuperación:** no aplica a la VM; no hubo cambios.

## 2026-10-18 — B006 — Búsqueda acotada de bots por curso

- **Objetivo:** identificar bots configurables por curso con conexión documentada a Ollama local.
- **Estado:** revisión documental, sin instalación.
- **Resultado:** [lista corta](bots-por-curso.md) con MooChat, Exabis y alternativa AI Chat/AI Manager. Diferenciar conversación, contexto y consulta de documentos; no atribuir RAG local a partir del solo soporte de Ollama.
- **Decisión:** no descartar por almacenar datos en Moodle ni por admitir proveedores externos opcionales. No aprobar una cadena local completa sin verificación. Mantener alcance progresivo.
- **Límites:** no se recuperó la página de versiones de MooChat; paquete exacto pendiente. No se confirmó la herramienta de una institución de referencia ni se guardan datos de personas.
- **Recuperación:** no aplica a servicios; solo documentación.

## 2026-10-18 — B007 — MooChat priorizado y enlace Asyntai identificado

- **Objetivo:** resolver la consulta del plugin 3401 y concretar la revisión del candidato preferido.
- **Estado:** revisión documental y estática parcial verificada; ensayo pendiente.
- **Acción:** consultar ficha y versiones oficiales, leer archivos del autor mediante API de GitHub a revisión fija y comprobar las API principales en Moodle 4.5. Código no ejecutado.
- **Evidencia:** [fuentes y hallazgos](revision-moochat.md). MooChat v1.8.2 / 2026042801 Beta; commit 01ac171790fa7c01ea681b6b6ff523512ef52b67. El enlace 3401 es Asyntai, con cuenta/servicio externo documentado.
- **Resultado:** archivos propios delimitados por contexto de actividad, generación delegada al proveedor Moodle, restricción mediante instrucciones y guardado de historial recibido del cliente. No se acredita aislamiento integral ni ausencia de conexiones externas.
- **Decisión:** priorizar MooChat para evaluación pequeña; comenzar eventualmente con texto sintético explícito, sin calificación ni incorporación automática de sección. No instalar todavía.
- **Recuperación:** no aplica a servicios; cambios documentales trazables.
- **Siguiente paso:** validar Ollama local y completar revisión del paquete antes de ensayar integración en 4.5.8.

## 2026-10-18 — B008 — Normalización editorial y consolidación del protocolo

- **Objetivo:** expresar la documentación como registro técnico de decisiones, fundamentos, procedimientos y pendientes del proyecto.
- **Estado:** documentación actualizada; sin cambios en servicios.
- **Acción:** revisar README, estado, protocolo, matriz, controles y revisiones de candidatos; actualizar las reglas de mantenimiento documental.
- **Resultado:** se conserva la cronología. Se elimina el tratamiento de informe del asistente hacia la administración y se reemplaza la secuencia exploratoria desactualizada por la definida: recuperación, Ollama local, validación de controles e integración acotada con MooChat.
- **Trazabilidad:** las entradas históricas conservan las propuestas registradas en su fecha. El protocolo vigente las reemplaza cuando existe una decisión posterior. Las opciones de configuración no acordadas permanecen pendientes de definición; la decisión de laboratorio no acredita ejecución ni aprobación institucional.
- **Situación operativa:** clonación previa anunciada, sin confirmación de finalización. La migración MySQL/MariaDB prevista para otro clon es independiente del ensayo de IA.
- **Recuperación:** revisión documental anterior conservada en el historial del repositorio.
- **Siguiente paso:** completar la preparación del entorno y definir los parámetros de instalación de Ollama.

## 2026-10-18 — B009 — Generalización de referencias institucionales

- **Objetivo:** mantener documentación reutilizable sin identificar las áreas del entorno de aplicación.
- **Estado:** referencias actualizadas en la documentación vigente.
- **Acción:** reemplazar nombres y siglas de organismos por denominaciones genéricas en README, estado, fundamentos de seguridad y entradas cronológicas; registrar el criterio editorial permanente.
- **Resultado:** se conserva la cronología y la atribución de fuentes públicas de software. El repositorio permanece privado.
- **Pendiente:** revisión del historial de Git antes de cualquier publicación; las revisiones anteriores pueden conservar referencias retiradas de los archivos vigentes.
- **Recuperación:** historial existente preservado, sin reescritura.

## 2026-10-18 — B010 — Antecedentes públicos y condición de seguridad de MooChat

- **Objetivo:** identificar aportes de ChatOllama y antecedentes aplicables a la integración local.
- **Estado:** documentación consultada y patrón de código contrastado; ejecución pendiente.
- **Acción:** consultar README y documentación web de ChatOllama a revisión fija, fuentes oficiales e incidencias de MooChat; comparar reporte #13 con lib.php de la revisión ya identificada.
- **Evidencia:** [antecedentes y fuentes](antecedentes-github.md).
- **Resultado:** ChatOllama aporta referencias de arquitectura, con componentes adicionales fuera de alcance. En MooChat se confirma la presencia del patrón de extracción XML señalado por un reporte público abierto; explotación y alcance efectivo no reproducidos.
- **Condición de evaluación:** integración de MooChat sujeta a resolver o excluir verificablemente la ruta afectada y completar revisión del paquete. La validación independiente de Ollama continúa en la secuencia definida.
- **Recuperación:** sin cambios en VM; revisión documental trazable.

## 2026-10-18 — B011 — Preparación de instalación de Ollama

- **Objetivo:** establecer los requisitos para instalar el servicio independiente en la VM existente.
- **Estado:** preparación documental; comandos sin ejecutar en la VM.
- **Acción:** consultar guía Linux y FAQ oficiales; contrastar requisitos con inventario registrado y preparar comprobaciones de herramientas, instalación previa, puerto y SELinux.
- **Evidencia:** [preparación de Ollama](preparacion-ollama.md).
- **Resultado:** instalación Linux amd64 con servicio dedicado, operación local y carga acotada; versión, modelo, ubicación y límites concretos pendientes de definición. Descarga de artefactos diferenciada de inferencia sin salida de datos.
- **Recuperación:** sin cambios operativos; clonación previa todavía sin confirmación de finalización.
- **Siguiente paso:** ejecutar la comprobación previa dentro de la VM y completar los parámetros de instalación.

## 2026-10-18 — B012 — Comprobación previa de la VM

- **Objetivo:** verificar herramientas de instalación y estado inicial del servicio y del puerto.
- **Estado:** ejecutado en la VM; salida aportada y verificada.
- **Acción y comandos:** `rpm -q curl tar zstd ca-certificates`, `command -v ollama`, `ss -ltn '( sport = :11434 )'`, `getenforce`.
- **Evidencia:** curl, tar y certificados instalados; zstd no instalado; búsqueda del ejecutable sin salida; sin escucha TCP en 11434; SELinux Enforcing. Se conserva únicamente el resultado textual anonimizado.
- **Resultado:** dependencia Zstandard pendiente. No se acredita instalación de Ollama ni finalización de clonación a partir de esta comprobación.
- **Siguiente paso:** instalar zstd y verificar el paquete. Comandos documentados, sin ejecución acreditada todavía.
- **Recuperación:** no aplica; comprobación de solo lectura.

## 2026-10-18 — B013 — Separación de componentes de la instalación

- **Objetivo:** explicitar qué incluye Moodle 4.5 y qué requiere incorporación independiente.
- **Estado:** requisito documental verificado con MoodleDocs 4.5.
- **Resultado:** el subsistema IA y el conector forman parte de Moodle; Ollama se instala en el sistema operativo, los modelos se descargan por separado y MooChat se incorpora como actividad adicional en una etapa posterior.
- **Evidencia:** [componentes y fuente oficial](preparacion-ollama.md).
- **Situación operativa:** sin nuevos cambios acreditados en la VM; instalación de zstd pendiente de confirmación.

## 2026-10-18 — B014 — Zstandard instalado y paquete Ollama identificado

- **Objetivo:** completar la dependencia de extracción y fijar el artefacto de instalación.
- **Estado:** dependencia ejecutada y salida verificada; descarga de Ollama pendiente.
- **Acción y comandos:** `dnf install zstd` y `rpm -q zstd` ejecutados en la VM. Consulta documental de guía Linux y metadatos de release oficial mediante API de GitHub.
- **Evidencia:** instalación satisfactoria de `zstd-1.5.5-1.el9.x86_64` desde BaseOS. Release oficial Ollama v0.40.6, paquete amd64 y digest registrados en [preparación](preparacion-ollama.md).
- **Resultado:** dependencia completa. Preparada descarga versionada con comprobación de hash, anterior a extracción y configuración de servicio. Ollama todavía sin instalación acreditada.
- **Recuperación:** cambio limitado al paquete Zstandard; estado anterior conservado en la bitácora. Clonación previa sin confirmación adicional.
- **Siguiente paso:** descargar el archivo y verificar SHA-256 antes de instalar.

## 2026-10-18 — B015 — Depuración del README

- **Estado:** actualización documental, sin cambios en la VM.
- **Acción:** retirar del README restricciones de actuación y mantenimiento del asistente; conservarlas en AGENTS.md.
- **Resultado:** presentación del proyecto centrada en objetivo, documentación, método técnico y datos de ensayo. Sin modificación de resultados ni cronología previa.

## 2026-10-18 — B016 — Descarga e integridad de Ollama verificadas

- **Objetivo:** obtener y verificar el paquete oficial versionado antes de instalar.
- **Estado:** descarga ejecutada; SHA-256 verificado mediante salida aportada.
- **Acción y comandos:** descarga con `curl -fL --retry 3` del artefacto oficial v0.40.6 y consulta `sha256sum /var/tmp/ollama-linux-amd64-v0.40.6.tar.zst`.
- **Evidencia:** SHA-256 `c164ab8b1b28e2a247c29719b8e404c423c5b83ae64c3ab4e59d50c7ff7fc5e0`, coincidente con el digest oficial registrado.
- **Incidencias y recuperación:** intentos con errores de transcripción de URL produjeron HTTP 404; uso de `-fl` produjo archivo vacío. Corregidos URL y opción `-fL`; descarga final completa sustituyó el archivo vacío.
- **Resultado:** paquete verificado disponible. Extracción y arranque no ejecutados todavía.
- **Siguiente paso:** extracción manual en `/usr`, seguida de preparación del servicio local.

## 2026-10-18 — B017 — Extracción del paquete Ollama

- **Objetivo:** incorporar los archivos del paquete verificado al sistema de laboratorio.
- **Estado:** extracción ejecutada; retorno al prompt sin errores visibles en la salida aportada.
- **Acción y comandos:** `tar --zstd -xf /var/tmp/ollama-linux-amd64-v0.40.6.tar.zst -C /usr`.
- **Incidencia:** primer intento con extensión incompleta `.tar`; archivo no encontrado. Corregido a `.tar.zst` en la ejecución posterior.
- **Resultado:** extracción finalizada. Servicio sin configurar y sin inferencia probada.
- **Siguiente paso:** comprobar `/usr/bin/ollama --version` y preparar el usuario y servicio local.
- **Recuperación:** inventario y retirada de archivos incorporados pendientes de completar; no se ejecutaron eliminaciones.

## 2026-10-18 — B018 — Versión del cliente comprobada

- **Estado:** ejecutado en la VM; salida verificada.
- **Acción y comandos:** `/usr/bin/ollama --version`.
- **Evidencia:** cliente 0.40.6; advertencia de falta de conexión a una instancia en ejecución.
- **Resultado:** ejecutable y versión confirmados. Servicio todavía sin iniciar e inferencia sin probar.
- **Siguiente paso:** creación y comprobación de la cuenta dedicada del servicio; paso preparado, ejecución pendiente.
- **Recuperación:** no aplica; comprobación de versión.

## 2026-10-18 — B019 — Cuenta dedicada creada con corrección pendiente

- **Estado:** creación ejecutada y cuenta comprobada; corrección pendiente.
- **Acción:** `useradd` con cuenta/grupo propios y directorio `/usr/share/ollama`; consulta `id ollama`.
- **Evidencia:** uid 995, gid 994, grupo propio. Advertencia de shell ausente o no ejecutable por error de transcripción de la ruta.
- **Resultado:** cuenta existente; no requiere recreación. Servicio todavía sin configurar.
- **Recuperación y siguiente paso:** corregir únicamente el shell mediante `usermod -s /sbin/nologin ollama` y comprobar el registro de la cuenta.

## 2026-10-18 — B020 — Corrección de shell ejecutada

- **Estado:** ejecutado; salida sin advertencias observada. Lectura del registro pendiente.
- **Acción y comandos:** `usermod -s /sbin/nologin ollama`.
- **Incidencia y recuperación:** intento intermedio con barra final en la ruta produjo advertencia; retirado ese carácter y repetido el comando correctamente.
- **Resultado:** retorno al prompt sin mensajes de error; no se recreó la cuenta.
- **Siguiente paso:** `getent passwd ollama` para comprobar los campos antes de configurar el servicio.

## 2026-10-18 — B021 — Registro de cuenta verificado

- **Estado:** ejecutado en la VM; salida verificada.
- **Acción y comandos:** `getent passwd ollama`.
- **Evidencia:** cuenta ollama, uid 995, gid 994, directorio `/usr/share/ollama` y shell `/sbin/nologin`.
- **Resultado:** corrección del shell comprobada; cuenta dedicada preparada para el servicio.
- **Siguiente paso:** crear y configurar `/etc/systemd/system/ollama.service` antes de iniciar Ollama.
- **Recuperación:** no aplica; consulta de solo lectura.

## Formato de nuevas entradas

### AAAA-MM-DD — BNNN — Título

- **Objetivo:**
- **Estado:** propuesto / ejecutado informado / verificado / fallido / pendiente.
- **Acción y comandos:** versión y parámetros sustituibles; sin secretos.
- **Evidencia:** salida mínima anonimizada y fuente; «listo» cuando corresponda.
- **Resultado y límites de prueba:**
- **Decisión:**
- **Recuperación:** prevista o ejecutada, diferenciadas.
- **Siguiente paso:**
