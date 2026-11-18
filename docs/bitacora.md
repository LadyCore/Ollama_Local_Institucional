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

## 2026-10-18 — B022 — Unidad systemd preparada

- **Estado:** configuración preparada; guardado, validación y arranque pendientes.
- **Acción:** definir unidad con usuario dedicado, destino de escucha local, nube deshabilitada y límites iniciales.
- **Parámetros:** `OLLAMA_HOST=127.0.0.1:11434`, `OLLAMA_NO_CLOUD=1`, un modelo y una solicitud paralela, `MemoryMax=4G`, `CPUQuota=200%`.
- **Evidencia:** [contenido y alcance de límites](preparacion-ollama.md); variables contrastadas con FAQ oficial.
- **Siguiente paso:** completar el archivo de servicio y verificarlo antes de iniciar; no se acredita configuración aplicada todavía.
- **Recuperación:** unidad sin arranque acreditado; retirada del archivo preparado o restauración de su revisión previa si corresponde.

## 2026-10-18 — B023 — Revisión visual de la unidad en edición

- **Estado:** archivo en edición inspeccionado visualmente; corrección, guardado y validación pendientes.
- **Resultado:** cuatro directivas de variables escritas `Enviroment` requieren corrección a `Environment`. Las demás líneas visibles coinciden con el contenido preparado.
- **Acción documental:** incorporar función, alcance y límites de las directivas con fuentes oficiales; distinguir controles de escucha, nube y recursos del bloqueo efectivo de salida.
- **Evidencia:** [configuración y explicación técnica](preparacion-ollama.md). Sin captura original en el repositorio.
- **Siguiente paso:** corregir la directiva, guardar y validar la unidad antes de iniciar.

## 2026-10-18 — B024 — Unidad de servicio guardada

- **Estado:** corrección y guardado ejecutados; validación pendiente.
- **Acción:** corregir las cuatro directivas a `Environment` y guardar `/etc/systemd/system/ollama.service`.
- **Evidencia:** editor informa 20 líneas y 321 bytes escritos, con retorno al prompt. Revisión visual previa del contenido corregido.
- **Resultado:** archivo guardado; no se acredita servicio iniciado ni parámetros aplicados.
- **Pendiente de ensayo:** consultas en cola y tiempos de espera de Moodle con paralelismo inicial de una solicitud.
- **Siguiente paso:** `systemd-analyze verify /etc/systemd/system/ollama.service`, antes de recarga y arranque.

## 2026-10-18 — B025 — Validación de unidad completada tras correcciones

- **Estado:** validación ejecutada; última salida sin mensajes de error.
- **Acción y comandos:** corrección del archivo y repetición de `systemd-analyze verify /etc/systemd/system/ollama.service`.
- **Incidencias:** directivas mal transcritas de ExecStart y Environment y sección Install incorrecta. La revisión visual previa no identificó todos los errores; el validador permitió localizarlos. Último guardado: 20 líneas, 320 bytes.
- **Resultado:** unidad validada sin mensajes, con retorno al prompt. Servicio sin arranque acreditado todavía.
- **Siguiente paso:** recarga de systemd, inicio manual y consulta de estado; después inspección de controles efectivos.
- **Recuperación:** corrección del archivo y nueva validación; sin cambios en servicios ajenos.

## 2026-10-18 — B026 — Primer arranque de Ollama verificado

- **Estado:** ejecutado; servicio activo según salida aportada.
- **Acción y comandos:** `systemctl daemon-reload`, `systemctl start ollama`, `systemctl status ollama --no-pager`.
- **Evidencia:** `active (running)`, unidad cargada y arranque automático `disabled`; proceso `/usr/bin/ollama serve`. Registro `Ollama cloud disabled: true`. Estado informa máximo de memoria 4,0 G; consumo puntual 13,2 M antes de cargar modelos.
- **Incidencia:** recarga informa rc.local sin permiso ejecutable; no impide arranque de Ollama. Archivo ajeno sin modificar.
- **Resultado:** servicio iniciado. Socket completo, CPUQuota efectivo, descarga de modelo e inferencia pendientes. No se acredita bloqueo general de salida de red.
- **Siguiente paso:** comprobar escucha con `ss -ltnp 'sport = :11434'`.
- **Recuperación:** parada controlada mediante `systemctl stop ollama` ante anomalías.

