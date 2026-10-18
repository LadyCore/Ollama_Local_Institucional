# Bots por curso con Ollama: selección documental

Consulta: 2026-10-18. Objetivo: localizar opciones, no decidir instalación ni uso académico. Ningún candidato probado en Moodle 4.5.8. El almacenamiento en Moodle o la existencia de otros proveedores configurables no son motivos de descarte: importa el recorrido elegido y sus dependencias efectivas.

## Opciones

| Opción | Evidencia de conexión local y alcance | Pendientes |
|---|---|---|
| MooChat, mod_moochat | La ficha declara Moodle 4.5–5.2, actividades de chat dentro del curso y Ollama local mediante el subsistema IA de Moodle. Admite documentos de referencia PDF/texto y configuración docente | Fijar release/build compatible con 4.5.8 y revisar recorrido del contenido, restricciones y persistencia. La página de versiones no pudo recuperarse en esta consulta |
| Exabis AI Chat, block_exaaichat | Soporte documentado de Ollama autoalojado y configuración del bot por curso. Versión 5.2 / 2026091000 declarada para Moodle 4.5 | No equiparar chat con consulta documental local. El README consultado documenta Simple RAG con archivos/vector store de OpenAI; verificar funciones exactas del paquete antes de atribuir RAG local |
| AI Chat + AI Manager, block_ai_chat + local_ai_manager | El chat documenta instancias por curso, instrucciones/personas y contexto. AI Manager documenta proveedor Ollama | No se fijó conjunto de versiones compatibles con 4.5.8. El chat actual también requiere tiny_ai. Mayor cantidad de componentes; no es instalación propuesta para ahora |

Fuentes primarias:

- [MooChat: ficha y funciones](https://marketplace.moodle.com/plugins/mod_moochat).
- [Exabis: README del autor](https://github.com/gtn/moodle-block_exaaichat).
- [Exabis: versiones](https://marketplace.moodle.com/plugins/3286/versions?show=all).
- [AI Chat: documentación del autor](https://github.com/bycs-lp/moodle-block_ai_chat).
- [AI Manager: proveedores y requisitos](https://github.com/bycs-lp/moodle-local_ai_manager).

## Interpretación para la prueba pequeña

MooChat es un candidato documental especialmente cercano a chat con material proporcionado por el docente, sin que eso constituya aprobación de seguridad. La ficha presenta funciones de calificación e historial; la calificación queda fuera del alcance. Su restricción verbal a documentos no debe presentarse como una garantía técnica contra respuestas ajenas al material.

Exabis permite estudiar el concepto de bot configurado por curso con Ollama para conversación y contexto. La disponibilidad del proveedor local no garantiza que la función de archivos use ese mismo proveedor.

No se declara ausencia total de conexiones externas para ninguna instalación sin revisar paquete y configuración y ensayar la salida de red. No se instalará un conjunto de plugins por el solo hecho de aparecer aquí. Los demás quedan como referencias futuras.
