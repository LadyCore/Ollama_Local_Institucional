# Entorno y estado

Actualizado: 2026-10-18. Etapa: preparación documental.

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
- Restricciones y límites: por diseñar y ensayar.
- Plugins: ninguno declarado compatible o habilitado por este proyecto.
- Integración, acceso desde red y uso institucional: pendientes de evaluación y aprobación específica.

## Próxima secuencia

1. Consultar documentación oficial actual de Ollama para Linux, configuración, operación local y recursos.
2. Preparar instalación y recuperación, decidir ubicación de modelos y límites considerando la convivencia con Moodle/MySQL.
3. Instalar y comprobar localmente con un modelo adecuado al laboratorio y datos sintéticos.
4. Evaluar restricciones y consumo; registrar fallos y límites.
5. Recuperar/verificar versiones exactas de Moodle/PHP/MySQL cuando sean necesarias para compatibilidad y estudiar candidatos.
6. Preparar procedimiento y propuesta técnica para DIRINFO basados en resultados.
