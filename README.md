# Ollama local institucional

Laboratorio para conocer el funcionamiento de Ollama local, determinar configuraciones y restricciones, y evaluar plugins de Moodle compatibles. La evidencia obtenida servirá para elaborar una propuesta técnica ante DIRINFO; la selección de usos corresponde a las áreas destinatarias dentro de las capacidades que se validen.

Estado inicial: proyecto documentado el 18 de octubre de 2026. Instalación de Ollama pendiente. No hay integración Moodle ni habilitación institucional aprobada.

## Documentación

- [Bitácora viva](docs/bitacora.md): acciones, evidencias, decisiones y recuperación.
- [Entorno y estado](docs/estado.md): inventario confirmado, límites y próximos pasos.
- [Plan de evaluación](docs/plan-evaluacion.md): instalación, restricciones, pruebas y criterios de cierre.
- [Compatibilidad Moodle](docs/compatibilidad-moodle.md): matriz de candidatos y resultados.

## Método

Avanzar por pasos breves y verificables. La administradora ejecuta las acciones dentro de la VM; las herramientas del asistente en Windows no equivalen a acceso a la consola Linux. Registrar resultados observados o confirmados, distinguirlos de propuestas y conservar los intentos fallidos.

La bitácora se actualiza durante el trabajo asistido, después de cada avance confirmado, junto con el estado y la matriz correspondiente. La actualización en GitHub debe comprobarse antes de declararse sincronizada. No hay un recolector ni una tarea en segundo plano: no se observa la VM ni se inventan novedades entre sesiones. Las reglas persistentes se encuentran en [AGENTS.md](AGENTS.md).

## Alcance y privacidad

Evaluación en un clon de laboratorio con MySQL. Producción y el proyecto de actualización a Moodle 5.3 quedan fuera del alcance. No modificar Moodle, PHP, MySQL, pools ni configuraciones existentes salvo necesidad documentada y autorización específica. No crear cursos de prueba.

Mantener el repositorio privado. Aun en privado, excluir credenciales, identificadores institucionales, nombres reales de máquinas, direcciones de red, rutas personales, datos de usuarios y capturas de plataformas reales. Emplear datos sintéticos y parámetros sustituibles en procedimientos. No publicar ni enviar la propuesta a terceros automáticamente.

## Resultado esperado

Un procedimiento reproducible con requisitos, parámetros, instalación, controles, restricciones, recuperación y límites de pruebas; una matriz de compatibilidad sustentada; y evidencia suficiente para preparar una presentación técnica sin confundir un ensayo con una aprobación para producción.
