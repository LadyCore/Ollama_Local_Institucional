# Terus RAG: revisión dirigida de viabilidad

Fecha: 2026-10-18. Código consultado: etiqueta v1.0.9, build 2026040106. Revisión estática dirigida, sin instalación ni pruebas de explotación. No equivale a auditoría completa. La ficha del catálogo declara Moodle 4.5; version.php requiere Moodle 4.2 como mínimo.

## Resultado

Esta versión queda excluida de la primera prueba de consulta de materiales restringida a un curso. Fundamento: la capacidad anunciada no coincide con el recorrido Ollama observado y falta delimitación de búsqueda por curso/usuario. El desarrollo de un fork queda fuera del alcance.

## Procesamiento local

El proveedor Ollama usa el destino configurado para `/api/embed` y `/api/generate`; la optimización del prompt en llm.php es procesamiento PHP local. En ese recorrido no se observó fallback automático hacia otro proveedor. Puede plantearse generación y embeddings locales, pero la ausencia efectiva de tráfico externo requiere ensayo con control de salida.

Los valores predeterminados no constituyen una configuración local segura: el proveedor seleccionado por defecto es Gemini y el campo de endpoint Ollama contiene una dirección externa. Deben seleccionarse explícitamente Ollama, destino local y modelos descargados. El cliente deshabilita la verificación TLS y omite controles HTTP de Moodle si el texto del destino contiene localhost. Esta comprobación textual no es una validación robusta de destino. No extrapolar seguridad a conexiones remotas HTTPS.

Fuentes: [ollama.php](https://github.com/khairu-aqsara/moodle-blocks_terusrag/blob/v1.0.9/classes/ollama.php), [llm.php](https://github.com/khairu-aqsara/moodle-blocks_terusrag/blob/v1.0.9/classes/llm.php), [settings.php](https://github.com/khairu-aqsara/moodle-blocks_terusrag/blob/v1.0.9/settings.php).

## Alcance del material y permisos

- `data_initialization()` del proveedor Ollama consulta cursos visibles y procesa su resumen; si falta, utiliza el nombre completo. En esta implementación no se encontró extracción de PDF/DOCX ni recorrido de recursos/actividades para indexar sus cuerpos.
- `get_top_ranked_chunks()` busca sobre la tabla completa, sin filtro de curso, matrícula o disponibilidad para el usuario. Que un curso tenga visible=1 no demuestra autorización individual.
- `submit_query()` recibe courseid, pero no lo pasa al proveedor; se describe como reservado para uso futuro. Valida contexto de sistema y exige addinstance en ese contexto, no un permiso de consulta limitado al curso. Esto puede impedir el uso esperado de roles docentes locales/alumnos; no se debe resolver otorgando permisos globales indiscriminadamente.
- Insertar el bloque en un curso no restringe por sí mismo el índice ni sus resultados. La búsqueda global implica riesgo de mezcla de información para quien logre acceder al endpoint; no se afirma que todos los alumnos tengan acceso por defecto.

Fuentes: [proveedor Ollama](https://github.com/khairu-aqsara/moodle-blocks_terusrag/blob/v1.0.9/classes/ollama.php), [endpoint de consultas](https://github.com/khairu-aqsara/moodle-blocks_terusrag/blob/v1.0.9/classes/external.php), [permisos](https://github.com/khairu-aqsara/moodle-blocks_terusrag/blob/v1.0.9/db/access.php).

## Almacenamiento y componentes

El recorrido inspeccionado guarda fragmentos de contenido, embeddings serializados, título, referencias de origen, hash y fechas en la tabla Moodle block_terusrag, con el prefijo efectivo de la instalación. Utiliza la base existente; no necesita ChromaDB ni Supabase para ese recorrido. Los selectores de almacenamiento presentes en configuración no acreditan implementación efectiva de esos servicios.

Se necesitan Ollama, un modelo de generación y uno de embeddings, además del cron de Moodle para la tarea de indexación. No se observó una tabla dedicada a conversaciones en install.xml; esto no demuestra ausencia de rastros: el cliente activa caché HTTP y algunos diagnósticos incluyen contenido o respuestas. Revisar cachés, logs y eliminación antes de cualquier uso real.

Fuentes: [esquema](https://github.com/khairu-aqsara/moodle-blocks_terusrag/blob/v1.0.9/db/install.xml), [tarea](https://github.com/khairu-aqsara/moodle-blocks_terusrag/blob/v1.0.9/classes/task/datainitializer.php), [proveedor](https://github.com/khairu-aqsara/moodle-blocks_terusrag/blob/v1.0.9/classes/ollama.php).

## Decisión de alcance

La primera entrega comprende procesamiento local sin conexiones externas y una consulta acotada de material de curso con permisos comprobables. La validación de Ollama precede al ensayo del plugin seleccionado. Los demás plugins son antecedentes sin ejecución programada.

Antecedente de selección: Terus RAG se identificó inicialmente por su ficha del catálogo; la revisión de código determinó su exclusión de la primera prueba por los hallazgos registrados. Referencia general: [catálogo y versiones](https://marketplace.moodle.com/plugins/3202/versions?show=all).
