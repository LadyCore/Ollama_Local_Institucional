# Ollama local institucional

Laboratorio para conocer el funcionamiento de Ollama local, determinar configuraciones y restricciones, y evaluar plugins de Moodle compatibles. La evidencia obtenida servirá para elaborar una propuesta técnica ante la instancia jerárquica superior; la selección de usos corresponde a las áreas destinatarias dentro de las capacidades que se validen.

Estado inicial: proyecto documentado el 18 de octubre de 2026. Instalación de Ollama pendiente. No hay integración Moodle ni habilitación institucional aprobada.

## Documentación

- [Bitácora viva](docs/bitacora.md): acciones, evidencias, decisiones y recuperación.
- [Entorno y estado](docs/estado.md): inventario confirmado, límites y próximos pasos.
- [Protocolo de evaluación](docs/plan-evaluacion.md): secuencia de trabajo, restricciones, pruebas y criterios de cierre.
- [Compatibilidad Moodle](docs/compatibilidad-moodle.md): matriz de candidatos y resultados.
- [Seguridad y confidencialidad](docs/seguridad-confidencialidad.md): fundamentos, requisitos de validación y evidencia requerida.

## Método

El trabajo se realiza por etapas verificables. La ejecución en la VM corresponde a la administración del servidor. Cada etapa registra las acciones ejecutadas, la evidencia disponible, los resultados y los pendientes; los intentos fallidos se conservan para trazabilidad.

La bitácora, el estado y la matriz se actualizan con cada avance confirmado durante las sesiones de trabajo. La sincronización en GitHub incluye verificación de la revisión publicada. El registro no dispone de monitoreo automático de la VM. Las reglas de mantenimiento documental se encuentran en [AGENTS.md](AGENTS.md).

La documentación conserva la cronología y expresa las decisiones y procedimientos del proyecto en forma impersonal. Se distinguen los acuerdos de laboratorio, las acciones verificadas y las autorizaciones institucionales pendientes.

## Alcance y privacidad

Evaluación en un clon de laboratorio con MySQL. Producción y el proyecto de actualización a Moodle 5.3 quedan fuera del alcance. No modificar Moodle, PHP, MySQL, pools ni configuraciones existentes salvo necesidad documentada y autorización específica. No crear cursos de prueba.

El repositorio permanece privado y excluye credenciales, identificadores institucionales, nombres reales de máquinas, direcciones de red, rutas personales, datos de usuarios y capturas de plataformas reales. Los procedimientos utilizan datos sintéticos y parámetros sustituibles. La presentación a terceros requiere una decisión específica.

## Resultado esperado

Un procedimiento reproducible con requisitos, parámetros, instalación, controles, restricciones, recuperación y límites de pruebas; una matriz de compatibilidad sustentada; y evidencia suficiente para preparar una presentación técnica sin confundir un ensayo con una aprobación para producción.
