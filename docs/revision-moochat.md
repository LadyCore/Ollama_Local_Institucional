# MooChat: revisión inicial dirigida

Fecha: 2026-10-18. Estado: código inspeccionado parcialmente; instalación y ensayo pendientes. Candidato principal para una prueba pequeña de consulta de material, según preferencia confirmada. No constituye aprobación para producción.

## Identificación reproducible

- Componente: `mod_moochat`, actividad de curso.
- Marketplace: v1.8.2, build `2026042801`, madurez **Beta**, soporte declarado Moodle 4.5, 5.0, 5.1 y 5.2.
- Código inspeccionado: commit `01ac171790fa7c01ea681b6b6ff523512ef52b67` del repositorio del autor. `version.php` coincide en release/build/madurez; no se verificó identidad binaria con el ZIP del catálogo.
- El mínimo 4.4 de `version.php` no elimina la dependencia del subsistema IA. Se verificó en la rama `MOODLE_405_STABLE` la existencia de `core\di::get()` y el constructor de `generate_text` utilizado; no equivale a una ejecución en 4.5.8.

Fuentes: [versiones publicadas](https://marketplace.moodle.com/plugins/3741/versions), [version.php fijado](https://github.com/bapool/moodle-mod_moochat/blob/01ac171790fa7c01ea681b6b6ff523512ef52b67/version.php), [API generate_text de Moodle 4.5](https://github.com/moodle/moodle/blob/MOODLE_405_STABLE/ai/classes/aiactions/generate_text.php).

## Recorrido observado y consecuencias

1. `send_message.php` obtiene la instancia y su contexto de actividad, valida ese contexto y exige `mod/moochat:submit`.
2. Los archivos propios se buscan por contexto de esa actividad. La extracción observada es local: lectura de texto o PDF mediante `pdftotext`/biblioteca incluida.
3. El texto extraído se concatena con instrucciones, historial recibido del navegador y pregunta. Se entrega a `core_ai\manager::process_action()` como generación de texto. En este recorrido no se observa una API directa de embeddings ni una base vectorial adicional. El destino efectivo depende del proveedor habilitado en Moodle.
4. La opción de restringir al material añade instrucciones al mismo texto de consulta; no es una barrera técnica contra inyección de instrucciones ni garantiza respuestas correctas. Si no se extrae texto, no se incorpora esa restricción en la rama inspeccionada: incluir ese caso en el ensayo.
5. `save_conversation.php` guarda mensajes asociados al usuario actual y a la actividad. Recibe tanto la pregunta como la respuesta desde el navegador: el historial almacenado no es evidencia inalterable de lo generado. Valida contexto y sesión, pero no contiene la comprobación explícita de `submit` que sí usa el envío; requiere revisión adicional antes de habilitar.
6. `history.php` exige acceso al curso/actividad y `viewhistory`, y filtra las conversaciones por actividad y usuario elegido. Falta ensayar restricciones y separación de grupos; no deducir aislamiento completo de esta lectura.

Código: [envío](https://github.com/bapool/moodle-mod_moochat/blob/01ac171790fa7c01ea681b6b6ff523512ef52b67/classes/external/send_message.php), [biblioteca y archivos](https://github.com/bapool/moodle-mod_moochat/blob/01ac171790fa7c01ea681b6b6ff523512ef52b67/lib.php), [guardado](https://github.com/bapool/moodle-mod_moochat/blob/01ac171790fa7c01ea681b6b6ff523512ef52b67/classes/external/save_conversation.php), [historial](https://github.com/bapool/moodle-mod_moochat/blob/01ac171790fa7c01ea681b6b6ff523512ef52b67/history.php), [permisos](https://github.com/bapool/moodle-mod_moochat/blob/01ac171790fa7c01ea681b6b6ff523512ef52b67/db/access.php).

## Configuración de referencia para el primer ensayo

Propuesta pendiente: proveedor dirigido únicamente a Ollama local; actividad sin calificación ni objetivos de evaluación; un texto sintético corto cargado expresamente; incorporación automática de sección desactivada; límite horario de consultas. Probar extracción fallida, pregunta fuera del material, acceso sin permiso y contenido demasiado largo. Verificar salida de red y persistencia en Moodle, proveedor, temporales y copias.

El modo de sección puede incorporar más contenido que los archivos elegidos y tiene otras rutas de extracción; queda fuera de esta primera configuración. La lectura completa de documentos en cada envío puede afectar memoria y longitud de contexto: no se promete capacidad sobre la VM sin medir.

## Comparación solicitada: Asyntai

La [ficha 3401](https://marketplace.moodle.com/plugins/3401) identifica `local_asyntai`, Asyntai AI Chatbot for Moodle. Describe vinculación de cuenta con Asyntai, administración en su dashboard y activación automática en todas las páginas. No documenta conexión a Ollama autoalojado. Su soporte declarado incluye 4.5, pero la información consultada no acredita el recorrido local requerido. No se selecciona para la primera prueba; no se auditó su código.

## Límite y siguiente paso

Revisión estática parcial, sin ejecutar código de terceros ni modificar la VM. Falta revisar el paquete íntegro y su integración efectiva con Moodle 4.5.8. Mantener Ollama local como siguiente validación operativa, antes de ensayar el plugin. No ampliar a desarrollo de un fork ni a pruebas simultáneas de otros candidatos.
