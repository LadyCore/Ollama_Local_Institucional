# AERO: calidad, razonamiento y tiempos de espera

## Alcance del registro

Consolidado el 2026-10-20, fecha de Argentina, a partir de salidas y capturas aportadas en la conversación. No hubo acceso directo a la VM. Registro retrospectivo: las pruebas posteriores a B035 no se sincronizaron durante su ejecución. Se conservan resultados fallidos, cambios revertidos y límites de evidencia. No se publican capturas, identificadores de personas, cursos, hosts ni direcciones internas. Los tiempos aproximados informados por la administradora se distinguen de las mediciones de curl.

Los ensayos iniciales de esta secuencia abarcan el cierre de la sesión anterior y la continuación del día 20; donde no existe hora inequívoca se conserva el orden, sin inventar marcas temporales. No hay aprobación pedagógica ni de producción. La prioridad acordada es calidad antes de velocidad.

## Estado vigente al cierre

| Elemento | Última evidencia disponible |
|---|---|
| Modelo del proveedor Moodle | `qwen3-estudio` |
| Modelo inspeccionado | Arquitectura qwen3, 2.0B parámetros, Q4_K_M; contexto declarado 40960; thinking false/true, predeterminado true |
| Perfil efectivo, verificado tras recreación | num_predict 1536, num_thread 2, num_ctx 2048, temperature 0.6, top_k 20, top_p 0.95, repeat_penalty 1; stop im_start/im_end |
| Archivo de creación | `FROM qwen3-lab` y `PARAMETER num_predict 1536` en `/var/tmp/Modelfile-estudio` |
| Instrucción de actividad | Español breve, texto plano, reconocer falta de información, identidad AERO; sin `/no_think` |
| Instrucción global del proveedor | Texto original en inglés que pide resumen en texto plano; restauración informada con «listo»; sin `/no_think` |
| API Moodle | Compatible OpenAI hacia loopback, puerto 11434, `/v1/chat/completions`; no se editó código PHP ni JavaScript |
| Apache | `ProxyTimeout 240` dentro del VirtualHost de Moodle; configtest Syntax OK; recarga indicada y posterior respuesta observada |
| SELinux | No se desactivó; `httpd_can_network_connect on` temporal, sin `-P`; no equivale a permiso limitado a Ollama |
| Ollama | Activo en comprobaciones; inicio automático sigue sin habilitarse |
| Avatar | Visible en AERO en pruebas posteriores |
| Materiales | Sin PDF ni contenido de sección en estas pruebas; no probado RAG ni generación de diapositivas |

La identificación previa de la descarga como `qwen3:1.7b` es un antecedente, no debe reemplazar la salida posterior que muestra 2.0B en este perfil. No se ha explicado esa discrepancia mediante inventario de manifiestos. El contexto soportado por la arquitectura no es el contexto activo de 2048.

## Preguntas sintéticas

- **C (clases):** Un curso tiene cuatro clases de treinta minutos cada una. Un estudiante calcula 30 dividido por 4, obtiene 7,5 y afirma que esa es la duración de cada clase. ¿Es correcto? ¿Qué representa 30?
- **L (lápices):** Hay seis cajas con ocho lápices cada una. Una estudiante divide 8 entre 6 para hallar el total. ¿Es correcto? ¿Qué representa 8 y cuántos lápices hay?

Variantes de tipeo usan cifras, palabras, barra o signo de división; no son réplicas byte a byte. C: 30 minutos por clase, 120 total; la cuenta 30/4 es aritméticamente válida pero no resuelve la pregunta. L: 8 por caja, 6 cajas, total 48. La evaluación considera toda la explicación, no una frase aislada. Una respuesta que identifica correctamente las cantidades no debe invalidarse por interpretar literalmente «el cálculo es incorrecto» fuera de su contexto; una contradicción explícita sobre qué representa 30 sí es un fallo.

## Secuencia de modelos y ensayos iniciales

