# Implementación de IA en Moodle: experiencias públicas y relevancia para AERO

Fecha de corte: **17 de noviembre de 2026**. Investigación documental; no instalación, modificación de servicios ni ensayo nuevo de modelos.

## 1. Resultado principal

La evidencia encontrada permite sostener que **Moodle puede utilizar Ollama local y modelos pequeños**, incluso en equipos de 8 GB, pero no demuestra que cualquiera de las alternativas examinadas resuelva simultáneamente extracción de todos los materiales, delimitación por curso, citas correctas, actualización documental y tiempos aceptables en el laboratorio AERO.

Los resultados mejor acreditados son reparaciones concretas de conexión y testimonios de funcionamiento. Para recuperación documental predominan descripciones de producto, prototipos y experiencias sin métricas comparables. No se encontró una configuración pública reproducible que garantice eliminar las alucinaciones de Qwen3 con MooChat.

Las alternativas más pertinentes son MooChat, la suite AI Manager de Bavaria, OpenAI Chat Block y su variante para Ollama, y LAMB como sistema existente integrado por LTI. Terus RAG requiere conservar la exclusión de la versión previamente inspeccionada: su descripción comercial no invalida los límites registrados en el código. No se decide todavía un reemplazo ni una arquitectura.

## 2. Método, cobertura y limitaciones

Se revisó el índice del foro oficial **Artificial intelligence (AI) and Moodle**, que mostraba 66 discusiones, y se leyeron íntegramente las intervenciones textuales de **21 hilos seleccionados**, incluyendo continuaciones y cierres. También se consultaron el foro de desarrolladores, una discusión histórica francesa, documentación oficial, fichas y versiones de plugins y repositorios enlazados. El corpus leído abarca junio de 2023 a octubre de 2026; la consulta se realizó en noviembre de 2026.

Las búsquedas combinaron Moodle/MooChat/Ollama/Qwen/Llama/DeepSeek con PDF, DOCX, RAG, course content, context, chatbot, hallucinations, benchmarking e inteligencia artificial/documentos. Se utilizaron términos ingleses y españoles. Los resultados en español fueron principalmente documentación oficial e índices, sin un testimonio técnico detallado y reproducible adicional sobre MooChat/Ollama. Esto describe lo recuperado, no la inexistencia de experiencias hispanohablantes.

El buscador devolvía con frecuencia índices y duplicados por idioma; el acceso automatizado a discusiones produjo errores 403 o una pantalla de comprobación. Los hilos incluidos pudieron leerse en el navegador. El buscador interno no produjo resultados utilizables durante la consulta. No se accedió a conversaciones privadas de Matrix ni se verificaron grabaciones completas, entornos de participantes o todos los adjuntos. No se presenta una transcripción generada por IA como sustituto de una prueba técnica.

**Alcance de exhaustividad:** relevamiento amplio y trazable de fuentes recuperables, no censo de cada intervención histórica de Moodle.org. Las 66 discusiones fueron examinadas como índice; no se afirma haber leído todas. Las fechas corresponden a los mensajes visibles; las fichas de producto son una consulta a la fecha de corte y pueden cambiar.

### Escala de evidencia

- **E1 — solución confirmada en el hilo:** el participante comunica que la acción resolvió su problema. No equivale a reproducción independiente en AERO.
- **E2 — experiencia o medición informada:** se describe una ejecución, a veces con salida técnica, pero falta un protocolo completo reproducible.
- **E3 — capacidad documentada por el mantenedor:** ficha, README, notas de versión o demostración anunciada; no prueba independiente de eficacia.
- **E4 — propuesta, hipótesis o problema abierto:** no hay confirmación del resultado buscado.
- **EL — evidencia local previa de AERO:** se mantiene separada del relevamiento externo.

## 3. MooChat: actividad, bloque y documentos

### M1. Actividad mod_moochat

**Compatibilidad declarada:** la ficha de versiones consultada publica v1.8.2, build 2026042801, del **28/04/2026**, madurez **Beta**, para Moodle 4.5, 5.0, 5.1 y 5.2. Esa declaración no demuestra un ensayo en cada combinación de servidor y proveedor. No debe confundirse con block_moochat ni con el paquete exacto instalado en AERO.

**Necesidad:** conversación contextual en una actividad, con material cargado e historial. **Capacidades anunciadas:** PDF/TXT y restricción al contenido subido; extracción de determinados archivos de sección; uso del subsistema AI de Moodle. La descripción recomienda pdftotext/Poppler y documenta un lector PDF alternativo. No acredita OCR general de escaneos, lectura de videos, seguimiento recursivo de enlaces ni extracción de DOCX.

