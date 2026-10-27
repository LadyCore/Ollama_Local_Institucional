# AERO: documentos offline y selección de reemplazo

Registro retrospectivo: 2026-10-26 (Argentina). Pruebas realizadas el 2026-10-25; antecedente de guía sintética ensayada el 24. Evidencia: 27 capturas aportadas y aclaraciones de la administradora. Se conserva únicamente una síntesis anonimizada, no los documentos, capturas ni identificadores personales.

## Ampliación documental recibida el 26

Fuente adicional: bitácora DOCX aportada por la administradora con transcripciones de pruebas del 25–26. Se registra como evidencia informada en ese documento, no como nueva inspección de VM ni revisión directa de todas las capturas referidas. No se publica el original ni sus imágenes.

- El 26, con Internet habilitado, se informó lectura exitosa de un PDF de UML cargado junto a dos TXT y Only Use Uploaded Content activado. Se verificó una respuesta específica y otras sobre UML; duración informada superior a un minuto y medio. PDF falló offline en la sesión anterior y funcionó posteriormente: la causa de la diferencia y la dependencia de Internet siguen sin demostrarse.
- La referencia del DOCX a La farolera como pregunta ajena al material se corrige con la aclaración directa de la administradora: era un TXT cargado y se leyó. No se reconstruye el contenido disponible en cada consulta anterior.
- Medición transcrita: 1905 tokens de entrada; evaluación del prompt 45199,31 ms (42,15 tokens/s); 237 tokens generados; generación 26800,29 ms (8,81 tokens/s); total interno 71999,60 ms. HTTP 200 de chat completions en 1m38s. En esta muestra, procesar la entrada tarda más que generar. La diferencia HTTP/interno no está explicada.
- ollama ps transcrito: qwen3-estudio:latest, 1,6 GB, 100% CPU, contexto 2048, runner llamacpp. Ese tamaño no representa toda la RAM requerida. Log transcrito: nube deshabilitada, escucha local e inferencia CPU. Suspensión del anfitrión y posterior reinicio de VM informados como condición de sesión, no diagnóstico causal.
- Código instalado según transcripción: moochat_get_uploaded_content en lib.php:291, extracción TXT/PDF y concatenación; send_message.php agrega contenido, historial y mensaje a fullprompt y lo entrega a core_ai. No se observa recuperación semántica de fragmentos en ese recorrido. La entrada completa puede aumentar latencia, pero no se midió contribución por archivo.
- Búsqueda de substr/truncate/mb_substr en lib.php sin coincidencias según transcripción; no demuestra ausencia de límites en otras capas. Manejo efectivo de contexto y posibles recortes pendientes de medición.

Inspecciones registradas como ejecutadas en el DOCX (MOODLE_ROOT sustituye la ruta de instalación):

```bash
grep -Rnl 'generate_text' "$MOODLE_ROOT/mod/moochat"
grep -n -C 8 'generate_text' "$MOODLE_ROOT/mod/moochat/classes/external/send_message.php"
sed -n '135,165p' "$MOODLE_ROOT/mod/moochat/classes/external/send_message.php"
grep -Rn 'function .*uploaded_content' "$MOODLE_ROOT/mod/moochat" --include='*.php'
sed -n '291,310p' "$MOODLE_ROOT/mod/moochat/lib.php"
sed -n '330,350p' "$MOODLE_ROOT/mod/moochat/lib.php"
grep -n 'substr\|truncate\|mb_substr' "$MOODLE_ROOT/mod/moochat/lib.php"
sed -n '160,175p' "$MOODLE_ROOT/mod/moochat/classes/external/send_message.php"
```

La búsqueda de return $content quedó expresamente NO ejecutada. Pendientes: medir texto extraído/tokens sin divulgar documentos; separar extracción, preparación, evaluación y generación; correlacionar bloqueos y suspensión. Esta ampliación no reanuda pruebas pausadas ni modifica código.

## Alcance vigente

AERO se evalúa como asistente que consulta y explica materiales del curso donde está ubicado, o documentos cargados expresamente para ese curso. Debe reconocer la falta de información. Las pruebas generales de aritmética del 20 de octubre se conservan como antecedente, pero no son el criterio principal de selección ni el próximo trabajo previsto. El aislamiento de red y la restricción de contenido son controles distintos; ninguno garantiza por sí solo respuestas correctas.