## 2026-10-18 — B027 — Escucha local comprobada

- **Estado:** ejecutado; salida verificada.
- **Acción y comandos:** `ss -ltnp 'sport = :11434'`.
- **Evidencia:** socket TCP LISTEN en `127.0.0.1:11434`, asociado a Ollama; sin escucha en todas las interfaces en esta consulta.
- **Incidencia:** filtro inicial sin dos puntos delante del puerto produjo error de análisis; consulta corregida satisfactoria.
- **Resultado:** escucha loopback comprobada. No acredita bloqueo de conexiones salientes ni restricciones de otros intermediarios.
- **Siguiente paso:** comprobar cuota CPU, memoria y usuario mediante propiedades de systemd.
- **Recuperación:** no aplica; inspección de solo lectura.

## 2026-10-18 — B028 — Parámetros de recursos verificados

- **Estado:** verificado mediante salida aportada.
- **Objetivo y comando:** comprobar configuración efectiva con `systemctl show ollama -p CPUQuotaPerSecUSec -p MemoryMax -p User`.
- **Evidencia:** `CPUQuotaPerSecUSec=2s`, `MemoryMax=4294967296`, `User=ollama`.
- **Incidencia:** primera consulta omitió la cuota por transcripción de `USec`; consulta corregida satisfactoria.
- **Resultado:** cuota CPU, techo de 4 GiB y usuario dedicado confirmados. Rendimiento y consumo bajo carga pendientes.
- **Recuperación:** no aplica; consulta de solo lectura.
- **Siguiente paso:** descarga propuesta de `qwen3:1.7b` para prueba técnica pequeña; fuente, tamaño y estado pendiente en [preparación](preparacion-ollama.md). No se registra descarga ni aprobación para producción.

## 2026-10-18 — B029 — Descarga del primer modelo completada

- **Objetivo:** disponer de un modelo pequeño para el ensayo local.
- **Estado:** ejecutado; salida verificada.
- **Acción y comando:** `ollama pull qwen3:1.7b`.
- **Evidencia:** capas descargadas al 100%, verificación SHA-256 y escritura de manifiesto informadas; resultado `success`.
- **Resultado:** descarga completada. Inferencia y comportamiento de red pendientes de prueba; no acredita aptitud para producción.
- **Recuperación prevista:** `ollama rm qwen3:1.7b` permite retirar el modelo si se descarta; no ejecutado.
- **Siguiente paso:** registrar identificador y tamaño mediante `ollama ls`, seguido de una consulta sintética.

## 2026-10-18 — B030 — Identificador local del modelo comprobado

- **Objetivo:** registrar la distribución efectivamente descargada.
- **Estado:** verificado.
- **Acción y comando:** `ollama ls`.
- **Evidencia:** `qwen3:1.7b`, identificador `8f68893c685c`, tamaño 1,4 GB.
- **Resultado:** identificador coincidente con el catálogo consultado. Inferencia todavía pendiente.
- **Recuperación:** no aplica; inspección de solo lectura.
- **Siguiente paso:** primera consulta sintética definida en [preparación](preparacion-ollama.md).

## 2026-10-18 — B031 — Consolidación de pruebas locales y perfil

- **Estado:** resultados verificados en salidas aportadas; consolidación documental posterior a los ensayos.
- **Acciones:** primera inferencia interrumpida, parada con timeout, diagnóstico, reinicio, ajustes de sesión y ensayos sintéticos progresivos. Desconexión de ambos cables virtuales y recarga del modelo con contexto nuevo. Creación y comprobación de qwen3-lab.
- **Evidencia:** [comandos, métricas, incidente y perfil](pruebas-locales.md). Última consulta del perfil: precio correcto, 2,27 s. journald activo y contador de reinicios sin incremento al cerrar ensayos previos.
- **Resultado:** funcionamiento local sin red acreditado en pruebas pequeñas. Causa del incidente inicial sin establecer; controles permanentes de salida pendientes.
- **Recuperación ejecutada:** interrupción de consulta y parada del servicio en el incidente inicial; reinicio posterior. No se alteraron servicios ajenos.
- **Siguiente paso:** comprobar requisitos del filtro IP por servicio antes de aplicarlo y verificarlo con red conectada.

## 2026-10-19 — B032 — Filtro persistente y recuperación de continuidad