1. **Experimento `aero-lab`:** exportación de plantilla a `/var/tmp/Modelfile-aero`; condición final sustituida por `{{ if true -}}` para insertar un bloque think vacío. Creación completada; no se desplegó ese modelo en Moodle. Una consulta agotó la espera tras 461,568744 s (0 bytes); en el servidor hubo un HTTP 500 de 10m58s. Ahorro de energía informado como interferencia; no diagnóstico exclusivo del kernel. Repetición: 12,481595 s, 84 tokens de salida, stop, respuesta incorrecta de 7,5 minutos. No seleccionar ese experimento como solución de calidad.
2. **`qwen3-estudio` inicial:** FROM qwen3-lab, num_predict 512. Creación y parámetros 512 verificados. Saludo y ejercicio simple C correctos, aproximadamente 13 s cada uno. Follow-ups erróneos, contradicciones sobre promedio y total; un carácter de otro idioma en una respuesta; error genérico de conexión en otro intento.
3. **Calidad inicial en MooChat:** incluso con conversación nueva, una respuesta concluyó 30 por clase pero explicó erróneamente que 30 era el total y 7,5 el promedio. Preguntas descompuestas permitieron obtener 4, 30 y 120; no estabilizaron explicaciones posteriores. Una respuesta quedó incompleta, sin causa determinada.
4. **Muestra de servidor de esa etapa:** HTTP 200, 28,902406472 s; 539 tokens de entrada, 404 cacheados; evaluación de entrada 5,70128 s para 135 tokens; salida 247 tokens en 22,30528 s, 11,03 tokens/s. No agotó 512. No asociar sin más a todas las respuestas de esa sesión.

## Comparación directa de razonamiento, día 20

Se usó curl a la API de chat, con `stream:false`; los parámetros de solicitud no alteran el perfil persistente. Antes de estos ensayos se corrigieron errores de tipeo (falta de número en max-time, JSON sin valor de max_tokens, comando rub en vez de run); no fueron fallos del modelo. Servicio detenido recuperado con `systemctl start ollama`.

| Prueba | Configuración relevante | Resultado y evidencia |
|---|---|---|
| D01 C | Perfil 512, `/no_think`, sin reasoning_effort | 62,734189 s; 512 tokens de salida, length; content vacío, reasoning presente |
| D02 C | Perfil 512, `/no_think`, reasoning_effort none | 38,276130 s; 476 tokens, stop; respuesta completa incorrecta: 30 como total |
| D03 C | max_tokens 1536, medium; `/no_think` quedó presente | 102,023081 s; 1129 tokens, stop; datos principales correctos con explicación contradictoria |
| D04 C | max_tokens 1536, medium; sin `/no_think` | 83,509300 s; 769 tokens, stop; respuesta aceptada como correcta tras revisar su sentido completo; aviso clocksource en la salida |
| D05 L | max_tokens 1536, medium; sin `/no_think` | 74,909450 s; 885 tokens, stop; respuesta correcta y explicada |

Los tokens de salida de estas respuestas incluyen reasoning y content. Los resultados de D04/D05 no constituyen evaluación general ni demuestran un nivel graduado de razonamiento: el modelo inspeccionado declara thinking booleano. Aquí medium es el valor enviado, no una capacidad certificada de tres niveles.

## Paso a Moodle e incidentes

### Límite de salida: aplicación inicialmente no acreditada

Se editó `/var/tmp/Modelfile-estudio` de 512 a 1536 y `ollama create qwen3-estudio -f /var/tmp/Modelfile-estudio` mostró success. Se afirmó prematuramente que el cambio era efectivo. Una comprobación posterior con `ollama show qwen3-estudio --parameters` todavía mostró **512**, mientras `cat` mostraba **1536** en el archivo. Causa no determinada. Se repitió exactamente la creación y luego se verificó **1536** en los parámetros. No atribuir la discrepancia a un error de tipeo sin evidencia.

Se quitaron `/no_think` de la actividad y del proveedor. El proveedor siguió apuntando a qwen3-estudio. Su instrucción global conservaba «Return the summary in plain text only».

