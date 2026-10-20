# Matriz de compatibilidad Moodle

Consulta inicial: 2026-10-18; actualización de ensayo: 2026-10-19. Plataforma objetivo: Moodle 4.5.8. MooChat v1.8.2 instalado por ZIP e integración sintética con Ollama operativa. No constituye validación completa de compatibilidad. [Configuración, evidencia y límites](integracion-aero.md).

La verificación de versiones de Moodle y sus dependencias permanece pendiente. El laboratorio de actualización a Moodle 5.3 es un entorno independiente y sus versiones no se atribuyen a este clon.

## Búsqueda acotada de bots por curso

La selección de laboratorio prioriza MooChat para consulta de material por curso, después de validar Ollama local. [MooChat, Exabis y AI Chat](bots-por-curso.md) registra antecedentes. Instalación e integración textual de MooChat completadas; consulta de archivos y controles por curso pendientes.

## Revisión posterior de Terus RAG

La [revisión dirigida de v1.0.9](revision-terusrag.md) identifica búsqueda global sin delimitación por curso y un indexador Ollama limitado a resúmenes/nombres de cursos. Esta versión queda excluida de la primera prueba de consulta de materiales. Las filas siguientes conservan la compatibilidad declarada del catálogo como antecedente documental.

## Candidatos documentados

Los rangos publicados incluyen Moodle 4.5, no un certificado de funcionamiento específico en 4.5.8. Antes de instalar: revisar version.php, dependencias, PHP, licencia del paquete, avisos de seguridad y cambios de la versión exacta.

| Componente | Versión consultada | Uso posible | Conexión y respaldo documental |
|---|---|---|---|
| mod_moochat | v1.8.2, build 2026042801; Beta | Actividad AERO instalada; ensayo textual sintético satisfactorio | Subsistema IA de Moodle con Ollama local; [versiones](https://marketplace.moodle.com/plugins/3741/versions), [revisión de código](revision-moochat.md) y [resultados](integracion-aero.md). Documentos, permisos y concurrencia pendientes |
| Proveedor incluido aiprovider_openai | Incluido en Moodle 4.5 | Generación de texto y resumen mediante las ubicaciones de IA del editor y asistencia de curso | API compatible de Ollama; procedimiento en [MoodleDocs 4.5](https://docs.moodle.org/405/en/Ollama). No requiere cuenta OpenAI para este destino local |
| tiny_aipromptgen | 1.9, build 2026030501; Stable | Construir instrucciones guiadas y generar borradores dentro de TinyMCE | Ollama explícito; Moodle 4.5 incluido en [versiones](https://marketplace.moodle.com/plugins/3543/versions). [Ficha](https://marketplace.moodle.com/plugins/3543) indica PHP mínimo 8.1 |
| block_exaaichat | 5.2, build 2026091000; Stable | Chat configurable por curso; la consulta documental local no está acreditada | Ollama explícito para chat; Moodle 4.5 incluido en [versiones](https://marketplace.moodle.com/plugins/3286/versions?show=all). El README documenta archivos/vector store de OpenAI para Simple RAG |
| block_terusrag | 1.0.9, build 2026040106; Stable | Consultar contenido de cursos mediante recuperación de fragmentos (RAG) | Ollama explícito; Moodle 4.2–4.5 en [versiones](https://marketplace.moodle.com/plugins/3202/versions?show=all) |
| local_textinsights | 1.3.0, build 2025080103; Alpha | Explicar y resumir texto seleccionado; ofrece también acción Validate | Ollama explícito; Moodle 4.5 incluido en [versiones](https://marketplace.moodle.com/plugins/3363/versions) |

## Seguridad y limitaciones por candidato

- **Proveedor incluido:** MoodleDocs requiere ajustar la seguridad HTTP para alcanzar loopback y el puerto del servicio. Es un cambio de seguridad global que debe evaluarse y acotarse, no una instrucción para vaciar listas de bloqueo. La clave ficticia del ejemplo satisface el formulario, no autentica Ollama. Limitar la prueba a texto/resumen; no extrapolar otras funciones.
- **Tiny AI Prompt Generator:** trabaja con TinyMCE, no con Atto. Su historial documenta omisión automática de validación SSL para endpoints Custom locales/privados: revisar el código del paquete antes de aprobar conexiones HTTPS internas. La declaración Privacy API null no equivale a auditoría de seguridad. Restringir proveedores alternativos, roles y salida renderizada.
- **Exabis:** su historial declara retención de logs e historial en localStorage del navegador; admite incorporar nombres/calificaciones al contexto. Revisar y limitar estos datos, la configuración de proveedores por curso y la separación de usuarios. Las funciones RAG exigen comprobar también extracción, almacenamiento y destinos de embeddings. No se ha auditado la versión 5.2.
- **Terus RAG:** verificar permisos de cada recurso y actividad, qué se indexa, dónde quedan fragmentos/embeddings y qué proveedor interviene en cada etapa. Que la generación use Ollama no acredita por sí sola que toda la cadena sea local.
- **Text Insights:** sigue marcado Alpha. La acción Validate es una respuesta generativa, no una verificación factual certificada. La revisión de contexto y permisos queda pendiente; componente fuera de la primera prueba.

## Alternativas no incorporadas a la lista corta

- [Provider API OpenWebUI](https://marketplace.moodle.com/plugins/aiprovider_openwebui): declara Moodle 4.5–5.1, pero añade un servicio intermedio. Paquete exacto, configuración integral local y seguridad pendientes de revisión.
- [AI Manager](https://github.com/bycs-lp/moodle-local_ai_manager): documenta Ollama, gestión por roles/tenant y Moodle mínimo 4.4. Es un ecosistema alternativo; advierte que sus consumidores y los del subsistema core no son intercambiables. Falta fijar versiones coordinadas de gestor y complementos para 4.5.8.
- [AI Chat Block](https://github.com/Limekiller/moodle-block_openai_chat): las fuentes consultadas muestran diferencias entre descripciones/versiones. Paquete sin seleccionar; mecanismo de conexión y dependencias en 4.5 pendientes de resolución.

## Secuencia de evaluación definida

1. Preparar la recuperación del entorno antes de la instalación.
2. Instalar Ollama y comprobar inferencia local con datos sintéticos.
3. Verificar aislamiento de red, persistencia y consumo en convivencia con Moodle/MySQL.
4. Completar la revisión de MooChat y comprobar el recorrido Moodle → Ollama mediante el subsistema IA.
5. Ensayar una consulta acotada de material con MooChat y registrar los resultados de acceso, separación de datos y funcionamiento.

Esta secuencia corresponde al laboratorio. Los demás plugins permanecen como antecedentes de investigación, sin ejecución programada. La capacidad concurrente queda pendiente de medición. La creación de cursos de prueba está fuera del alcance.

El registro de cada componente ensayado incluye instalación, configuración con parámetros sustituibles, restricciones, prueba sintética, consumo, errores y desinstalación/recuperación. La validación comprende todas las etapas de procesamiento utilizadas, además de la conexión con el modelo local.

La evaluación técnica delimita qué se puede habilitar; las áreas destinatarias decidirán qué usos necesitan dentro de ese conjunto.