- **Estado:** ejecución informada en bitácora técnica de la sesión 18–19 de octubre, aportada por la administradora; no reinspección de la VM.
- **Acciones:** comprobación de systemd 252, cgroups v2 y soporte BPF; respaldo de unidad; creación y validación de network.conf; recarga y reinicio. API local respondió con modelos disponibles.
- **Evidencia y comandos:** [registro del control de red](control-red.md). Misma unidad temporal, usuario y destino: timeout con filtro y HTTP 301 sin filtro.
- **Resultado y límites:** evidencia favorable para conexión IPv4 HTTP ensayada en unidad temporal; no prueba universal ni intento exterior directo del servicio Ollama. Archivo temporal eliminado y ausencia comprobada.
- **Confirmación posterior:** ambos adaptadores quedaron conectados al cierre, según mensaje de la administradora del 2026-10-19. Se resuelve el pendiente que figuraba en la bitácora aportada.
- **Recuperación:** respaldo y filtro permanente conservados. Retirada del filtro no ejecutada.
- **Siguiente paso:** inferencia con filtro y red conectada, y ampliación de validación del servicio real. Consolidación documental sin datos de red internos ni identificadores personales.

## 2026-10-19 — B033 — Prueba de salida desde el servicio real

- **Estado:** verificado en salidas aportadas.
- **Objetivo y acción:** contrastar salida IPv4 con red conectada; curl desde terminal respondió HTTP 301. Drop-in temporal en `/run/systemd/system/ollama.service.d/prueba.conf` con `[Service]` y `ExecStartPost=-/usr/bin/curl -4 -I --connect-timeout 5 --max-time 10 http://1.1.1.1`.
- **Evidencia:** `systemd-analyze verify ollama.service` sin errores; recarga y reinicio; registro 16:00:45 con curl 28 y timeout de 5000 ms dentro de ollama.service.
- **Resultado:** bloqueo del destino IPv4 ensayado desde servicio real; no prueba universal ni control de salida de PHP.
- **Recuperación ejecutada:** eliminado solo el drop-in temporal, `systemctl daemon-reload`, servicio active y `/api/tags` HTTP 200. Filtro permanente conservado.
- **Siguiente paso:** integración; cobertura IPv6 y auditoría completa pendientes.

## 2026-10-19 — B034 — MooChat y actividad AERO operativos

- **Estado:** instalación y respuestas verificadas en evidencia aportada; registro consolidado al cierre.
- **Objetivo y acciones:** snapshot previo 16:39, instalación ZIP MooChat v1.8.2, proveedor local y actividad AERO con contenido sintético. Diagnóstico de bloqueos HTTP y SELinux, recuperación del servicio tras apagados.
- **Comandos, configuración y evidencia:** [registro reproducible de integración](integracion-aero.md).
- **Resultado:** dos preguntas sintéticas respondidas correctamente; saludo inadecuado. HTTP 200 con latencias 39,99 / 13,19 / 17,99 s. No se probaron documentos ni separación de usuarios.
- **Decisión:** laboratorio operativo; no habilitación institucional. Cambios HTTP globales y permiso de red web temporal documentados.
- **Recuperación:** disponible snapshot previo; reversión del booleano con `setsebool httpd_can_network_connect off`. No ejecutada al cierre. Arranque automático de Ollama no habilitado.
- **Siguiente paso:** evaluar rendimiento y permiso mínimo, sin extrapolar seguridad de Ollama a toda la cadena Moodle.

## 2026-10-19 — B035 — Comparación del control de razonamiento

- **Estado:** API directa verificada; aplicación del control en Moodle pendiente.
- **Objetivo:** distinguir demora y salida generada sin pasar por MooChat.
- **Acción:** curl a `/v1/chat/completions` con qwen3-lab y pregunta sintética; comparación entre `/no_think` textual y añadido `reasoning_effort: none`.
- **Evidencia:** 20,140108 s, 256 tokens, reasoning y contenido final vacío, cierre length; segunda ejecución 11,567252 s, 114 tokens, respuesta final correcta y cierre stop. [Comando y límites](integracion-aero.md).
- **Resultado:** control explícito eficaz en este caso; instrucción textual insuficiente. No son pruebas idénticas al contexto que envía MooChat ni certifican rendimiento general.
- **Recuperación:** no se cambiaron archivos ni perfil del modelo; parámetros de solicitud únicamente.
- **Siguiente paso:** definir incorporación mantenible del parámetro a la integración; no se aplicó aún ni se alteró el núcleo Moodle.