### Conexión y permisos

- Error cURL 7 en Moodle; servicio active pero `getsebool httpd_can_network_connect` mostró off. Se restableció temporalmente con `setsebool httpd_can_network_connect on`; comprobación posterior on.
- Nueva petición falló en interfaz tras aproximadamente 68 s. Ollama procesó la consulta y registró HTTP 200: entrada 221 tokens en 20,65705 s, salida 310 tokens en 53,03894 s (5,83 tokens/s), procesamiento 73,69599 s; petición completa 2m5s. Diferencia no explicada definitivamente.
- Congelación temporal de la VM, recuperación espontánea y aviso `clocksource: Long readout interval, skipping watchdog check`, también visto en otras pruebas. No es una denegación SELinux; no acredita por sí solo causa de suspensión o falta de CPU. Las mediciones de pared no son un benchmark controlado.

### Timeout Apache/PHP: evidencia y corrección

Comandos de diagnóstico (rutas de instalación sustituibles):

```bash
journalctl -u ollama -n 25 --no-pager
tail -n 30 /var/log/httpd/error_log
grep -Ri ErrorLog /etc/httpd/conf.d
tail -n 30 /var/log/httpd/moodle_error.log
grep -Ri timeout /etc/httpd/conf /etc/httpd/conf.d
cat /etc/httpd/conf.d/moodle.conf
```

Registro global sin el error buscado; se identificó registro del VirtualHost. Este mostró varios `proxy_fcgi:error`, `(70007) The timeout specified has expired`, `AH01075: Error dispatching request ... (polling)`, asociados a MooChat. La última muestra incluye 21:06 y 21:14; no afirmar coincidencia exacta con cada intento de interfaz. La búsqueda de timeout no encontró directivas explícitas en las carpetas examinadas.

Se agregó `ProxyTimeout 240` inmediatamente después de `<VirtualHost *:80>`, sin modificar ServerName, DocumentRoot ni Directory. `apachectl configtest` dio Syntax OK; aviso global de ServerName no bloqueante. Se indicó `systemctl reload httpd` y se observó luego una respuesta de AERO. No se modificaron pools PHP, SELinux global ni servicios de base de datos.

Recuperación prevista: quitar solo ProxyTimeout 240, validar y recargar. No ejecutada. El ajuste permite esperar más; no acelera inferencia. Que una prueba termine en 48 s no demuestra por sí solo que ya soporte una respuesta superior al límite anterior.

## Resultados en AERO después del ajuste web

| Prueba | Contexto y cambio | Resultado |
|---|---|---|
| M01 L | Tras recarga; conversación limpia | Correcta, 48 s aproximados; avatar visible |
| M02 C | Misma conversación que L | Incorrecta: 30 como total; contradicción con 120 |
| M03 C | Clear Chat | 34 s aproximados; primera oración incorrecta, resto contradictorio |
| M04 C | Clear Chat; instrucción global cambiada a español neutro | 25 s aproximados; validó 7,5 y 30 como total; fallida |
| M05 C | Tras restauración de instrucción global y recreación con 1536 efectivamente verificado | Aproximadamente 60 s; incorrecta, validó 7,5 minutos por clase |

M01–M04 precedieron la detección del perfil aún en 512; el valor efectivo no se comprobó por petición. M05 tuvo el perfil inspeccionado en 1536. No se registraron JSON crudos ni finish_reason de estas respuestas web; no inferir truncamiento ni cantidad de razonamiento desde su duración.

Instrucción global experimental de M04: «Respondé a la pregunta del usuario en español y en texto plano. Conservá el significado de los datos del enunciado. Si falta información, indicá cuál». Revertida por decisión de la administradora, acción confirmada con «listo». Estado restaurado:

```text
You will receive a text input from the user. Your task is to generate text based on their request. Follow these important instructions:
1. Return the summary in plain text only.
2. Do not include any markdown formatting, greetings, or platitudes.
```

