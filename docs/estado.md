# Entorno y estado

Actualizado: 2026-10-18. Etapa: revisión documental de seguridad completada; controles sin aplicar.

## Inventario de laboratorio confirmado

| Componente | Evidencia disponible | Fuente |
|---|---|---|
| Virtualización | VirtualBox sobre notebook Windows | Contexto confirmado y consulta local |
| Sistema invitado | CentOS Stream 9, x86_64 | Salida aportada de os-release y uname |
| CPU presentada al invitado | AMD Ryzen 7 7730U with Radeon Graphics | Salida aportada de lscpu |
| CPU virtuales asignadas | 6 | Configuración local de VirtualBox leída |
| RAM asignada | 9250 MB | Configuración local de VirtualBox leída |
| RAM visible / disponible | 8,5 GiB / 7,4 GiB | Muestra de free -h aportada |
| Swap total / usada | 4,5 GiB / 0 B | Misma muestra |
| Raíz | 70 GB totales, 63 GB libres; /var comparte raíz | Salida aportada de df -h |
| /home | 148 GB totales, 146 GB libres | Misma muestra |
| Base de datos | MySQL; versión pendiente de recuperar o verificar | Confirmación de la administradora |
| Moodle y PHP | Versiones exactas pendientes de recuperar o verificar | No trasladar versiones de otro laboratorio |
| GPU de cómputo | No acreditada dentro de la VM | El nombre del procesador no demuestra acceso a GPU |

La memoria disponible y el espacio libre son mediciones puntuales, no reservas garantizadas. No se conservan identificadores ni capturas originales en el repositorio.

## Situación

- Ollama: no instalado por este proyecto; sin prueba de funcionamiento.
- Modelos: ninguno seleccionado o descargado por este proyecto.
- Restricciones y límites: propuesta inicial en [seguridad y confidencialidad](seguridad-confidencialidad.md); implementación y ensayo pendientes.
- Plugins: MooChat priorizado; v1.8.2 / 2026042801 **Beta**, declarado para 4.5. [Revisión inicial de código y comparación con Asyntai](revision-moochat.md) registrada. Ninguno ensayado ni habilitado; objetivo 4.5.8. Otros candidatos como referencia en [bots por curso](bots-por-curso.md).
- Integración, acceso desde red y uso institucional: pendientes de evaluación y aprobación específica.

## Alcance inmediato corregido

Primera prueba pequeña y progresiva: validar Ollama local sin conexiones externas y evaluar una consulta acotada de material de curso. No habilitar múltiples funciones ni decidir usos académicos. Los demás candidatos quedan como referencias futuras. Terus RAG v1.0.9 no supera la revisión dirigida para ese objetivo: ver [hallazgos](revision-terusrag.md). No se instala ni se desarrolla un fork en este paso.

## Secuencia de referencia, no compromiso de ejecución inmediata

1. Revisión inicial oficial de Linux, privacidad, autenticación y seguridad realizada; seleccionar versión y revisar sus avisos antes de instalar.
2. Preparar instalación y recuperación, decidir ubicación de modelos y límites considerando la convivencia con Moodle/MySQL.
3. Instalar y comprobar localmente con un modelo adecuado al laboratorio y datos sintéticos.
4. Evaluar restricciones y consumo; registrar fallos y límites.
5. Recuperar/verificar versiones exactas de Moodle/PHP/MySQL cuando sean necesarias para compatibilidad y estudiar candidatos.
6. Preparar procedimiento y propuesta técnica para DIRINFO basados en resultados.