## 2026-10-20 — B036 — Consolidación retrospectiva de modelos y calidad

- **Estado:** verificado en evidencia aportada; registro retrospectivo de sesión anterior y continuación, sin inventar horas.
- **Objetivo y acciones:** experimento aero-lab no desplegado; creación qwen3-estudio con 512; ensayos C/L, follow-ups y chats nuevos. [Cronología, comandos y resultados](ensayos-aero-2026-10-20.md).
- **Evidencia:** aero-lab 12,481595 s/84 tokens, incorrecto; estudio inicialmente mostró 512. Respuestas simples correctas y explicaciones posteriores erróneas. Muestra servidor 28,90 s/247 tokens.
- **Resultado:** no selección por velocidad ni aprobación pedagógica. Ahorro de energía informado en primer incidente; causalidad de pausas posteriores pendiente.
- **Recuperación:** modelo experimental separado; no cambio del modelo base original acreditado.
- **Siguiente paso:** comparación directa del control de razonamiento.

## 2026-10-20 — B037 — API directa y límites de salida

- **Estado:** verificado en capturas, matriz D01–D05 del documento de ensayos.
- **Acciones:** consultas a chat completions, cambios de /no_think, reasoning_effort y max_tokens por solicitud; recuperación del servicio detenido con systemctl start ollama.
- **Evidencia:** D01 62,73 s/512/length/content vacío; D02 38,28 s/476/stop incorrecto; D03 102,02 s/1129 con inconsistencias; D04 83,51 s/769 correcto en contexto; D05 74,91 s/885 correcto.
- **Resultado:** más presupuesto permitió respuestas completas; no garantiza verdad. Qwen3 inspeccionado como 2.0B/Q4_K_M y thinking true por defecto.
- **Recuperación:** parámetros de estas solicitudes no persistidos. No se atribuyen niveles de razonamiento graduados al modelo booleano.
- **Siguiente paso:** trasladar configuración y comprobar valores efectivos.

## 2026-10-20 — B038 — Diagnóstico web y timeout

- **Estado:** salidas de servicio, booleano, registros y configtest verificadas; recarga indicada con respuesta web posterior.
- **Acciones y comandos:** httpd_can_network_connect off restablecido con `setsebool httpd_can_network_connect on`; búsqueda de ErrorLog; identificación de AH01075/70007 en proxy_fcgi; ProxyTimeout 240 dentro del VirtualHost Moodle; `apachectl configtest`, `systemctl reload httpd`.
- **Evidencia:** Ollama active, permiso on; HTTP 200 del servidor con 2m5s total y 73,70s de procesamiento; interfaz falló en ~68s. Configtest Syntax OK. Posterior respuesta de lápices correcta en ~48s.
- **Resultado:** conexión y timeout son incidentes distintos; no se desactivó SELinux. Avisos clocksource y pausas VM documentados sin causa atribuida.
- **Recuperación prevista:** retirar solo ProxyTimeout, validar y recargar; booleano off revierte permiso. No ejecutada. Persistencia de booleano y arranque siguen pendientes.
- **Siguiente paso:** calidad en chats nuevos, no solo conectividad.

## 2026-10-20 — B039 — Fallos en AERO, reversión y perfil efectivo

- **Estado:** respuestas y parámetros verificados; restauración de prompt informada con «listo».
- **Acciones:** pruebas M01–M05; instrucción global en español neutro ensayada y revertida; sin /no_think. Inspección de parámetros mostró 512 pese a archivo con 1536 y create success previo. Nueva creación y consulta confirmaron 1536.
- **Evidencia:** fallos C con historial y sin historial; ~34s, ~25s y ~60s según ensayo. La prueba posterior a 1536 siguió validando erróneamente 7,5 min.
- **Resultado:** aumento de tokens no solucionó fiabilidad. Causa de discrepancia de perfil no determinada; se corrige afirmación prematura de actualización efectiva.
- **Recuperación:** prompt global original restaurado, no los límites ni el timeout. No se editaron archivos del plugin.
- **Siguiente paso:** contrastar estructura real de solicitudes.

