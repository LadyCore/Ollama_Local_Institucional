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
- Distribución de componentes: Moodle 4.5 incluye el subsistema IA y su conector; Ollama y sus modelos requieren instalación/descarga independientes. [Detalle](preparacion-ollama.md).
- Preparación: [comprobación previa, dependencia y descarga](preparacion-ollama.md) verificadas. zstd 1.5.5-1.el9.x86_64 instalado. Paquete oficial Ollama v0.40.6 descargado con SHA-256 coincidente. Extracción, configuración de servicio, modelo y límites concretos pendientes. SELinux Enforcing en la comprobación inicial.
- Modelos: ninguno seleccionado o descargado por este proyecto.
- Restricciones y límites: requisitos de validación en [seguridad y confidencialidad](seguridad-confidencialidad.md); implementación y ensayo pendientes.
- Plugins: MooChat priorizado; v1.8.2 / 2026042801 **Beta**, declarado para 4.5. [Revisión inicial de código y comparación con Asyntai](revision-moochat.md) registrada. Ninguno ensayado ni habilitado; objetivo 4.5.8. Otros candidatos como referencia en [bots por curso](bots-por-curso.md).
- Integración, acceso desde red y uso institucional: pendientes de evaluación y aprobación específica.
- Documentación: referencias a las áreas del entorno expresadas mediante denominaciones genéricas; README limitado a descripción y método técnico. Reglas de actuación del asistente en AGENTS.md. Repositorio privado; revisión del historial pendiente antes de una eventual publicación.
- Antecedentes: [ChatOllama y fuentes directamente aplicables](antecedentes-github.md) registrados. Reporte de seguridad de MooChat sobre extracción PPTX contrastado con código; integración condicionada a resolución o exclusión verificable de la ruta. Sin reproducción local.

## Alcance de la primera prueba

Primera prueba pequeña y progresiva: validar Ollama local sin conexiones externas y evaluar una consulta acotada de material de curso. No habilitar múltiples funciones ni decidir usos académicos. Los demás candidatos quedan como referencias futuras. Terus RAG v1.0.9 no supera la revisión dirigida para ese objetivo: ver [hallazgos](revision-terusrag.md). No se instala ni se desarrolla un fork en este paso.

## Secuencia de trabajo definida

1. Preparación de recuperación antes de instalar; clonación anunciada, finalización pendiente de confirmación.
2. Definición de versión de Ollama, modelo, almacenamiento y límites para convivencia con Moodle/MySQL.
3. Instalación y comprobación de inferencia local con datos sintéticos.
4. Validación de restricciones de red, persistencia y consumo.
5. Comprobación de versiones efectivas del entorno, revisión final de MooChat e integración acotada.
6. Consolidación de resultados para la propuesta técnica ante la instancia jerárquica superior.

El ensayo de migración de MySQL a MariaDB previsto en otro clon constituye trabajo independiente. No se registra una migración ejecutada ni se modifica el inventario confirmado de este laboratorio.
