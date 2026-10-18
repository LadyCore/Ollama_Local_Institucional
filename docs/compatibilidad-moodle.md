# Matriz de compatibilidad Moodle

Consulta: 2026-10-18. Objetivo solicitado: Moodle 4.5.8. Estado: compatibilidad documental de la rama 4.5; ningún ensayo local realizado. La versión objetivo no sustituye una comprobación del código instalado antes de instalar plugins.

Antes de clasificar candidatos, recuperar o verificar las versiones exactas del Moodle del clon y de sus dependencias. No utilizar como sustituto las versiones del laboratorio de actualización a Moodle 5.3.

## Búsqueda acotada de bots por curso

Ver [MooChat, Exabis y AI Chat](bots-por-curso.md): soporte local documentado, funciones y pendientes separados. MooChat se incorpora como candidato documental; ningún paquete nuevo ha sido aprobado o instalado.

## Revisión posterior de Terus RAG

La [revisión dirigida de v1.0.9](revision-terusrag.md) encuentra búsqueda global sin delimitación por curso y un indexador Ollama limitado a resúmenes/nombres de cursos. No recomendar esta versión sin cambios para consultar material de un curso. Las filas siguientes conservan la compatibilidad declarada del catálogo, no una aprobación técnica.

## Candidatos documentados

Los rangos publicados incluyen Moodle 4.5, no un certificado de funcionamiento específico en 4.5.8. Antes de instalar: revisar version.php, dependencias, PHP, licencia del paquete, avisos de seguridad y cambios de la versión exacta.

| Componente | Versión consultada | Uso posible | Conexión y respaldo documental |
|---|---|---|---|
| Proveedor incluido aiprovider_openai | Incluido en Moodle 4.5 | Generación de texto y resumen mediante las ubicaciones de IA del editor y asistencia de curso | API compatible de Ollama; procedimiento en [MoodleDocs 4.5](https://docs.moodle.org/405/en/Ollama). No requiere cuenta OpenAI para este destino local |
| tiny_aipromptgen | 1.9, build 2026030501; Stable | Construir instrucciones guiadas y generar borradores dentro de TinyMCE | Ollama explícito; Moodle 4.5 incluido en [versiones](https://marketplace.moodle.com/plugins/3543/versions). [Ficha](https://marketplace.moodle.com/plugins/3543) indica PHP mínimo 8.1 |
| block_exaaichat | 5.2, build 2026091000; Stable | Chat configurable por curso; contexto y consulta de documentos mediante RAG según historial funcional | Ollama explícito; Moodle 4.5 incluido en [versiones](https://marketplace.moodle.com/plugins/3286/versions?show=all) |
| block_terusrag | 1.0.9, build 2026040106; Stable | Consultar contenido de cursos mediante recuperación de fragmentos (RAG) | Ollama explícito; Moodle 4.2–4.5 en [versiones](https://marketplace.moodle.com/plugins/3202/versions?show=all) |
| local_textinsights | 1.3.0, build 2025080103; Alpha | Explicar y resumir texto seleccionado; ofrece también acción Validate | Ollama explícito; Moodle 4.5 incluido en [versiones](https://marketplace.moodle.com/plugins/3363/versions) |

## Seguridad y limitaciones por candidato

- **Proveedor incluido:** MoodleDocs requiere ajustar la seguridad HTTP para alcanzar loopback y el puerto del servicio. Es un cambio de seguridad global que debe evaluarse y acotarse, no una instrucción para vaciar listas de bloqueo. La clave ficticia del ejemplo satisface el formulario, no autentica Ollama. Limitar la prueba a texto/resumen; no extrapolar otras funciones.
- **Tiny AI Prompt Generator:** trabaja con TinyMCE, no con Atto. Su historial documenta omisión automática de validación SSL para endpoints Custom locales/privados: revisar el código del paquete antes de aprobar conexiones HTTPS internas. La declaración Privacy API null no equivale a auditoría de seguridad. Restringir proveedores alternativos, roles y salida renderizada.
- **Exabis:** su historial declara retención de logs e historial en localStorage del navegador; admite incorporar nombres/calificaciones al contexto. Revisar y limitar estos datos, la configuración de proveedores por curso y la separación de usuarios. Las funciones RAG exigen comprobar también extracción, almacenamiento y destinos de embeddings. No se ha auditado la versión 5.2.
- **Terus RAG:** verificar permisos de cada recurso y actividad, qué se indexa, dónde quedan fragmentos/embeddings y qué proveedor interviene en cada etapa. Que la generación use Ollama no acredita por sí sola que toda la cadena sea local.
- **Text Insights:** sigue marcado Alpha. La acción Validate es una respuesta generativa, no una verificación factual certificada. Revisar contexto añadido, permisos por acción y ubicación; mantenerlo como exploratorio.

## Alternativas no incorporadas a la lista corta

- [Provider API OpenWebUI](https://marketplace.moodle.com/plugins/aiprovider_openwebui): declara Moodle 4.5–5.1, pero añade un servicio intermedio. Paquete exacto, configuración integral local y seguridad pendientes de revisión.
- [AI Manager](https://github.com/bycs-lp/moodle-local_ai_manager): documenta Ollama, gestión por roles/tenant y Moodle mínimo 4.4. Es un ecosistema alternativo; advierte que sus consumidores y los del subsistema core no son intercambiables. Falta fijar versiones coordinadas de gestor y complementos para 4.5.8.
- [AI Chat Block](https://github.com/Limekiller/moodle-block_openai_chat): las fuentes consultadas muestran diferencias entre descripciones/versiones; no se recomienda un paquete concreto sin resolver su mecanismo de proveedor y dependencia en 4.5.

## Orden sugerido de evaluación

1. Proveedor incluido: comprobar el recorrido Moodle → Ollama con generación/resumen acotados.
2. Elegir una interfaz según el uso a explorar: editor (Tiny) o chat (Exabis), después de revisar sus puntos de seguridad.
3. RAG documental (Terus o Exabis), una vez validada la separación de datos y el consumo.
4. Text Insights como prueba exploratoria por su estado Alpha.

Es una recomendación técnica de menor a mayor alcance, no selección pedagógica ni autorización de instalación. No se promete capacidad concurrente con el hardware disponible. No se crean cursos de prueba.

Para cada candidato registrar instalación, configuración con parámetros sustituibles, restricciones, prueba sintética, consumo, errores y desinstalación/recuperación. La compatibilidad con una API no prueba por sí sola que todas las funciones del plugin operen con un modelo local.

La evaluación técnica delimita qué se puede habilitar; las áreas destinatarias decidirán qué usos necesitan dentro de ese conjunto.
