# Antecedentes técnicos en GitHub

Consulta: 2026-10-18. Alcance: documentación y reportes públicos; sin instalación ni reproducción de incidentes. Los ejemplos de implementación no acreditan cumplimiento de seguridad en este laboratorio.

## ChatOllama

Repositorio: [sugarforever/chat-ollama](https://github.com/sugarforever/chat-ollama). Revisión consultada: `96c3ce50c3ba4ec3b19f126f50c035f84183f9fc`.

El [README vigente](https://github.com/sugarforever/chat-ollama/blob/96c3ce50c3ba4ec3b19f126f50c035f84183f9fc/README.md) orienta el proyecto a agentes mediante una aplicación de terminal, con modelos locales o alojados. La documentación de la plataforma web y bases de conocimiento permanece en [CHATBOT.md](https://github.com/sugarforever/chat-ollama/blob/96c3ce50c3ba4ec3b19f126f50c035f84183f9fc/CHATBOT.md): describe carga de documentos, recuperación de fragmentos, PostgreSQL y Chroma/Milvus. Es una aplicación independiente; las fuentes consultadas no acreditan integración con permisos por curso de Moodle.

Aporte al laboratorio: referencia de separación entre interfaz, modelo, almacenamiento y recuperación documental. No se incorpora como dependencia. La arquitectura adicional queda fuera de la primera prueba. El soporte de Ollama y de servicios externos opcionales requiere identificar la configuración efectiva de cada función antes de atribuir procesamiento completamente local.

## Fuentes directamente aplicables

| Fuente | Aplicación |
|---|---|
| [Ollama oficial](https://github.com/ollama/ollama) | API, versiones y avisos del motor de inferencia |
| [Integración oficial de Moodle 4.5](https://docs.moodle.org/405/en/Ollama) | Configuración del recorrido Moodle → Ollama |
| [Código de MooChat](https://github.com/bapool/moodle-mod_moochat) | Permisos, extracción de materiales y persistencia del candidato seleccionado |
| [Incidencias de MooChat](https://github.com/bapool/moodle-mod_moochat/issues) | Problemas reportados que requieren contraste con versión y código |

## Hallazgo de seguridad: extracción de PPTX en MooChat

El [reporte abierto #13](https://github.com/bapool/moodle-mod_moochat/issues/13), del 2026-05-02, describe posible lectura de archivos locales mediante XML de un PPTX manipulado. Es una afirmación del reportante, sin reproducción en este laboratorio.

La inspección de [lib.php en la revisión fijada](https://github.com/bapool/moodle-mod_moochat/blob/01ac171790fa7c01ea681b6b6ff523512ef52b67/lib.php) confirma `loadXML` con `LIBXML_NOENT` en la extracción de presentaciones desde recursos de sección. Esa revisión continúa siendo la cabeza del repositorio al consultar. La coincidencia fundamenta una revisión de seguridad pendiente; no confirma todos los pasos de explotación ni los permisos atribuidos por el reporte.

La integración de MooChat queda condicionada a resolver o excluir de manera verificable esta ruta y completar la revisión del paquete. La desactivación de incorporación de sección es una opción de configuración pendiente de validación, no una corrección acreditada. No se ejecutaron pruebas con archivos manipulados ni se desarrolló un parche.

## Criterio de uso de antecedentes

Cada antecedente registra revisión, componente, función y evidencia. Los reportes de terceros se distinguen de los hallazgos confirmados por inspección y de los resultados reproducidos. La selección funcional de MooChat se conserva; su habilitación requiere cerrar los pendientes técnicos y de seguridad.