## 2026-10-20 — B040 — Código instalado y comparación de formato

- **Estado:** fragmentos instalados y consultas directas verificados; equivalencia completa con Moodle pendiente.
- **Acciones:** inspección read-only de process_generate_text.php y send_message.php; revisión de concatenación de prompt/historial y campos de API; recuperación de consultas por fc. Matriz D06–D08 en [ensayos](ensayos-aero-2026-10-20.md).
- **Evidencia:** proveedor no agrega reasoning_effort ni max_tokens, toma message.content. MooChat concatena instrucciones/historial como User/Assistant. D06 aún medium: 135,43s/1317, correcto en lo esencial. D07 sin campo: 107,00s/1218, reasoning presente, explicación confusa. D08 con instrucciones y etiquetas: 78,81s/455/stop, incorrecto, reasoning presente.
- **Resultado:** no hay evidencia de thinking necesariamente desactivado por omisión del campo. Último error no agotó salida. Sensibilidad al mensaje es hipótesis, no causalidad probada: sin réplicas, se cambiaron varias partes; falta system global para equivalencia.
- **Recuperación:** no hubo parches ni captura de tráfico; consultas no entrenan el modelo ni incluyen automáticamente historial de ensayos anteriores.
- **Siguiente paso:** detener cambios a ciegas; preparar comparación reproducible con repeticiones. Banco todavía no implementado.

## 2026-10-20 — B041 — Funcionalidades, referencias y recuperación de trazabilidad

- **Estado:** controles visibles verificados; descarga de alternativa informada; revisión de código público realizada; funcionalidades no ensayadas pendientes.
- **Acciones:** contraste visual de MooChat/Tutor AI; lectura de capacityAr y antecedentes aplicados. Consolidación de registros posteriores a B035 y actualización de estado/README/compatibilidad.
- **Evidencia:** avatar AERO visible; carga de materiales y restricción por contenido visibles. Tutor AI identificado en capturas como local_dttutor, no equiparado al nombre EdWork. capacityAr usa Groq/Gemini/mock, no Ollama implementado en los clientes revisados.
- **Resultado:** no instalar sustitutos ni prometer PDF, preguntas guía o diapositivas como capacidades verificadas. Documentación pendiente fue detectada por consulta de la administradora; no hubo sincronización por prueba. Remoto previo inspeccionado: 49022bb321890c16a69c7307bb5d47b132c23620, privado.
- **Recuperación:** consolidación retrospectiva con resultados fallidos, reversiones y evidencias parciales explícitos; sin imágenes ni identificadores del entorno.
- **Siguiente paso:** verificar publicación remota de este cambio documental y registrar avances futuros junto con estado, sin esperar una nueva solicitud.

## 2026-10-26 — B042 — Alcance documental y prueba de guía del 24

- **Estado:** registro retrospectivo; alcance confirmado por la administradora y respuesta observada en captura.
- **Objetivo:** evaluar AERO como asistente del material del curso. El razonamiento general deja de ser el criterio principal.
- **Acción y evidencia:** carga de guía TXT sintética y Only Use Uploaded Content informadas con «listo». Tras error de conexión, inicio manual de Ollama y activación temporal del booleano web; respuesta correcta sobre qué entregar y dónde, aproximadamente un minuto informado.
- **Resultado:** consulta documental básica funcional; calidad general, latencia y aislamiento por curso no validados.
- **Decisión:** evaluar material aportado y ausencia de información; conservar pruebas matemáticas anteriores como antecedentes.
- **Recuperación:** no nuevo parche ni cambio de parámetros acreditado. Procedimientos previos conservados.
- **Siguiente paso:** consolidar ensayos offline aportados el 26.

## 2026-10-26 — B043 — Pruebas offline del 25 y estabilidad

