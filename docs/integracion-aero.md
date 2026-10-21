# Integración AERO — 19 de octubre de 2026

Registro histórico. La configuración posterior, los fallos de calidad y los cambios de recuperación están en [ensayos del 20 de octubre](ensayos-aero-2026-10-20.md). No usar los valores de esta sesión como estado vigente sin consultar ese documento.

## Alcance y evidencia

Estado: verificado mediante salidas y capturas aportadas por la administradora; no acceso directo del asistente a la VM. Laboratorio personal VirtualBox, no producción. Evidencia transcrita y anonimizada, sin capturas ni material institucional. Objetivo Moodle 4.5.8; MooChat v1.8.2, build 2026042801, Beta, visible instalado. Las versiones exactas restantes requieren comprobación independiente.

Se creó un punto de recuperación de la VM a las 16:39 antes de instalar el plugin por ZIP. Hubo un arranque de VM registrado a las 17:03:05 de causa no determinada, y un apagado accidental posterior informado. No se atribuyen a Ollama. Ollama quedó inactivo tras reinicio por no tener arranque automático; `systemctl restart ollama` y `systemctl is-active ollama` confirmaron recuperación. No se habilitó inicio automático.

## Configuración de la prueba

- Proveedor `aiprovider_openai` habilitado y dirigido a `http://127.0.0.1:11434/v1/chat/completions`; modelo `qwen3-lab`. Clave de relleno `ollama`, no secreto ni mecanismo de autenticación; organización vacía. Azure deshabilitado.
- Solo Generate text habilitado; Generate image y Summarise text deshabilitados. Instrucción global de resumen/texto plano conservada con `/no_think` añadido.
- Actividad AERO — Asistente de aprendizaje; identidad y avatar propios. Sin archivos de contenido, Include Section Content desmarcado, Only Use Uploaded Content desmarcado, objetivos vacíos, Grade None, grupos No groups. Avatar no usado como material de consulta. Visibilidad del laboratorio sin usuarios adicionales; no acredita aislamiento entre roles.
- Instrucción de actividad: responder en español, breve y texto plano, reconocer información insuficiente; identidad AERO y `/no_think`. El avatar se generó fuera de la VM con una herramienta de imágenes; esto no es capacidad de generación local ni prueba de funcionamiento offline de Moodle.

## Diagnóstico de conexión y correcciones

1. Error inicial: `Error code and message must exist in an error response`. El código de Moodle exige código no cero y mensaje en respuestas fallidas; este aviso no identifica por sí solo la causa original.
2. Ollama activo; `curl --max-time 10 http://127.0.0.1:11434/api/tags` devolvió modelos, incluido qwen3-lab. Prueba desde terminal, no desde PHP.
3. Seguridad HTTP: se retiró `127.0.0.0/8` de hosts bloqueados y se añadió 11434 a puertos permitidos, conservando 80 y 443 y los otros bloqueos. Mantener `localhost` resultó insuficiente: el código realiza resolución inversa de IP y compara el nombre. Tras retirar únicamente `localhost`, el error cambió a cURL 7. Cambios globales del sitio, no de la actividad; no vaciar la lista completa. Recuperación prevista: reponer las entradas retiradas y retirar 11434 si se abandona la conexión local.
4. Auditoría mostró denegación AVC `name_connect` para php-fpm, destino 11434, `permissive=0`. `getenforce` devolvió Enforcing y `getsebool httpd_can_network_connect` devolvió off. Los registros iniciales sin coincidencias precedían a la petición que superó el bloqueo de Moodle; no descartaban SELinux.
5. `setsebool httpd_can_network_connect on` permitió obtener respuestas. No se usó `-P`: no persiste tras reinicio. No se desactivó SELinux. El booleano permite conexiones de red del dominio web en general, no exclusivamente loopback o 11434. Reversión disponible: `setsebool httpd_can_network_connect off`; no ejecutada al cierre observado. Pendiente diseño de permiso mínimo y persistencia aprobada.

## Resultados funcionales y tiempos

