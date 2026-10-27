# Ollama local institucional

Laboratorio para conocer el funcionamiento de Ollama local, determinar configuraciones y restricciones, y evaluar plugins de Moodle compatibles. La evidencia obtenida servirá para elaborar una propuesta técnica ante la instancia jerárquica superior; la selección de usos corresponde a las áreas destinatarias dentro de las capacidades que se validen.

Estado al 26 de octubre de 2026: AERO se evalúa para responder con materiales del curso. En pruebas offline, MooChat leyó los TXT de la guía y La farolera; Word no aportó respuestas y se informó fallo con PDF. Hubo además bloqueos de la VM y errores de conexión, sin causa determinada. Se pausan pruebas repetitivas de MooChat y se revisan reemplazos: primero viabilidad completa dentro de los aproximadamente 9 GB del laboratorio; después, en el destino de 15 GiB. Ningún reemplazo está instalado ni validado. Se conservan los parámetros históricos y controles de red documentados; no hay aprobación para producción ni demostración integral de ausencia de salida de datos desde Moodle.

## Documentación

- [Pruebas offline y candidatos, 25–26 de octubre](docs/ensayos-offline-2026-10-25.md): resultados de documentos, incidentes de VM, recursos y selección pendiente.

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

Las pruebas iniciales utilizan datos sintéticos; posteriormente se aportaron ensayos con otros documentos, cuyo contenido no se incorpora al repositorio. La evidencia publicada se limita a resultados técnicos anonimizados y procedimientos con parámetros sustituibles, sin credenciales, identificadores institucionales ni datos de usuarios.

## Resultado esperado

Un procedimiento reproducible con requisitos, parámetros, instalación, controles, restricciones, recuperación y límites de pruebas; una matriz de compatibilidad sustentada; y evidencia suficiente para preparar una presentación técnica sin confundir un ensayo con una aprobación para producción.