- **Estado:** 27 capturas revisadas; lectura TXT confirmada, Word fallido observado y PDF fallido informado.
- **Objetivo y acciones:** registrar consulta de guía, La farolera e informe sin conectividad exterior según la administradora. [Matriz y comandos visibles](ensayos-offline-2026-10-25.md).
- **Evidencia:** guía y La farolera eran TXT y se leyeron. Negativas reiteradas sobre informe Word; respuestas en inglés e incompletas en algunos casos. Failed to connect to AI service, watchdog/journald, soft lockup de 42 s y avisos RCU. Windows al 92–94 % de memoria en muestras.
- **Resultado y límites:** fallos documentales y de estabilidad diferenciados. No se demuestra causa por RAM, Internet u Ollama. No hay tiempos comparables de benchmark.
- **Decisión:** pausar nuevas repeticiones de MooChat; no modificar a ciegas modelo o prompt.
- **Recuperación:** capturas muestran arranque/reinicio de Ollama, booleano temporal y reinicios httpd/php-fpm; no se afirma reparación permanente. No se incorporan capturas ni contenido personal al repositorio.
- **Siguiente paso:** revisión de reemplazos y estabilidad del laboratorio.

## 2026-10-26 — B044 — Formatos, candidatos y límites de recursos

- **Estado:** revisión pública realizada; compatibilidad declarada, sin instalación ni medición local de candidatos.
- **Acción:** lectura de MooChat lib.php/mod_form.php; documentación/configuración de SOLA, requisitos de AnythingLLM y OpenChat. Fuentes, diferencias y versiones en [registro documental](ensayos-offline-2026-10-25.md).
- **Evidencia:** MooChat acepta subida genérica pero lector directo no procesa DOC/DOCX; PDF se extrae localmente. SOLA declara Moodle 4.5+, PDF/DOCX/PPTX, Ollama para chat y embeddings; RAM integral no acreditada. AnythingLLM publica 2 GB para aplicación, no para conjunto completo. OpenChat añade Open WebUI; formatos de integración pendientes.
- **Decisión:** primero viabilidad dentro de 9250 MB del laboratorio; después destino de 15 GiB totales, 11 GiB disponibles en muestra y 16 CPU visibles. Orden de investigación provisional, no ranking de consumo medido. Sin instalación ni aprobación productiva.
- **Recuperación de antecedente:** B041 identifica Tutor AI como local_dttutor en capturas; se corrige la falta de recuperación del nombre durante la conversación. Pendiente confirmar su correspondencia con el candidato recordado por la administradora y revisar funcionalidades.
- **Recuperación:** cambio exclusivamente documental, sin servicios afectados.
- **Siguiente paso:** fijar formatos y versión de candidatos; revisar cadena offline, permisos y consumo completo. Publicar y verificar este registro con actualización de estado en el mismo commit.

## 2026-10-26 — B045 — Ampliación por bitácora transferida

- **Estado:** documento DOCX leído; pruebas y métricas informadas mediante transcripciones, no ejecutadas nuevamente.
- **Objetivo y acción:** contrastar la nueva fuente con B043/B044 y preservar diferencias de evidencia. Se registra PDF UML exitoso con Internet habilitado el 26, tras fallo offline previo; causalidad pendiente. Se mantiene aclaración directa de que La farolera era TXT cargado.
- **Evidencia:** evaluación de entrada 45,2 s/1905 tokens; generación 26,8 s/237 tokens; total interno 72 s frente a HTTP 1m38s. Inspección instalada informada: extracción TXT/PDF, concatenación en fullprompt y core_ai; comandos y límites en [ampliación](ensayos-offline-2026-10-25.md).
- **Resultado:** PDF no debe describirse como incapaz de funcionar; se conserva fallo offline específico. La entrada explica más tiempo que la generación en la muestra, sin explicar toda la demora HTTP.
- **Decisión y recuperación:** actualización documental, sin instalar ni modificar servicios. No publicar DOCX ni capturas. Mantener selección bajo límite de laboratorio y pruebas repetitivas pausadas.
- **Siguiente paso:** separar tiempos de procesamiento y revisar contexto, estabilidad y candidatos; búsqueda de return $content informada como no ejecutada.


## 2026-10-27 — B046 — Reanudación de sincronización documental

- **Estado:** actualización documental preparada; publicación y verificación remota realizadas como cierre de esta sesión, con resultado comunicado por separado.
- **Objetivo y acción:** reanudar la sincronización de B045 solicitada por la administradora; revisar privacidad, enlaces, estado de rama y coincidencia de archivos publicados.
- **Resultado y límites:** se conserva el carácter informado de las métricas del DOCX. PDF exitoso con conectividad no demuestra requisito de Internet. No se realizaron cambios de servicios ni nuevas pruebas en la VM.
- **Recuperación:** publicación sin forzar la rama, preservando cambios remotos; en caso de discrepancia, detener y revisar antes de publicar.
- **Siguiente paso:** revisar candidatos y consumo integral bajo el límite del laboratorio; no repetir ajustes de MooChat a ciegas.

