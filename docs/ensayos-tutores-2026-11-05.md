# Ensayos en curso de tutores, 5 de noviembre de 2026

Registro incorporado el 6 de noviembre a partir del informe aportado por la administradora. Estado de las pruebas: ejecutado informado, con contrastes manuales consignados en el informe. Se conservan tiempos aproximados y preguntas para permitir futuras comparaciones.

## Entorno y configuración

Laboratorio VirtualBox, CentOS Stream 9, Moodle 4.5.8, MooChat y Ollama con Qwen local. Curso de formación de tutores restaurado desde una copia MBZ de producción. El asistente es otra instancia de MooChat sobre el mismo modelo utilizado en los ensayos anteriores.

La actividad se ubicó inicialmente al final del módulo 1. Después se agregó otra instancia tras el primer foro obligatorio. Contenido de sección y contenido oculto activados, sin archivos adicionales cargados. Creatividad 0,5 Balanced, máximo 20 mensajes, página separada, interfaz mediana (400 px de mensajes y 500 px total), avatar de 64 × 64.

El prompt inicial conservaba por error la especialidad del curso anterior. Se corrigió la referencia al curso, sin mejora inmediata observada. El texto exacto corregido queda pendiente de registro. Los cuatro objetivos pedían basarse en contenido accesible, reconocer información insuficiente y responder con claridad y rapidez.

## Consultas y contraste documental

| Prueba | Consulta | Tiempo informado | Resultado y contraste |
|---|---|---|---|
| A | Partes del módulo 1 | ~2 min | Respuesta extensa que reorganizó y numeró material, mezclando capítulos y actividades. Se conserva la corrección de tiempo efectuada por la administradora. |
| B | Objetivos del módulo 1 | Algo más de 3 min | Respuesta extensa y parcialmente divergente. La página de objetivos del libro expresa identificar las habilidades de un tutor virtual para desempeñarse en una plataforma educativa virtual. |
| C | De qué depende el éxito de una propuesta formativa en educación superior | Sin medición válida | Respuesta extensa, con dimensiones adicionales. La administradora se durmió durante la espera y volvió a observar la pantalla algo más de diez minutos después. Ese intervalo no mide la generación. |
| D | Cuatro dimensiones del rol del tutor según capítulo 5 | ~2 min | Respondió orientación y guía, asistencia y acompañamiento, gestión y coordinación, evaluación y retroalimentación. El capítulo enumera PEDAGÓGICA, SOCIAL, ADMINISTRATIVA y TÉCNICA. |
| E | Misma pregunta, con otra instancia en el módulo 1 | ~2 min | Respondió identificación de objetivos, selección de contenidos, diseño de actividades y selección de recursos tecnológicos. Esas categorías aparecen en capítulo 12, Diseño de un Plan de Clases. La atribución al capítulo 5 fue incorrecta aunque mencionó bibliografía existente. |
| F | Función Orientadora o de Guía Metodológica | ~1 min 30 s | Respuesta parcialmente pertinente sobre autonomía y orientación, mezclada con selección de contenidos del capítulo 12. Al pedir fuente señaló capítulo 5. El encabezado solicitado figura en capítulo 7, Funciones del tutor. |
| G | Qué es una competencia (consulta con error tipográfico) | ~2 min 40 s | Tras cambiar creatividad a 0,3 Focused y desactivar contenido oculto, respondió extensamente e incluyó caracteres chinos anómalos. El capítulo 6 define competencia como capacidad de movilizar recursos cognitivos para realizar tareas o resolver problemas en distintos contextos. |
| H | De dónde proviene esta información | Sin respuesta | MooChat mostró «Failed to connect to AI service». |

El recurso Libro contiene capítulos y subcapítulos, texto e imágenes. El curso también incluye foros, cuestionarios, tareas y actividades. El contenido completo enviado en estas solicitudes queda pendiente de inspección. La selección y representación de la estructura del libro en el prompt también quedan pendientes. La revisión realizada abarcó fragmentos concretos.

El ensayo G cambió dos opciones simultáneamente. El resultado observado fue largo y mezcló contenido pese al ajuste Focused. El efecto independiente de cada opción queda sin determinar.

## Incidente de VirtualBox y servicio

El informe recoge el kernel 5.14.0-687.el9.x86_64. Se ejecutó:

```sh
sudo journalctl -k -b --no-pager | grep -Ei 'soft lockup|watchdog|clocksource'
systemctl is-active ollama
```

Eventos del 5 de noviembre, horas tal como aparecen en los registros aportados:

- 18:22:16, 18:47:40 y 21:06:53, avisos de clocksource, «Long readout interval, skipping watchdog check».
- 22:45:09, «watchdog: BUG: soft lockup - CPU#1 stuck for 468s! [swapper/1:0]».
- 22:45:11, otro aviso de clocksource.

La consola recuperó el prompt y Ollama informó `active`. Esa consulta acredita el estado del servicio en ese instante. La recuperación de la API y de la inferencia quedó pendiente de verificar.

La relación causal entre el soft lockup y el fallo de conexión sigue abierta. La administradora propone investigar si la carga de inferencia y el contexto amplio contribuyen a la degradación, dado el uso previo de la VM para restauraciones y administración sin esos síntomas. Faltan mediciones para atribuir la causa.

## Comparación y continuidad

En este curso, las consultas medidas estuvieron entre aproximadamente 1,5 minutos y algo más de 3 minutos, con errores de correspondencia entre capítulos. En el curso anterior, el ensayo con PDF exclusivo rondó un minuto y produjo dos referencias cotejadas con el índice tras repreguntar. Cambiaron curso, estructura y volumen de contexto, archivo y preguntas. [Registro del ensayo previo](ensayos-2026-11-03-a-05.md).

Próxima etapa propuesta, pendiente de ejecución: pruebas con material explícitamente cargado, preguntas constantes y referencias conocidas, medición de tiempos y evaluación por las tutoras o administradoras autoras del curso. Diagnóstico separado de la temporización de VirtualBox y del comportamiento de Ollama/MooChat. La evaluación pedagógica integral sigue pendiente.
