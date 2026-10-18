# MooChat: revisión inicial dirigida

Fecha: 2026-10-18. Estado: código inspeccionado parcialmente; instalación y ensayo pendientes. Candidato priorizado para consulta acotada de material de curso. Aprobación para producción pendiente.

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

### Condición de seguridad previa

El [reporte público #13 y su contraste con el código](antecedentes-github.md) identifican una ruta de extracción PPTX con sustitución de entidades XML. La integración queda condicionada a su resolución o exclusión verificable y a completar la revisión del paquete. El reporte no se reprodujo en el laboratorio. La preferencia funcional por MooChat no acredita habilitación de esta versión.

El recorrido definido para el laboratorio es Moodle → Ollama local. La primera prueba se limita a consulta de material con datos sintéticos. Permanecen pendientes de definición los parámetros de la actividad: calificación, objetivos, selección de archivos, incorporación de sección y límite horario. Los casos de validación comprenden extracción fallida, pregunta fuera del material, acceso sin permiso y contenido demasiado largo, junto con salida de red y persistencia en Moodle, servicio de inferencia, temporales y copias.

El modo de sección puede incorporar más contenido que los archivos elegidos y tiene otras rutas de extracción; su habilitación requiere una decisión de configuración específica. La lectura completa de documentos en cada envío puede afectar memoria y longitud de contexto. La capacidad de la VM queda pendiente de medición.

## Alternativa evaluada: Asyntai

La [ficha 3401](https://marketplace.moodle.com/plugins/3401) identifica `local_asyntai`, Asyntai AI Chatbot for Moodle. Describe vinculación de cuenta con Asyntai, administración en su dashboard y activación automática en todas las páginas. No documenta conexión a Ollama autoalojado. Su soporte declarado incluye 4.5, pero la información consultada no acredita el recorrido local requerido. No se selecciona para la primera prueba; no se auditó su código.

## Límite y siguiente paso

Revisión estática parcial, sin ejecución del código ni cambios en la VM. La revisión del paquete íntegro y la integración efectiva con Moodle 4.5.8 permanecen pendientes. La secuencia establece la validación independiente de Ollama local antes del ensayo del plugin. El desarrollo de un fork y las pruebas simultáneas de otros candidatos quedan fuera del alcance.