## 2026-11-01 — B047 — Consolidación de informe técnico y pendiente resuelto

- **Estado:** informe DOCX leído y contrastado; ensayos ejecutados informados, sin repetir pruebas ni verificar directamente la VM. Búsqueda de return $content verificada en captura aportada del 27.
- **Objetivo y acción:** incorporar avances de recursos, latencia, truncamiento y control de razonamiento. [Detalle, métricas y evidencia](estado-aero-2026-11-01.md).
- **Evidencia:** CPUQuota=400 %, MemoryMax=4G tras reversión de 5G, contexto 2048, Python 3.9.25. Última muestra 110,02 s con 2021 tokens de entrada, 295 de salida y truncated=1. Think visible en UI informado. CLI --think=false: 3,448 s en consulta breve; texto en prompts ineficaz y retirado. HTTP reasoning_effort=none: respuesta válida 27/33 tokens, sin razonamiento visible. grep devolvió líneas 344 y 545.
- **Resultado y límites:** datos nuevos sustituyen configuración histórica donde corresponde; no se equiparan tiempos CLI/HTTP con UI, ni se generaliza mejora a documentos completos. No se afirma cambio de num_thread a partir de CPUQuota.
- **Decisión:** intermediario HTTP local registrado como alternativa acordada pendiente de implementar y validar; no cambio del endpoint ni modificación de núcleo acreditados. Se mantienen restricciones de recursos y revisión de candidatos como pendientes.
- **Recuperación:** 5G revertido a 4G y textos experimentales retirados según informe. Esta sesión solo actualiza documentación, sin publicar DOCX ni capturas.
- **Sincronización:** fallida el 2026-11-01 antes de crear commit remoto: gh informa credencial inválida y API de usuario 401; repositorio 404 tanto por CLI como por conector. Revisión local de privacidad y enlaces satisfactoria. Última revisión publicada verificada: e29c9f014c1dbb97693a511e71ff209945e4ee3a. No se declara publicada esta entrada.
- **Recuperación de sincronización:** autorización de dispositivo completada. Acceso a cuenta y repositorio privado comprobado fuera del entorno restringido; dentro de este persistía error de credencial. Rama base remota coincide con e29c9f014c1dbb97693a511e71ff209945e4ee3a. Se retoma publicación sin forzar cambios remotos.
- **Siguiente paso:** verificar publicación; posteriormente validar intermediario, latencia integral, exposición de razonamiento y truncamiento con condiciones comparables.

## 2026-11-01 — B048 — Parámetros y latencia de la consulta UML

Capturas verificadas: dos hilos, contexto 2048, generación máxima 1536, cuota CPU 400 % y memoria máxima 4 GiB. Se distinguieron 123,47 s internos y 2 min 27 s HTTP. La inspección previa acredita la inclusión del historial; su política de selección sigue pendiente.

## 2026-11-03 a 2026-11-04 — B049 — Actividad después del foro de la unidad

Configuración y respuestas observadas en capturas, tiempos informados. Consultas de unidad y foro en 44 y 43 s, respectivamente. La administradora contrastó el título atribuido a un documento y el resumen del segundo video. El tema existía en el libro, pero la referencia era incorrecta; el video trataba principalmente de antenas.

## 2026-11-05 — B050 — Cuatro objetivos y prueba con PDF

Ejecutado informado y cotejo manual. Antes del PDF, cuatro consultas demoraron 33, 43, 23 y aproximadamente 36 s. Con PDF exclusivo, la consulta sobre protección demoró unos 60 s y una repregunta produjo dos referencias reconocibles en el índice. Próxima demostración propuesta, pendiente. [Detalle y condiciones de reproducción](ensayos-2026-11-03-a-05.md).

## 2026-11-06 — B051 — Incorporación de ensayos del curso de tutores del día 5

