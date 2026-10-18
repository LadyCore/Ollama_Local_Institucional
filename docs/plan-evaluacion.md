# Plan de evaluación técnica

Estado: propuesto. Ningún control de esta lista se considera aplicado por estar documentado.

| Etapa | Acción prevista | Evidencia para cerrar |
|---|---|---|
| Fuentes y requisitos | Revisar documentación oficial, versiones, arquitectura y recursos | URLs, fecha de consulta y requisitos de la versión seleccionada |
| Recuperación | Definir snapshot/respaldo adecuado y reversión de cada cambio | Confirmación y procedimiento sin identificadores reales |
| Instalación | Preparar método, versión, usuario de servicio, rutas sustituibles y ubicación de modelos | Versión instalada, estado y arranque/parada controlados |
| Operación local | Ensayar API y modelo con texto sintético | Petición, respuesta, tiempo, consumo y errores |
| Red | Revisar escucha, exposición, firewall y flujos de salida | Comprobación efectiva de interfaces, puertos y destinos |
| Acceso | Evaluar autenticación, autorización y eventual intermediario si se requiere acceso remoto | Accesos permitidos/denegados ensayados; no asumir seguridad por ser local |
| Recursos | Evaluar límites CPU/RAM, concurrencia, contexto, tiempos y almacenamiento | Medidas con carga acotada y convivencia Moodle/MySQL |
| Datos | Evaluar logs, retención, permisos, eliminación y funciones que contacten servicios externos | Configuración y comprobación con datos sintéticos |
| Modelos | Revisar procedencia, licencia, tamaño y capacidad del modelo elegido | Identificador/versionado y condiciones de uso verificadas |
| Plugins | Revisar compatibilidad declarada, datos enviados, permisos y dependencias | Matriz documentada y ensayo explícitamente autorizado |
| Operación | Definir actualización, parada, diagnóstico, desinstalación y recuperación | Procedimiento con controles y resultados reproducibles |
| Presentación | Consolidar capacidades, restricciones, costos de recursos y pendientes | Propuesta técnica basada en evidencia, pendiente de aprobación institucional |

## Límites de ensayo

No usar datos personales o institucionales reales. No crear cursos como prueba. No habilitar acceso desde red ni integrar plugins automáticamente. Distinguir el servicio que responde de la calidad de sus respuestas, y la compatibilidad declarada del funcionamiento comprobado.

Ante falta de memoria, degradación de Moodle/MySQL, exposición inesperada o envío no previsto de datos, detener la prueba y registrar el incidente antes de ampliar el alcance.

## Fuentes

La revisión inicial oficial se registra en [seguridad y confidencialidad](seguridad-confidencialidad.md), con fecha, enlaces y distinción entre hechos documentados y controles propuestos. La selección de versiones, modelos y plugins continúa pendiente.
