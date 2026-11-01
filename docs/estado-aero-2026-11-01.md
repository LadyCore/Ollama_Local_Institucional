# AERO: recursos, latencia y control de razonamiento

Fecha de consolidación: 2026-11-01, Argentina. Fuente: informe técnico DOCX aportado por la administradora. Se registran sus mediciones e inspecciones como ejecutadas informadas, sin atribuir una nueva verificación directa en la VM. No se publica el documento original, sus imágenes ni identificadores del entorno. La fecha exacta de cada prueba no se infiere de la fecha del informe.

## Configuración informada vigente

- CentOS Stream 9 en VirtualBox; integración MooChat → proveedor OpenAI de Moodle → Ollama local, modelo qwen3-estudio, API chat completions.
- CPUQuota=400 %, frente al 200 % histórico: techo equivalente a cuatro CPU, no medición de utilización ni confirmación de cambio en num_thread.
- MemoryMax=4G. Se ensayó temporalmente 5G y se revirtió a 4G al no observar mejora apreciable.
- Contexto de 2048 tokens; Python 3.9.25 informado.
- No hay nuevo inventario completo de parámetros del modelo; no se supone modificación de num_predict, temperatura u otros valores históricos.
- No se modificó el núcleo de Moodle. Los textos experimentales --think=false se retiraron de los prompts de MooChat y del proveedor.

## Mediciones transcritas

| Prueba | Tiempo | Alcance |
|---|---|---|
| MooChat, otra pregunta | 43,56 s | Registro Ollama, no tiempo integral de interfaz |
| Consulta UML, 4 CPU / 4 GB | 59,30 s | Aproximadamente 1022 tokens de entrada |
| Consulta UML, 4 CPU / 5 GB | 58,94 s | Sin mejora apreciable en la muestra |
| MooChat posterior | 93,06 s | Aproximadamente 1937 tokens de entrada |
| --think=false como instrucción textual | 103,40 s | No desactivó razonamiento |
| MooChat posterior | 110,02 s | 2021 tokens de entrada; truncamiento informado |
| CLI normal | 22,575 s | Consulta breve sin documentos |
| CLI con /no_think textual | 20,871 s | Razonamiento todavía presente |
| CLI con argumento --think=false | 3,448 s | Consulta breve, sin razonamiento visible |

Las preguntas y longitudes difieren. No son comparaciones controladas equivalentes entre CLI y Moodle, ni medidas de extremo a extremo de interfaz. Tampoco el registro histórico de 13,19 s HTTP acredita ese tiempo en UI. La diferencia entre 4G y 5G no demuestra que la RAM nunca influya: solo no mostró beneficio apreciable en esta prueba.

Última medición detallada: 2021 tokens de entrada, 73,61 s de evaluación del prompt; 295 tokens de salida, 36,41 s de generación; total 110,02 s. La entrada representa aproximadamente el 67 % del tiempo. Se informa contexto 2048 y truncated=1; el truncamiento ya no es solo una posibilidad pendiente, aunque su impacto específico sobre calidad requiere comparación controlada.

## Razonamiento y solicitud HTTP

Se informó contenido delimitado por etiquetas think visible en MooChat. Debe verificarse que ese contenido no se exponga a estudiantes. El éxito de una consulta breve sin razonamiento visible no valida toda la integración.

El argumento --think=false de ollama run funcionó en la prueba CLI. Escribir ese argumento como texto en los prompts no produjo el mismo efecto; ambos cambios fueron retirados. La solicitud HTTP directa con reasoning_effort=none obtuvo respuesta válida, finish_reason=stop, 27 prompt_tokens, 33 completion_tokens y 60 total_tokens, sin razonamiento interno visible. No se midió todavía su mejora con documentos completos. No se reconstruye un comando curl completo no incluido en el informe.

## Inspección informada y comprobación previa

MooChat extrae TXT directamente y PDF mediante pdftotext o parser alternativo. Concatena el contenido y el historial; no se observa recuperación selectiva por pregunta en la implementación inspeccionada. La solicitud se entrega a core_ai como fullprompt.

provider.php contiene opciones de modelo, endpoint e instrucción del sistema. En process_generate_text.php se observaron model, user y messages antes de json_encode; no reasoning_effort en el fragmento inspeccionado. La búsqueda de additional, extra y options en las clases revisadas no produjo coincidencias. Esto no constituye auditoría completa de todas las extensiones posibles.

El pendiente de buscar return $content fue resuelto en captura aportada el 27 de octubre: lib.php mostró coincidencias en líneas 344 y 545. Se corrigió un error de escritura de la carpeta del plugin antes de ejecutar:

```bash
grep -n 'return $content' "$MOODLE_ROOT/mod/moochat/lib.php"
```

MOODLE_ROOT representa la ruta local de instalación. No se alteró código con esta inspección.

## Alternativa registrada como pendiente

El informe registra acuerdo para evaluar un intermediario HTTP local con Python 3.9.25 y biblioteca estándar que agregue reasoning_effort=none antes de reenviar a Ollama. No consta implementación, servicio instalado ni cambio de endpoint Moodle.

Criterios propuestos: escuchar solo en loopback; preservar solicitud, respuesta JSON, errores y tiempos de espera; probar primero mediante curl manteniendo el endpoint Moodle actual; comprobar ausencia de think y medir latencia; cambiar el endpoint únicamente tras validación y con reversión documentada. Estos criterios no se presentan como acciones ejecutadas ni como autorización para modificar producción.

## Continuidad

Prioridad documentada por el informe: evaluar el intermediario y medir UI con igual pregunta y documentos, verificar control de razonamiento y efecto del truncamiento. La revisión de reemplazos queda como línea pendiente; no hay sustituto seleccionado ni instalado. Se mantiene el límite de aproximadamente 9 GB del laboratorio y la posterior evaluación en el destino de 15 GiB. El intermediario propuesto no resuelve por sí solo extracción Word, tamaño del contexto, permisos entre cursos ni estabilidad de la VM.

Esta consolidación es exclusivamente documental. Recuperación de los ensayos informada: MemoryMax volvió a 4G y se retiraron las instrucciones textuales --think=false. No se aplicaron cambios adicionales durante la actualización del repositorio.