**Resultado y verificación:** E3. Las notas de versiones recientes se centran también en objetivos, calificación y finalización; no son una validación de citas documentales. Un objetivo escrito como «respuestas rápidas» no acredita una configuración de rendimiento.

Fuentes: [ficha de la actividad](https://marketplace.moodle.com/plugins/mod_moochat), [versiones y madurez](https://marketplace.moodle.com/plugins/mod_moochat/versions), [repositorio del mantenedor](https://github.com/bapool/moodle-mod_moochat).

### M2. Comentarios de usuarios y evolución del historial

En los comentarios oficiales, **8–10/12/2025**, un usuario consulta por conservación de conversaciones y el mantenedor describe el comportamiento temporal de aquella versión. El **25/05/2026**, otro usuario valora funciones de contenido cargado y objetivos. Son testimonios de uso, sin configuración local completa, evaluación de exactitud o medición de latencia. No corresponde trasladar la ausencia histórica de persistencia a todas las versiones posteriores.

**Clasificación:** E2 para el testimonio de uso; E3 para la explicación del mantenedor. **Moodle exacto:** no consignado en esos comentarios. **Límite:** comentarios del catálogo oficial, no hilos del foro. No se recuperó una discusión independiente detallada que demostrara que MooChat corrigió invenciones bibliográficas mediante un ajuste concreto.

Fuente: [comentarios de MooChat](https://marketplace.moodle.com/plugins/mod_moochat/comments).

### M3. Bloque block_moochat

Es otro componente, con su propio historial de versiones. La ficha consultada declara Moodle 4.5–5.1 y última publicación del **19/02/2026**. No debe usarse su documentación para atribuir automáticamente comportamiento a la actividad de AERO. **E3; sin prueba comparativa independiente recuperada.**

Fuentes: [ficha del bloque](https://marketplace.moodle.com/plugins/block_moochat), [repositorio del bloque](https://github.com/bapool/moodle-block_moochat).

### M4. Relación con los resultados locales

La inspección previa de AERO documenta concatenación de instrucciones, material e historial en el prompt. No demuestra qué fragmentos llegaron en cada consulta fallida. Los ensayos muestran tanto referencias cotejables con un PDF como títulos inventados y atribuciones erróneas. Por tanto, no corresponde afirmar «MooChat nunca lee PDF» ni «al estar en la sección accede a todo su contenido».

La revisión pública previa no encontró una rama DOC/DOCX en el lector examinado. Esto es evidencia de esa implementación, no una prohibición universal del formato en Moodle. La cantidad de historial recuperada y su eventual recorte deben vincularse al paquete instalado. **EL, no resultado externo.**

Antecedentes: [revisión dirigida de MooChat](revision-moochat.md), [pruebas documentales y offline](ensayos-offline-2026-10-25.md), [ensayos del 3–5 de noviembre](ensayos-2026-11-03-a-05.md).

## 4. Ollama con el subsistema de Moodle

### O1. Moodle 4.5: conexión mediante API compatible con OpenAI

**Hilo y fechas:** Ollama and Moodle, **04–19/02/2025**. Adam Jenkins informa un servidor universitario con Ollama en LAN, modelo llama3.1:8b y fallo «No providers available». Eloy Lafuente comunica una prueba de resumen funcional usando la ruta compatible **/v1/chat/completions**. Adam confirma el **07/02** que la clave API no podía quedar vacía: un valor ficticio permitió funcionar; Ollama no lo utilizaba como autenticación.

El hilo diferencia el formato nativo de Ollama del formato OpenAI y revisa las restricciones HTTP de Moodle. **E1 para el arreglo de clave vacía; E2 para el ensayo de resumen.** No aporta control de citas ni benchmark. Un intento posterior con AI Manager tuvo problemas al guardar configuración; no se documenta su resolución en ese intercambio.

Fuente: [hilo completo](https://moodle.org/mod/forum/discuss.php?d=465747), [confirmación del arreglo](https://moodle.org/mod/forum/discuss.php?d=465747#p1870140).

### O2. Confirmación independiente de la clave no vacía

**Hilo:** Unable to configure Ollama with Moodle 4.5, **07/02/2025**. Sarath P usa Moodle 4.5, Ollama y Llama3.2 en Windows. Había ajustado hosts y puerto, pero persistía el error. Tras la sugerencia de una clave ficticia, confirma que los errores desaparecieron. **E1**, con una segunda instalación que confirma el mismo bloqueo de configuración. No hay versión exacta del modelo, tiempos ni evaluación documental.

Fuente: [discusión y confirmación](https://moodle.org/mod/forum/discuss.php?d=465867). El procedimiento queda además documentado en [MoodleDocs 4.5](https://docs.moodle.org/405/en/Ollama), actualizado el 07/02/2025.

### O3. DeepSeek funciona, pero el razonamiento cambia la experiencia

En el hilo O1, **12–19/02/2025**, se reportan pruebas de DeepSeek-R1 con razonamiento visible y salida extensa. Un participante con Moodle **4.5.2** termina comunicando funcionamiento al cambiar a Llama. No hay una comparación controlada ni parámetros suficientes para atribuir la mejora exclusivamente al tamaño o familia del modelo. **E2**. Para AERO es un antecedente pertinente de salida de razonamiento y longitud, no prueba de que cambiar a Llama resuelva documentos o latencia.

Fuente: [continuación de Ollama and Moodle](https://moodle.org/mod/forum/discuss.php?d=465747).

### O4. Moodle 5: endpoint nativo y autenticación básica

**Hilo:** Moodle 5 and Ollama API not working, **25/04–29/11/2025**. André Krüger utiliza Ollama en otro servidor, llama3.1:8b y proxy con autenticación básica. Se aclara que el proveedor nativo espera la URL base y construye la ruta de generación. André confirma el **28/04** una corrección de la clave de configuración de autenticación: de basicauthenabled a enablebasicauth.

**E1 para esa instalación y corrección**, vinculada a MDL-85301. Una consulta posterior sobre Moodle 5.1 sin autenticación no queda resuelta. No se recomienda aplicar ese cambio a versiones actuales sin comprobar si ya está corregido. Tampoco trasladar la URL base al proveedor OpenAI de 4.5, que tiene otro contrato.

Fuentes: [hilo completo](https://moodle.org/mod/forum/discuss.php?d=467692), [incidencia referenciada](https://tracker.moodle.org/browse/MDL-85301). El tracker se conserva como referencia del hilo; no se certifica aquí su estado de resolución o backports.

### O5. «Something went wrong» no identifica una causa única

**Hilo:** Moodle 5.0.1+, **01/08/2025–13/05/2026**. Yunus Akarsu informa Moodle **5.0.1+ build 20250629**, Ollama y Llama3: la API directa funciona pero Moodle falla. Se sugieren clave, caché y la incidencia de autenticación; el autor no confirma solución. Otro participante comunica el **02/10/2025** que añadir la barra final a la URL base solucionó su caso. André describe una instalación separada con Llama3.3 funcionando.

**E1 informado para el caso de la barra final, E2 para Llama3.3, E4 para el caso original.** En mayo de 2026 reaparece el mismo mensaje con OpenAI. El texto genérico del error no permite asumir el mismo problema.

Fuente: [hilo y seguimiento](https://moodle.org/mod/forum/discuss.php?d=469210).

### O6. Olmo2 y resumen de páginas

**Hilo:** Ollama with olmo2, **25/02–07/03/2025**. Richard Jones comunica que generar funciona pero resumir no. Después anuncia que funciona, atribuyéndolo tentativamente a un error de escritura, sin identificar el cambio. **E2 para el funcionamiento posterior; no solución reproducible.** La versión exacta de Moodle no queda fijada. Su observación de menor demanda de memoria respecto de Llama3.3 no incluye mediciones comparables.

Fuente: [discusión completa](https://moodle.org/mod/forum/discuss.php?d=466353).

### O7. Medición real en Raspberry Pi y alucinación comprobada por el autor del plugin

En O6, **06–07/03/2025**, AL Rachels publica una ejecución de **Ollama 0.5.11, llama3.2:3b, Raspberry Pi 5**: 42 tokens de entrada, 4,486 s de evaluación; 241 tokens generados, 47,414 s; total aproximado 51,951 s; generación de 5,08 tokens/s. La respuesta atribuye a MooTyper funciones que su mantenedor considera falsas; reformular no soluciona el error.

**E2 con salida técnica y contraste del mantenedor.** Es una prueba de inferencia local, no un benchmark del recorrido completo Moodle. El participante compara equipos con accesorios diferentes y observa velocidades similares; no demuestra aceleración de Ollama por el HAT anunciado. No permite proyectar el tiempo de AERO ni concluir que más RAM acelera la generación.

Fuente: [mediciones y discusión sobre las respuestas](https://moodle.org/mod/forum/discuss.php?d=466353).

## 5. Plugins alternativos existentes

### A1. AI Manager y suite Bavaria/ISB: experiencia con modelos pequeños

**Hilo:** Local AI, **18/06–04/11/2025**. Norbert Forster comunica el **18/09** funcionamiento local con la suite de Bavaria/ISB, Moodle **4.5–5.1**, equipos MacBook Air de 8 GB y Dell i5 de 8 GB. Enumera motores probados —Ollama, LM Studio, llama.cpp y gpt4all— y modelos como Qwen3-1.7B-GGUF, Phi-4-GGUF y Ministral 3B. No ofrece una matriz que demuestre cada combinación de motor, modelo, equipo y Moodle.

**E2:** es el antecedente externo más cercano a AERO por memoria y familia de modelo. No publica latencia, citas correctas, porcentaje de aciertos o carga concurrente. Otros mensajes confirman instalación local sin detallar configuración.

Fuente: [Local AI y seguimiento completo](https://moodle.org/mod/forum/discuss.php?d=468519).

**Documentación complementaria, E3:** local_ai_manager administra proveedores, propósitos, usuarios y cuotas; requiere interfaces consumidoras. block_ai_chat aporta conversación, contexto y personalidad. Las fichas consultadas declaran Moodle 4.4–5.2; no son una certificación del laboratorio ni prueba de RAG documental automático. Fechas de últimas publicaciones visibles: **24/09/2026** y **23/07/2026**, respectivamente.

Fuentes: [AI Manager](https://marketplace.moodle.com/plugins/local_ai_manager), [AI Chat](https://marketplace.moodle.com/plugins/block_ai_chat).

### A2. OpenAI Chat Block: fuente de verdad configurable

**Hilo:** AI chat block, **20/07/2025–25/02/2026**. Se pregunta por información distinta según capítulo de un libro. Marcus Green explica la configuración de una fuente de verdad en el bloque de Bryce Yoder y advierte sobre confabulación. No aparece una prueba de cambio automático de corpus por capítulo ni de recuperación integral del libro. **E3/E4 según capacidad o propuesta. Moodle exacto no indicado.**

La ficha actual describe contexto configurable, historial y uso del subsistema AI. Esa documentación actual no debe proyectarse sobre la versión de 2023. Incluir preguntas y respuestas en una fuente de verdad no equivale a indexar todos los archivos del curso.

Fuentes: [discusión](https://moodle.org/mod/forum/discuss.php?d=469036), [ficha de OpenAI Chat Block](https://marketplace.moodle.com/plugins/block_openai_chat).

### A3. Ollama Chat de ragcon/eLeDia y anuncio de RAG

En A2, **21/07/2025**, André Krüger anuncia trabajo con eLeDia en recuperación de actividades y archivos, contemplando permisos. El repositorio de block_ollama_chat documenta conexión Ollama y fuente de verdad configurable, y excluye soporte de OpenAI Assistants. **E3 para lo documentado, E4 para el resultado integral del RAG anunciado.** No se encontró en ese hilo un ensayo cerrado de citas, DOCX, actualizaciones y restricciones por usuario.

**Moodle:** la discusión sobre implementación local menciona 4.5; eso no certifica todas las versiones del bloque. **Interés para AERO:** alternativa de interfaz local ya existente, sin atribuirle una indexación completa por el solo anuncio.

Fuentes: [anuncio en el hilo](https://moodle.org/mod/forum/discuss.php?d=469036), [repositorio Ollama Chat](https://github.com/ragcon-ai/moodle-block_ollama_chat).

### A4. Corolair: experiencia de instalación con dificultades

**Hilo:** feedback sobre Corolair, **01/04–17/05/2025**. El mantenedor solicita opiniones tras su lanzamiento. Eduardo Kraus informa configuración compleja de permisos/API y propone asistencia guiada. En mayo, Roger informa una interfaz reducida a una franja horizontal. No se documenta arreglo posterior. **E2 para problemas observados; E4 para su resolución.** Versión de Moodle, proveedor y hardware no suficientemente detallados.

No hay evidencia recuperada que lo haga una solución local sin servicios externos ni que resuelva la fidelidad documental de AERO. Una cifra de descargas del autor no sustituye esa comprobación.

Fuente: [discusión completa de Corolair](https://moodle.org/mod/forum/discuss.php?d=467195).

### A5. Asyntai: ausencia de API key no significa procesamiento local

Recomendado en A2 el **25/02/2026**, sin un protocolo de prueba. Su ficha exige conectar una cuenta y configurar el asistente en el panel de Asyntai. Declara Moodle 3.9–5.2 y tiempos de 1–3 s, pero esos tiempos son una afirmación del proveedor, sin comparabilidad con AERO. **E3; no validado para aislamiento de red.** El hecho de no solicitar una clave API al administrador no elimina la dependencia del servicio.

Fuentes: [recomendación](https://moodle.org/mod/forum/discuss.php?d=469036), [ficha e instrucciones del proveedor](https://marketplace.moodle.com/plugins/local_asyntai).

### A6. Terus RAG: conservar la revisión específica de la versión

La documentación pública anuncia Ollama y embeddings locales, además de otros proveedores, indexación y tareas programadas. Son capacidades **E3** que deben contrastarse con la implementación exacta.

La revisión local del **18/10/2026**, etiqueta **v1.0.9 build 2026040106**, encontró que el recorrido Ollama indexaba resúmenes/nombres de cursos y buscaba sin filtro de curso/matrícula/usuario en la función examinada. No encontró extracción de PDF/DOCX en ese recorrido. Por eso se excluyó esa versión de la primera prueba de consulta restringida por curso. **EL: inspección estática, no instalación ni auditoría completa.**

La ficha y el requisito de version.php también diferían: Moodle 4.5 declarado frente a mínimo 4.2 observado en el archivo. No se extrapola la exclusión a cualquier revisión futura ni se la revoca por un README más amplio. No se recuperó un hilo independiente que acreditara la resolución de esos puntos.

Fuentes: [revisión local y enlaces a código fijado](revision-terusrag.md), [repositorio del proyecto](https://github.com/khairu-aqsara/moodle-blocks_terusrag).

## 6. Recuperación documental y desarrollos complementarios

### D1. LAMB: sistema existente con integración LTI

**Hilo:** LAMB, **18/02–13/10/2026**. Marc Alier presenta el proyecto, menciona pilotos universitarios y lo califica como beta. Un participante posterior intenta explorarlo y comunica problemas con una dirección; el hilo no termina con una evaluación independiente de desempeño. **E2 para los pilotos informados por el autor; E4 para adopción del participante. Moodle exacto no indicado.**

El repositorio documenta carga de PDF/Word/Markdown, RAG, fuentes, inspección de prompts, integración Ollama y acceso desde Moodle por LTI. Usa componentes adicionales, incluido un servicio de base de conocimiento. **E3:** encaja funcionalmente con varias necesidades de AERO, pero no se verificó consumo del conjunto en la VM de aproximadamente 9 GB, actualización incremental ni exactitud de citas bajo Qwen3 pequeño.

Fuentes: [hilo original](https://moodle.org/mod/forum/discuss.php?d=473335), [documentación y repositorio de LAMB](https://github.com/Lamb-Project/lamb).

### D2. RAG con Solr: prototipo público

En el hilo AI chat block, **22/07/2025**, Michael Hughes enlaza una implementación que describe como rudimentaria, basada en Solr. Discute una diferencia relevante: poder ver un recurso no implica necesariamente permiso institucional para procesarlo con IA. **E3 para la existencia declarada, E4 para su aptitud integral.** Sin versión de Moodle, benchmark o despliegue reproducible completo en esa intervención.

Es información complementaria de desarrollo, no motivo para iniciar un plugin propio. Fuente: [intervención en el hilo](https://moodle.org/mod/forum/discuss.php?d=469036), [repositorio enlazado](https://github.com/mhughes2k/moodle-search_solrrag).

### D3. Acceder a metadatos no equivale a recuperar todo el contenido

**Hilo:** Accessing full student-visible course content for AI / RAG use, **30/03–13/04/2026**. Toni Jokinen enumera límites encontrados al explorar servicios REST: información de libros sin capítulos, carpetas sin todos los archivos y otros tipos con metadatos insuficientes. Considera copias de seguridad, pero señala contenido no visible al alumno y dificultades de actualización incremental. La respuesta aclara que el subsistema AI introducido en Moodle 4.5 no resuelve por sí mismo exportación/indexación.

**E4:** necesidad documentada y respuesta técnica, sin exportador completo validado. No prueba que todas las API posibles de Moodle sean incapaces de entregar esos contenidos; describe las funciones y el recorrido considerados. Es directamente pertinente a los errores de AERO al atribuir conocimiento de libros, videos y enlaces.

Fuente: [hilo del foro de desarrolladores](https://moodle.org/mod/forum/discuss.php?d=473767).

### D4. Generación de preguntas a partir de material propio

**Hilo:** How can AI generate questions from Moodle’s in-house content?, **21/10/2025**. Se propone qbank_questiongen junto a local_ai_manager para trabajar con contenido institucional. Michael Hughes distingue esa posibilidad del trabajo aún en curso para conectar recuperación automática. Marcus Green relata una prueba: una imagen de una postal con poema fue utilizada para generar preguntas de opción múltiple.

**E2 para la prueba de imagen; E4 para cobertura automática del curso.** No se indican modelo, versión Moodle ni configuración suficiente. No demuestra que un Qwen3 de texto transcriba imágenes o videos. Se conserva como experiencia de otro uso, no como sustituto probado del chat documental.

Fuente: [hilo completo](https://moodle.org/mod/forum/discuss.php?d=470513).

### D5. Microsoft Moodle AI Assistant

La documentación describe un acelerador con integración de materiales y RAG, componentes Moodle y dependencia de Azure OpenAI. **E3**, no testimonio independiente de foro que confirme desempeño. Es un antecedente de implementación con servicios externos, sin equivalencia con el requisito de inferencia local de AERO. No se propone adoptarlo ni reproducir su arquitectura.

Fuentes: [documentación del proyecto](https://microsoft.github.io/moodle-ai-assistant/), [repositorio](https://github.com/microsoft/moodle-ai-assistant).

## 7. Otros hilos que precisan los límites de la evidencia

| Fecha y fuente | Entorno, problema o necesidad | Acción, resultado y verificación |
|---|---|---|
| [14–16/06/2023: OpenAI Chat Block](https://moodle.org/mod/forum/discuss.php?d=447662) | Pruebas en un curso como administrador; Moodle no indicado. Se pregunta por consultar dos fuentes de datos. | Usuario comunica bloqueo por cuota. Varias explicaciones son respuestas copiadas de ChatGPT y no pruebas del plugin. E2 para el bloqueo; E4 para integración con bases externas. No usar la configuración de 2023 como documentación actual. |
| [25/11/2024–27/02/2025: AI Assistent](https://moodle.org/mod/forum/discuss.php?d=464005) | Solicitud de tareas con feedback y solución modelo; versión no indicada. | Interés y propuestas; no implementación confirmada en Moodle. E4. |
| [13/02/2025: AI Provider Benchmarking](https://moodle.org/mod/forum/discuss.php?d=466024) | Se piden medidas de modelo, escala, infraestructura y costos. | Respuesta conceptual; su autor aclara no gestionar IA educativa real. No contiene benchmark publicable ni fórmula de dimensionamiento. E4. |
| [03/07/2025: AI keeps generating exact same text](https://moodle.org/mod/forum/discuss.php?d=468761) | Repetición de salida; configuración insuficiente, versión no indicada. | Se solicita más información, sin solución. E4; no atribuirlo a temperatura, caché o cuotas sin datos. |
| [08–10/08/2025: AI summary of a forum thread](https://moodle.org/mod/forum/discuss.php?d=469308) | Resumir conversaciones largas; se menciona Moodle 5.0. | Se discute resumen integrado y queda abierta la cobertura cuando el hilo excede la página visible. E4 para lectura completa de todas las páginas. |
| [02/10/2025–18/09/2026: Restrict summarize](https://moodle.org/mod/forum/discuss.php?d=470188) | Evitar que la IA resuma cuestionarios y dé respuestas. | Helen Foster anuncia controles por curso/actividad en 5.1. Una consulta posterior sobre 4.5 no queda resuelta. E3 para función anunciada, E4 para alternativa en 4.5. |
| [21/01/2026: Open source integration](https://moodle.org/mod/forum/discuss.php?d=471936) | Institución solicita mejores prácticas de modelos locales, escala y pruebas; versión no fijada. | Derivación a Matrix, sin configuración ni resultado publicado en el hilo. E4. |
| [03–04/08/2026: Class courseassist utils not found](https://moodle.org/mod/forum/discuss.php?d=482187) | Moodle 5.1.5+ build 20260728, PHP 8.3.32. Fallan formularios después de retirar componentes AI del núcleo. | Restaurar courseassist/editor permite trabajar de nuevo, confirmado por el afectado. E1. El hilo menciona MDL-89055 y corrección prevista en 5.1.6; no se verificó aquí esa versión. No atribuir el incidente a AI Manager por coexistencia. |
| [25–29/09/2026: Yet another AI question](https://moodle.org/mod/forum/discuss.php?d=482659) | Formación y creación de contenido, preocupaciones de accesibilidad y seguridad; versión no indicada. | Se comparan experiencias de generación H5P; se informa necesidad de revisar los textos. Una herramienta instalada localmente usa ChatGPT API: alojamiento local no demuestra inferencia local. E2/E3, sin solución integral documentada. |
| [23–28/09/2026: Community AI Discussion](https://moodle.org/mod/forum/discuss.php?d=482637) | Modelos locales, tutores y desarrollos propios. | El resumen principal y un análisis posterior se identifican como generados por IA; un participante cuestiona que el segundo corresponda a esa sesión. Se usan para localizar proyectos, no como benchmark, auditoría o confirmación de modelos/hardware. |

## 8. Comparación por necesidad de AERO

| Alternativa | Evidencia práctica recuperada | Material/contexto y referencias | Procesamiento local | Qué falta comprobar |
|---|---|---|---|---|
| MooChat actividad | EL: ensayos AERO mixtos; E2: comentarios de usuarios | Material e historial en prompt; capacidades documentales dependientes de formato/versión. Sin garantía de citas | Posible mediante el proveedor Ollama ya utilizado | Paquete instalado, extracción real, texto enviado, recortes, procedencia de cada respuesta |
| AI Manager + AI Chat | E2: instalación local y modelos pequeños en equipos de 8 GB | Contexto configurable; no se acreditó indexación integral automática | Soporte documentado y experiencia informada | Corpus, permisos, citas, tiempos y memoria con el conjunto completo |
| OpenAI Chat Block | E2 histórico de uso; fuente de verdad documentada | Contexto controlado por configuración; no equivale a RAG general | Depende de versión y proveedor, no del nombre del bloque | Versión compatible con 4.5.8 y comportamiento documental con Ollama |
| ragcon Ollama Chat | E3 de interfaz; RAG anunciado | Fuente de verdad; RAG integral sin resultado cerrado en hilo | Documentado | Estado real del RAG, formatos, límites por curso/usuario y actualizaciones |
| LAMB vía LTI | Pilotos informados por autor; E3 de implementación | Documenta PDF/Word/Markdown, recuperación y citas | Ollama/modelos locales documentados | Recursos del conjunto, instalación compatible, permisos, borrado/reindexación y precisión |
| Terus RAG v1.0.9 | EL: revisión estática adversa para el alcance | Recorrido Ollama inspeccionado insuficiente para archivos y aislamiento por curso | Generación/embeddings locales posibles en recorrido examinado | Correcciones verificables en otra revisión; no rehabilitado |
| Corolair | E2 de dificultades de instalación e interfaz | No hubo validación documental detallada recuperada | No acreditado para aislamiento | Dependencias, correcciones, fidelidad y costos |
| Asyntai | Recomendación y descripción del proveedor | Personalización anunciada | La configuración requiere servicio externo | No cumple evidencia de independencia de servicios externos |
| Microsoft AI Assistant | E3, documentación de proyecto | RAG y contenido Moodle documentados | Implementación examinada dependiente de Azure OpenAI | Fuera del requisito local actual |
| Solr RAG | Prototipo descrito por desarrollador | Recuperación basada en búsqueda, permisos discutidos | Sin ensayo completo recuperado | Madurez, integración y evidencia operativa |

Esta tabla no compara tiempos como si las preguntas, modelos y máquinas fueran iguales. Tampoco convierte compatibilidad declarada en compatibilidad ensayada.

## 9. Qué explica y qué no explica los problemas de AERO

### Extracción, selección y generación son problemas distintos

Los hilos de exportación de contenido, libros y resumen de foros muestran que la existencia de un recurso en Moodle no demuestra que se envíe su cuerpo completo. En AERO, una respuesta temática sobre un video no acredita transcripción. Del mismo modo, que un libro tenga una sección sobre un tema no verifica el título bibliográfico que inventó el asistente. Esta interpretación surge del contraste de los casos D3, A2 y los registros locales; no es una nueva inspección del prompt efectivo.

### RAG tiene pertinencia, pero no una eficacia demostrada aquí

LAMB y las iniciativas de Solr/eLeDia tratan la recuperación como una capa específica. La evidencia recuperada justifica evaluarlas, pero no permite afirmar un porcentaje de reducción de errores ni prometer referencias correctas. Faltan pruebas con preguntas sin respuesta, atribuciones, cambios de archivos y separación entre cursos/usuarios. Ningún testimonio encontrado sustituye esas comprobaciones.

### Los tiempos de 23 segundos no identifican una configuración ganadora

El laboratorio conserva dos observaciones distintas: la consulta histórica «qué es la destrucción?» de aproximadamente 23 s del día 5, y la consulta sobre cantidad de clases del día 9, estimada en 23 s por interfaz, con 24,66 s HTTP y 14,35 s internos registrados. No son el mismo ensayo ni tiempos intercambiables. Los reportes externos no permiten explicar causalmente esa diferencia.

Los ejemplos de Raspberry Pi y modelos pequeños muestran que la cantidad de tokens y la plataforma importan, pero no prueban que la RAM adicional o un valor aislado de hilos explique las variaciones de AERO. Los incidentes de la VM, modelo cargado o no, contexto, historial y razonamiento siguen siendo factores sin aislar en los ensayos históricos.

Fuentes locales: [mediciones y discrepancias del 9 de noviembre](ensayos-2026-11-09.md), [registro del 3–5 de noviembre](ensayos-2026-11-03-a-05.md). Fuente externa: [medición de Raspberry Pi](https://moodle.org/mod/forum/discuss.php?d=466353).

### No mezclar nombres y versiones históricas

El modelo fue presentado históricamente como Qwen3 de 1.7B; la inspección registrada del alias qwen3-estudio informó 2.0B/Q4_K_M. Se conserva la discrepancia documental, sin reemplazarla por un dato externo sobre Qwen. Tampoco se da por resuelta la diferencia entre versiones de Ollama informadas. Esta investigación no interrogó nuevamente la VM.

## 10. Conclusión para la decisión posterior

**Con evidencia práctica suficiente para el hecho limitado:** conectar Moodle 4.5 a Ollama mediante API compatible y clave no vacía; usar integraciones locales con modelos pequeños; corregir ciertos fallos concretos de endpoint/autenticación; recuperar formularios tras restaurar componentes del núcleo eliminados. Son resultados acotados, no certificaciones de tutor académico fiable.

**Con pertinencia documental, pero sin validación comparable:** AI Manager/AI Chat como alternativa de integración local y LAMB como sistema existente de recuperación documental. El primero tiene un testimonio cercano a los recursos de AERO; el segundo documenta funciones más directamente relacionadas con materiales y citas. No existe evidencia suficiente para declarar a uno ganador.

**Sin respaldo para presentarlo como solución:** aumentar RAM, cambiar creatividad, acortar un prompt o introducir un aviso de errores como remedio demostrado a las referencias inventadas; asumir que el proveedor nativo nuevo añade lectura completa del curso; adoptar Terus RAG por su ficha ignorando la revisión de v1.0.9.

Antes de decidir continuar con MooChat, sustituirlo o desarrollar algo propio, falta una comparación que identifique versión exacta, documentos realmente extraídos, contexto enviado, reglas de permisos, referencias contrastables, cambios del corpus y recursos consumidos. Estos son vacíos de evidencia detectados, no una arquitectura ni un plan de implementación aprobado.

La investigación **no justifica iniciar todavía un plugin propio**. Existen alternativas y experiencias que merecen evaluación; tampoco justifica afirmar que una de ellas ya resuelve el caso AERO. Los antecedentes de SOLA, AnythingLLM, Open WebUI y Tutor AI permanecen en el registro previo, sin ser descartados: no se recuperaron aquí testimonios de foro suficientes para elevarlos a soluciones verificadas.

## 11. Registro del corpus leído

Los 21 hilos leídos completos corresponden a los identificadores: 465747, 465867, 466353, 468519, 467692, 469036, 473335, 482659, 470513, 467195, 471936, 469308, 466024, 468761, 470188, 473767, 482637, 447662, 464005, 469210 y 482187. Todos tienen enlace directo y valoración en este informe. «Completo» se refiere al texto de las intervenciones accesibles, no a haber auditado cada enlace externo, video o adjunto.

No se encontraron testimonios suficientes para establecer actualización incremental garantizada de todo tipo de recurso, un tiempo de respuesta objetivo de Qwen3/MooChat, o supresión efectiva de alucinaciones con una combinación determinada de parámetros. La ausencia de esos testimonios en el corpus no demuestra que una implementación no funcione.