| Prueba | Resultado observado |
|---|---|
| Saludo | Respuesta que repetía instrucciones sobre brevedad e información insuficiente; inadecuada como saludo |
| Cuatro clases de treinta minutos: duración de cada clase | Cada clase durará 30 minutos; correcta |
| Precio de inscripción no proporcionado | Reconoció que el costo no se indicó; correcta en este caso |

Últimas tres peticiones `/v1/chat/completions`: HTTP 200, 39,99459802 s (19:38:28), 13,193986126 s (19:39:37) y 17,99354785 s (19:41:04), según registro del invitado. No son tiempos completos de navegador ni una muestra estadística de capacidad. Último desglose: entrada 3,06 s; generación 14,90 s, 9,40 tokens/s. No se asigna causa a la primera demora sin evidencia de carga.

## Control de razonamiento: API directa

Comando de comparación sin Moodle:

```bash
curl -sS --max-time 120 \
http://127.0.0.1:11434/v1/chat/completions \
-H 'Content-Type: application/json' \
-d '{"model":"qwen3-lab","messages":[{"role":"user","content":"Hay cuatro clases de treinta minutos. Cuanto dura cada clase? /no_think"}]}' \
-w '\nTiempo total: %{time_total} segundos\n'
```

- `/no_think` solo: 20,140108 s, 256 tokens de salida, `content` vacío, campo `reasoning` extenso, `finish_reason: length`. El límite de generación se agotó sin respuesta final. La instrucción textual no fue suficiente en este ensayo.
- Segunda ejecución: mismo comando, añadiendo `"reasoning_effort":"none"` junto a `model`. Resultado 11,567252 s, 114 tokens de salida, contenido final correcto (30 minutos), `finish_reason: stop`, sin campo reasoning visible. Incluyó explicación y formato matemático innecesarios. No prueba una mejora universal; ni prompt ni historial equivalen exactamente a los de MooChat.
- El perfil conserva num_thread=2, num_ctx=2048, num_predict=256. `--think=false` de la CLI no se hereda en Moodle. El código del proveedor de Moodle 4.5 consultado envía modelo, usuario y mensajes, no `reasoning_effort`.
- No se modificó código de Moodle, del plugin ni la plantilla del modelo. La integración del control explícito queda pendiente; no confundir éxito de API directa con configuración ya aplicada a AERO.

## Continuidad y límites

1. Tras reinicio: verificar estado de Ollama y SELinux; el arranque del servicio es manual y el booleano fue temporal. No asumir recuperación automática de la integración.
2. Resolver cómo enviar el control de razonamiento de forma mantenible y contrastar instrucciones globales de resumen con la función conversacional.
3. Medir tiempos con casos repetidos y contexto controlado antes de cambiar recursos. No se han probado concurrencia, documentos ni permisos entre cursos/usuarios.
4. El filtro de salida de Ollama no cubre PHP/Moodle. El booleano web amplía conectividad: falta validación de toda la cadena y ausencia de destinos externos. No se acredita confidencialidad integral solo por respuestas locales.
5. La ruta de extracción PPTX reportada no se ensayó ni corrigió. Se avanzó con texto sintético, sin archivos; no constituye aceptación para producción.
6. Mantener separados el aval técnico/regulatorio y la definición académica con docentes y responsables de cursos. Ninguno se considera concedido por estos ensayos.

## Fuentes contrastadas el 2026-10-19

- [Construcción de solicitudes en Moodle 4.5](https://raw.githubusercontent.com/moodle/moodle/MOODLE_405_STABLE/ai/provider/openai/classes/process_generate_text.php).
- [Control HTTP y resolución inversa](https://raw.githubusercontent.com/moodle/moodle/MOODLE_405_STABLE/lib/classes/files/curl_security_helper.php).
- [Validación de respuestas fallidas](https://raw.githubusercontent.com/moodle/moodle/MOODLE_405_STABLE/ai/classes/aiactions/responses/response_base.php).
- [Compatibilidad OpenAI de Ollama](https://docs.ollama.com/api/openai-compatibility).
- [Control por instrucciones de Qwen3](https://qwenlm.github.io/blog/qwen3/).

Las ramas y documentación web son referencias móviles; el comportamiento local descrito corresponde a las salidas observadas de Ollama 0.40.6.