## Resultados observados

| Caso | Evidencia y resultado | Estado |
|---|---|---|
| Guía de práctica TXT | Recupera informe de dos páginas en PDF, descripción del problema, propuesta de solución, tarea de entrega y comprobación de apertura del archivo | Verificado en capturas |
| Fecha de entrega | La guía declara que no establece fecha. El chat responde que no tiene información, en inglés, pese a la instrucción de español | Ausencia de fecha no inventada; idioma inadecuado |
| Pregunta sobre en qué consiste la entrega | Una respuesta posterior menciona únicamente dónde entregar y omite qué debe entregarse | Respuesta incompleta |
| La farolera TXT | La administradora confirma el formato TXT y su lectura; captura muestra respuesta sobre de quién se enamoró | Lectura funcional confirmada en la prueba aportada |
| Informe Word | Se observa el archivo cargado junto a la guía, restricción Only Use Uploaded Content marcada y reiteradas negativas sobre participantes, responsabilidades y recomendaciones del informe | Fallo funcional observado; extensión exacta DOC/DOCX no recuperada |
| PDF | La administradora informa que tampoco funcionó offline | Ejecutado informado; causa y documento exacto pendientes |
| Conexión | Aparece Failed to connect to AI service en varios momentos | Fallo observado; no atribuido automáticamente a Internet o RAM |

El TXT sí funcionó: tanto la guía como La farolera. No corresponde tratar toda la sesión como fracaso de lectura. Las respuestas del propio bot sobre qué formatos puede leer no constituyen inventario técnico de sus extractores.

## Estabilidad y recuperación durante los ensayos

Las capturas muestran avisos clocksource, fallos de systemd-journald por watchdog, core dumps, reinicios del servicio de registro, soft lockup de CPU durante 42 segundos y avisos RCU. En un aviso figura llama-server; esto identifica el proceso observado, no demuestra la causa del bloqueo. No se observa evidencia suficiente para atribuir los incidentes a agotamiento de RAM, a Ollama o a la desconexión de Internet.

En Windows se observó memoria utilizada del 92–94 %. Es una condición del equipo anfitrión, no una medición de RAM interna de Ollama. Los tiempos de captura no se convierten en latencias de inferencia. La estabilidad del laboratorio impide considerar esta sesión un benchmark limpio.

Comandos visibles, ejecutados por la administradora en distintos momentos (no una secuencia nueva a aplicar):

```bash
systemctl start ollama
systemctl is-active ollama
systemctl restart ollama
setsebool httpd_can_network_connect on
systemctl restart httpd
systemctl restart php-fpm
```

Se observan respuestas active tras iniciar/reiniciar Ollama y, tras un arranque posterior, inactive antes de reiniciarlo. El booleano se activa sin -P; no acredita persistencia. Se conserva el antecedente de arranque automático de Ollama deshabilitado. No se registran nuevos cambios del modelo, del código del plugin o del límite ProxyTimeout en estas capturas. Los últimos parámetros verificados siguen siendo los del 20 de octubre, no una nueva comprobación del día 25.

## Hallazgos sobre MooChat

Consulta de fuentes públicas: 2026-10-26. Instalación histórica: mod_moochat v1.8.2, build 2026042801, Beta. El código público main consultado no se ha comparado byte a byte con la instalación.

