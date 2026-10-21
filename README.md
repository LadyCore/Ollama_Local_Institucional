# Ollama local institucional

Laboratorio para conocer el funcionamiento de Ollama local, determinar configuraciones y restricciones, y evaluar plugins de Moodle compatibles. La evidencia obtenida servirá para elaborar una propuesta técnica ante la instancia jerárquica superior; la selección de usos corresponde a las áreas destinatarias dentro de las capacidades que se validen.

Estado al 20 de octubre de 2026: integración de MooChat v1.8.2 con Ollama local operativa en laboratorio, pero calidad de AERO no validada: errores conceptuales repetidos incluso con conversación nueva y perfil de salida de 1536 tokens verificado. Se diagnosticó timeout Apache/PHP y se aplicó ProxyTimeout 240 al sitio de laboratorio. Filtro IP persistente y permiso SELinux web temporal conservados. No hay aprobación para producción ni demostración integral de ausencia de salida de datos desde Moodle. Las respuestas correctas aisladas no constituyen validación pedagógica.

## Documentación

- [Ensayos AERO del 20 de octubre](docs/ensayos-aero-2026-10-20.md): matriz de resultados, cambios efectivos, discrepancias, reversiones y siguiente comparación pendiente.

- [Integración AERO: sesión del 19 de octubre](docs/integracion-aero.md): configuración, diagnóstico, resultados y continuidad.

- [Bitácora viva](docs/bitacora.md): acciones, evidencias, decisiones y recuperación.
- [Entorno y estado](docs/estado.md): inventario confirmado, límites y próximos pasos.
- [Protocolo de evaluación](docs/plan-evaluacion.md): secuencia de trabajo, restricciones, pruebas y criterios de cierre.
- [Preparación de Ollama](docs/preparacion-ollama.md): requisitos y comprobación previa de instalación.
- [Pruebas locales](docs/pruebas-locales.md): incidente inicial, métricas, funcionamiento sin red y perfil reproducible.
- [Control de red](docs/control-red.md): filtro persistente, ensayo comparativo y límites de la evidencia.
- [Compatibilidad Moodle](docs/compatibilidad-moodle.md): matriz de candidatos y resultados.
- [Seguridad y confidencialidad](docs/seguridad-confidencialidad.md): fundamentos, requisitos de validación y evidencia requerida.
- [Antecedentes en GitHub](docs/antecedentes-github.md): referencias de arquitectura e incidencias contrastadas con código.

## Método

La evaluación comprende instalación de Ollama, validación de procesamiento local y pruebas acotadas de integración con Moodle. Cada etapa registra configuración, evidencia, resultados y pendientes para permitir su reproducción.

## Datos de ensayo y privacidad

Las pruebas utilizan datos sintéticos. La evidencia publicada se limita a resultados técnicos anonimizados y procedimientos con parámetros sustituibles, sin credenciales, identificadores institucionales ni datos de usuarios.

## Resultado esperado

Un procedimiento reproducible con requisitos, parámetros, instalación, controles, restricciones, recuperación y límites de pruebas; una matriz de compatibilidad sustentada; y evidencia suficiente para preparar una presentación técnica sin confundir un ensayo con una aprobación para producción.
