# Protocolo de evaluación técnica

Estado: secuencia de laboratorio definida; ejecución pendiente. La inclusión de un control en el protocolo no acredita su implementación ni su resultado.

## Secuencia de trabajo

1. Preparación de recuperación del entorno.
2. Instalación y prueba independiente de Ollama local con un modelo adecuado a los recursos disponibles.
3. Verificación de operación sin conexiones externas, persistencia y consumo.
4. Revisión final del paquete e integración de MooChat con Moodle 4.5.8 y Ollama.
5. Prueba acotada de consulta de materiales y consolidación de evidencia técnica.

La versión de Ollama, el modelo y los valores de los límites de recursos permanecen pendientes de definición. Los demás plugins documentados no forman parte de esta secuencia.

## Controles y evidencia

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
| MooChat | Revisar compatibilidad declarada, datos enviados, permisos y dependencias | Paquete identificado y ensayo sobre Moodle 4.5.8 con resultados registrados |
| Operación | Definir actualización, parada, diagnóstico, desinstalación y recuperación | Procedimiento con controles y resultados reproducibles |
| Presentación | Consolidar capacidades, restricciones, costos de recursos y pendientes | Propuesta técnica basada en evidencia, pendiente de aprobación institucional |

## Límites de ensayo

No usar datos personales o institucionales reales. No crear cursos como prueba. No habilitar acceso desde red ni integrar plugins automáticamente. Distinguir el servicio que responde de la calidad de sus respuestas, y la compatibilidad declarada del funcionamiento comprobado.

Ante falta de memoria, degradación de Moodle/MySQL, exposición inesperada o envío no previsto de datos, detener la prueba y registrar el incidente antes de ampliar el alcance.

## Fuentes

Los fundamentos se registran en [seguridad y confidencialidad](seguridad-confidencialidad.md), con fecha, enlaces y estado de validación de los controles. MooChat es el candidato priorizado. La selección de versión de Ollama y modelo continúa pendiente.