No se volvió a agregar `/no_think`. La instrucción global es una diferencia respecto de las consultas directas, no una causa demostrada del error.

## Inspección del código instalado, sin modificaciones

- `ai/provider/openai/classes/process_generate_text.php`: petición construida con model, user y messages; mensaje system global y mensaje user con prompttext. No agrega reasoning_effort ni max_tokens en el método observado. Lee `choices[0].message.content`; no muestra el campo reasoning al alumno.
- `mod/moochat/classes/external/send_message.php`, líneas 120–190: toma systemprompt almacenado sin limpieza HTML visible en ese tramo; incorpora materiales si existen; concatena instrucciones, historial con etiquetas textuales User/Assistant y pregunta actual, terminando en Assistant:. Todo se transmite como prompttext. No se inspeccionó el valor crudo almacenado en base de datos, por lo que no se confirma presencia de HTML.
- La ausencia de reasoning_effort no equivale a thinking desactivado. No se introdujo un parche en Moodle ni una captura de tráfico/conversaciones.

Lecturas realizadas: `grep -A 65 'function create_request_object' process_generate_text.php`, `grep -n -A 25 'fullprompt =' send_message.php`, `sed -n '120,165p' send_message.php` desde sus respectivas carpetas.

## Últimos ensayos directos: no confundir con petición completa de Moodle

| Prueba | Mensaje y parámetros | Resultado |
|---|---|---|
| D06 C | Pregunta sola; max_tokens 1536; medium quedó presente al editar | 135,431413 s; 1317 tokens, stop; correcta en lo esencial. No fue ensayo sin reasoning_effort |
| D07 C | Pregunta sola; max_tokens 1536; reasoning_effort eliminado | 107,001297 s; 1218 tokens, stop; reasoning presente; identifica 30 por clase y 120 total, con explicación confusa sobre interpretación del estudiante |
| D08 C | Instrucciones de AERO y etiquetas User/Assistant dentro de un solo mensaje user; max_tokens 1536, sin reasoning_effort | 78,812803 s; entrada 109, salida 455, total 564, stop; reasoning presente; respuesta final incorrecta: valida 7,5 y 30 como total |

Se recuperaron comandos con `fc -ln 984 984` (lectura) y `fc -e vi 984` / `fc -e vi curl` (editar y ejecutar al salir). No son comandos de reproducción portables: dependen del historial de esa sesión. No se deben volver a ejecutar por número desde otro historial.

Solicitud mínima de D08, con datos sintéticos y sin instrucción system global:

```json
{
  "model": "qwen3-estudio",
  "messages": [{
    "role": "user",
    "content": "Responde en español, de forma breve y usando texto plano. Si no tenés información suficiente, indicalo sin inventar datos. Te llamas AERO\n\nUser: Un curso tiene cuatro clases de treinta minutos cada una. Un estudiante calcula 30/4 = 7.5 y dice que es la duración de cada clase. ¿Es correcto? Explicá qué representa el número 30 en el enunciado. \nAssistant:"
  }],
  "max_tokens": 1536,
  "stream": false
}
```

Se envió con curl, Content-Type application/json, max-time 240, registro de time_total. El ejemplo transcribe el texto visible; no conserva bytes de terminal ni una captura de red. D08 aproxima el formato de MooChat, pero no reproduce toda su solicitud: falta el system global, no se verificó HTML almacenado y se envía max_tokens explícito. Se cambiaron conjuntamente instrucciones y etiquetas; no permite atribuir causalidad a una sola de ellas. Una ejecución por variante, sin semilla fija ni muestreo repetido, no demuestra una relación causal ni deterioro acumulativo del modelo.

## Decisiones y continuidad