- **Objetivo:** preservar configuración, consultas, contrastes y tiempos del nuevo curso.
- **Estado:** ejecutado informado por la administradora. Informe leído e incorporado a documentación local el día 6.
- **Evidencia:** informe de ocho pruebas, comparaciones con capítulos 5, 6, 7 y 12, error de conexión y registros del kernel del día 5.
- **Resultado:** errores de atribución entre capítulos, respuestas extensas y tiempos de aproximadamente 1,5 a más de 3 minutos. El intervalo de más de diez minutos de la consulta C queda excluido como medición de generación.
- **Incidente y recuperación:** soft lockup de CPU virtual de 468 s, avisos de clocksource y posterior retorno del prompt. Ollama informó active. Recuperación de inferencias pendiente de comprobar.
- **Cambios informados:** corrección de la especialidad en el prompt, nueva instancia tras un foro, cambio posterior a creatividad 0,3 y contenido oculto desactivado. Efectos causales sin aislar.
- **Siguiente paso propuesto:** material explícito, preguntas constantes, contraste por autoras del curso y diagnóstico separado de VM e inferencia.
- [Registro detallado y comandos ejecutados en la sesión informada](ensayos-tutores-2026-11-05.md).

## 2026-11-09 — B052 — Métricas, fidelidad y fallo de ejecución CLI

- **Objetivo:** consolidar capturas de sesión e informe técnico del día.
- **Estado:** capturas observadas y comprobaciones CLI ejecutadas informadas.
- **Acciones y evidencia:** inspección de modelo, versión, Modelfile, entorno y estado del servicio; cuatro intentos run fallidos. Comandos y resultados en el [registro detallado](ensayos-2026-11-09.md).
- **Resultado:** métricas de seis solicitudes, respuesta correcta de cinco clases, discrepancias de fuentes y exámenes, servicio activo con fallo de resolución del modelo en los intentos CLI examinados.
- **Correcciones de continuidad:** conservar la pregunta histórica «qué es la destrucción?» (23 s, día 5). Registrar versión 0.4.6 informada hoy frente a 0.40.6 histórica como discrepancia pendiente.
- **Recuperación:** sin cambios permanentes informados ni mejora CLI confirmada.
- **Siguiente paso:** manifiesto local, resolución del modelo, cotejo de versión y pruebas comparables de thinking mediante MooChat.

## 2026-11-17 — B053 — Investigación de experiencias públicas de IA en Moodle

- **Objetivo:** reunir evidencia sobre plugins existentes, Ollama local, contexto documental, citas, rendimiento y alternativas; desarrollo propio solo como antecedente.
- **Estado:** verificada la consulta documental; no se reprodujeron las instalaciones externas.
- **Acción:** búsqueda pública en inglés y español, examen del índice del foro AI, lectura textual completa de 21 hilos y consulta de documentación, versiones y repositorios enlazados. Recuperación de revisiones y ensayos previos del proyecto.
- **Evidencia:** [informe completo con enlaces, fechas, configuraciones y grado de verificación](investigacion-foros-ia-moodle-2026-11-17.md). El informe distingue limitaciones del buscador, errores de acceso automatizado y alcance real del corpus.
- **Resultado:** soluciones de conexión confirmadas en Moodle 4.5 y 5; testimonios de modelos locales pequeños; insuficiencia de pruebas comparables para citas, extracción integral, actualización documental y tiempos de AERO.
- **Decisión:** no seleccionar arquitectura ni instalar sustitutos. Conservar revisión adversa de Terus RAG v1.0.9 y candidatos históricos sin revalidarlos por publicidad. Separar los dos ensayos de aproximadamente 23 segundos.
- **Resguardo:** documentos previos comparados con la revisión remota fd09070fb98fb5fa97b91bcb452778d51c15d064 antes de editar; coincidencia verificada y repositorio privado confirmado. Publicación de esta actualización sujeta a comprobación de revisión final.
- **Recuperación:** no aplica a servicios; no hubo cambios de configuración ni código del laboratorio.
- **Siguiente paso:** decisión posterior basada en evidencia y vacíos de validación; sin ensayo nuevo acordado en este avance.

## Plantilla de entrada siguiente

### AAAA-MM-DD — BNNN — Título

- **Objetivo:**
- **Estado:** propuesto / ejecutado informado / verificado / fallido / pendiente.
- **Acción y comandos:** versión y parámetros sustituibles; sin secretos.
- **Evidencia:** salida mínima anonimizada y fuente; «listo» cuando corresponda.
- **Resultado y límites de prueba:**
- **Decisión:**
- **Recuperación:** prevista o ejecutada, diferenciadas.
- **Siguiente paso:**
