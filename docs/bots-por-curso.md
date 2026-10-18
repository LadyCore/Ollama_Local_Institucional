# Bots por curso con Ollama: selección documental

Consulta: 2026-10-18. Registro de alternativas para consulta de materiales por curso con Ollama local. MooChat es el candidato priorizado para el laboratorio; los demás componentes permanecen como antecedentes. Ningún candidato probado en Moodle 4.5.8. La selección considera el recorrido de datos y sus dependencias efectivas; el almacenamiento en Moodle y los servicios externos opcionales no determinan por sí solos la exclusión.

## Opciones

| Opción | Evidencia de conexión local y alcance | Pendientes |
|---|---|---|
| MooChat, mod_moochat | v1.8.2 / 2026042801, **Beta**, soporte declarado Moodle 4.5–5.2. Actividad con documentos de referencia y proveedor del subsistema IA | Candidato principal. [Revisión inicial del código](revision-moochat.md); compatibilidad exacta 4.5.8, paquete y seguridad integral sin ensayo |
| Exabis AI Chat, block_exaaichat | Soporte documentado de Ollama autoalojado y configuración del bot por curso. Versión 5.2 / 2026091000 declarada para Moodle 4.5 | No equiparar chat con consulta documental local. El README consultado documenta Simple RAG con archivos/vector store de OpenAI; verificar funciones exactas del paquete antes de atribuir RAG local |
| AI Chat + AI Manager, block_ai_chat + local_ai_manager | El chat documenta instancias por curso, instrucciones/personas y contexto. AI Manager documenta proveedor Ollama | No se fijó conjunto de versiones compatibles con 4.5.8. El chat actual también requiere tiny_ai. Mayor cantidad de componentes; no es instalación propuesta para ahora |

Fuentes primarias:

- [MooChat: ficha y funciones](https://marketplace.moodle.com/plugins/mod_moochat).
- [Exabis: README del autor](https://github.com/gtn/moodle-block_exaaichat).
- [Exabis: versiones](https://marketplace.moodle.com/plugins/3286/versions?show=all).
- [AI Chat: documentación del autor](https://github.com/bycs-lp/moodle-block_ai_chat).
- [AI Manager: proveedores y requisitos](https://github.com/bycs-lp/moodle-local_ai_manager).

## Decisión de evaluación y fundamentos

MooChat queda priorizado por su configuración por actividad, incorporación de material y conexión al subsistema IA de Moodle. Asyntai (`local_asyntai`, ficha 3401) documenta conexión a su servicio y bot global; no acredita Ollama local. Detalle en la [revisión dirigida](revision-moochat.md).

El alcance de MooChat comprende consulta de material proporcionado por el docente. La calificación queda fuera de la primera evaluación. La restricción a documentos utiliza instrucciones al modelo y no acredita una garantía técnica contra respuestas ajenas al material. La aprobación de seguridad permanece pendiente de validación.

Exabis permite estudiar el concepto de bot configurado por curso con Ollama para conversación y contexto. La disponibilidad del proveedor local no garantiza que la función de archivos use ese mismo proveedor.

La validación del recorrido local requiere revisión del paquete y configuración, y ensayo de salida de red. La primera evaluación se limita a MooChat, después de validar Ollama; los demás componentes carecen de ejecución programada.