1. Frenar modificaciones manuales sucesivas y no instalar otro plugin como supuesto arreglo del modelo.
2. Preparar comparación reproducible con variantes separadas, repeticiones, parámetros registrados, salida final, finish_reason, conteos, tiempo y criterio de corrección. La automatización de ese banco todavía no se implementó.
3. No subir más tokens ni modificar temperature/plantilla sin hipótesis y registro; el último fallo terminó en 455 de 1536, con razonamiento presente.
4. Verificar solicitud completa de Moodle antes de afirmar equivalencia; después evaluar modelo/configuración alternativos si no supera calidad. No se seleccionó sustituto.
5. Conservar ajustes de conexión actuales del laboratorio y documentar persistencia pendiente: arranque manual de Ollama y booleano web temporal tras reinicio.
6. No considerar las respuestas correctas aisladas como aprobación para alumnos. Latencia, pausas de VM, estabilidad y concurrencia siguen pendientes.

## Funcionalidades y referencias examinadas

Las pantallas de MooChat muestran carga de hasta cinco materiales, restricción a contenido cargado, contenido de sección, objetivos, avatar/tamaño y modo de visualización. La presencia del control no verifica extracción PDF, fundamentación, citas ni aislamiento por curso. Preguntas guía, trabajo con libros/PDF y generación de diapositivas son capacidades a investigar, no ensayadas.

Tutor AI fue descargado según informe; no se confirmó instalación. Capturas de referencia muestran identificador `local_dttutor`, avatar flotante/posición, bienvenida, nombre, prompt y control de tema. Compatibilidad con Ollama, personalización por curso y prestaciones documentales pendientes. El nombre EdWork de otra referencia no fue identificado; no se afirma equivalencia con Tutor AI.

Se revisó código público de [capacityAr](https://github.com/etrigan16/capacityAr): clientes Groq/Gemini y mock, no integración Ollama/MooChat verificada. Ideas: reglas deterministas, evaluación separada de explicación, validación estructural. Límites: comparación textual, respuestas esperadas generadas por IA, expected_answer recibido pero no incluido en prompt de feedback, JSON válido no garantiza verdad. No se instaló ni ejecutó ese código. Otras referencias exploratorias: [CourseChat](https://arxiv.org/html/2610.02510v1), [prototipo Moodle/Ollama](https://github.com/IliasAlmerekov/moodle), [fork de chat Ollama](https://github.com/ragcon-ai/moodle-block_ollama_chat); no equivalen a configuración ensayada ni sustitutos aprobados.

Fuentes técnicas consultadas el 2026-10-20:

- [Apache ProxyTimeout](https://httpd.apache.org/docs/current/mod/mod_proxy.html#proxytimeout).
- [Código público MooChat send_message](https://github.com/bapool/moodle-mod_moochat/blob/main/classes/external/send_message.php) y [chat.js](https://github.com/bapool/moodle-mod_moochat/blob/main/amd/src/chat.js): mensaje genérico de fallo no identifica causa; fragmentos instalados contrastados en consola.
- [Proveedor Moodle 4.5](https://github.com/moodle/moodle/blob/MOODLE_405_STABLE/ai/provider/openai/classes/abstract_processor.php) y [cliente HTTP](https://github.com/moodle/moodle/blob/MOODLE_405_STABLE/lib/classes/http_client.php): lectura, sin parche.
- [Código del aviso clocksource](https://android.googlesource.com/kernel/common/+/7db06e329af30dcb170a6782c1714217ad65033d/kernel/time/clocksource.c): referencia explicativa, no identificación del kernel instalado ni causa de pausas.

## Recuperación y límites de esta consolidación

No se ejecutó ninguna reversión de la VM desde el asistente. Modelo: volver a 512 requiere editar el Modelfile, recrear e inspeccionar parámetros; no basta success. Apache: quitar línea agregada y validar antes de recargar. Booleano: `setsebool httpd_can_network_connect off` restablece bloqueo web, no hacerlo durante una prueba sin prever pérdida de conexión. Prompts: reversión del experimento M04 ya informada; no volver a introducir no_think por error.

Esta consolidación no convierte en verificados los aspectos pendientes ni reconstruye duraciones no observadas. La publicación documental debe verificarse contra el commit remoto y conservar el repositorio privado; no incluir trazas completas de conversaciones reales.