- El formulario acepta cualquier tipo de archivo; eso no acredita extracción para todos los formatos.
- La función moochat_get_uploaded_content procesa PDF mediante pdftotext local y, si no obtiene texto, intenta Smalot PdfParser mediante vendor/autoload.php. También procesa TXT y tipos MIME text/*.
- No aparece una rama para DOC/DOCX en esa función. La ausencia encaja con el fallo Word observado.
- La ruta PDF revisada no necesita Internet y no incorpora OCR. Falta comprobar en la VM disponibilidad de herramientas, permisos, dependencias y características del PDF; no se determina la causa del fallo reportado.
- La lectura de PPTX en recursos de sección es una ruta diferente y no equivale al soporte de PPTX en carga directa. Permanece el antecedente de seguridad documentado en la revisión previa.

Fuentes: [lector de archivos](https://github.com/bapool/moodle-mod_moochat/blob/main/lib.php), [formulario](https://github.com/bapool/moodle-mod_moochat/blob/main/mod_form.php), [ficha Moodle](https://marketplace.moodle.com/plugins/3741). No se encontró un reporte verificable de terceros que establezca que el PDF requiera Internet.

## Recursos: filtro de selección obligatorio

1. Primero, viabilidad del conjunto completo en el laboratorio: 9250 MB asignados, aproximadamente 9 GB como límite de la administradora; notebook anfitriona de 16 GB. El inventario histórico del invitado indica 8,5 GiB visibles y 6 vCPU. No ampliar la VM como supuesto para aprobar un candidato.
2. Después, viabilidad en el entorno de destino: muestra aportada de 15 GiB totales, 3,4 GiB usados, 11 GiB disponibles; swap de 8 GiB con 10 MiB usados; 16 CPU visibles, Intel Xeon Silver 4314 a 2,40 GHz. Los recursos son compartidos y la disponibilidad es puntual. No se ha acreditado GPU ni capacidad concurrente.

El presupuesto debe incluir Moodle, MySQL, sistema operativo, modelo generador, modelo de embeddings y extracción/indexación. Deben medirse tanto los picos de preparación documental como la consulta. Ningún reemplazo está validado todavía dentro de esos límites.

## Preselección, no decisión de instalación

| Candidato | Evidencia publicada consultada | Pendientes y prioridad |
|---|---|---|
| SOLA, local_ai_course_assistant | README consultado declara Moodle 4.5+, PDF/DOCX/PPTX y contenido de curso. Configuración ofrece Ollama para generación y embeddings, PDF por pdftotext y DOCX/PPTX por ZipArchive | Primer candidato para revisión funcional. Sin medición de RAM del conjunto; funcionamiento integral offline, permisos por curso, dependencias y versión exacta del paquete pendientes. No garantiza DOC antiguo, OCR ni todos los formatos |
| AnythingLLM | Documentación publica 2 GB de RAM para la aplicación y ofrece embeddings locales y widget insertable | Segunda opción. Los 2 GB no son el total con Moodle y modelos. Integración, autenticación, permisos por curso y formatos exactos pendientes |
| OpenChat + Open WebUI | Actividad Moodle conectada con Open WebUI; documenta chat con documentos | Menor prioridad provisional por servicio adicional; formatos de la integración y consumo total sin validar |
| Tutor AI, local_dttutor | B041 ya registra identificación en capturas y descarga informada | Candidato histórico recuperado de la bitácora. No confundirlo con SOLA ni dar por demostrada su lectura offline; revisar paquete, formatos y recursos |

La primera revisión de SOLA mostró README 7.8.8/build 2026101300; otros resultados indexados mostraron versiones anteriores. Es una referencia de consulta, no una versión seleccionada ni instalada. Antes de instalar se requiere fijar release/commit y revisar las dependencias efectivas. No hay orden de consumo medido entre candidatos: la prioridad anterior es de investigación.

Fuentes consultadas el 26:

- [SOLA README](https://github.com/saylordotorg/moodle-local_ai_course_assistant) y [configuración de extractores y proveedores](https://github.com/saylordotorg/moodle-local_ai_course_assistant/blob/main/settings.php).
- [AnythingLLM: requisitos](https://docs.anythingllm.com/installation-docker/system-requirements), [embeddings](https://docs.anythingllm.com/setup/embedder-configuration/overview) y [widget](https://docs.anythingllm.com/features/chat-widgets).
- [OpenChat](https://github.com/CATALPAresearch/moodle-mod_openchat).

## Decisión y continuidad

Se pausa la repetición de pruebas de MooChat y los ajustes de parámetros a ciegas. No se instaló ningún sustituto ni se modificó el entorno real. Se continúa con revisión de candidatos bajo el límite del laboratorio y la necesidad de documentos del curso. Antes de ensayar un reemplazo, debe aclararse la inestabilidad de la VM para no confundir fallos del entorno con defectos del plugin.

Pendientes: fijar formatos requeridos (incluidos DOC antiguo, documentos escaneados y otros), revisar Tutor AI y SOLA, confirmar cadena completamente local, aislamiento entre cursos/usuarios, versión de Moodle/PHP y compatibilidad MySQL, estimar y luego medir consumo completo. Los resultados offline no certifican bloqueo integral de salida de datos. Recuperación: no hay nueva instalación que revertir; se conserva la configuración previa y su procedimiento documentado.
