# Bitácora viva

Registro cronológico del laboratorio. Zona de referencia: America/Buenos_Aires. No representa una receta completa ni una aprobación de despliegue institucional.

## 2026-10-18 — B001 — Apertura y alcance

- **Objetivo:** explorar Ollama local, configuraciones y restricciones, y compatibilidad de plugins Moodle para una futura presentación técnica ante DIRINFO.
- **Acción:** recuperar antecedentes del trabajo anterior, consultar configuración de VirtualBox y consolidar las salidas de sistema aportadas por la administradora.
- **Evidencia:** lectura local de asignación de CPU/RAM; salidas de `cat /etc/os-release`, `uname -m`, `lscpu`, `free -h` y `df -h / /var /home`. Resumen anonimizado en [estado](estado.md).
- **Resultado verificado:** CentOS Stream 9 x86_64, 6 CPU virtuales, RAM visible 8,5 GiB y disponible 7,4 GiB; 63 GB libres en raíz y 146 GB en /home. MySQL confirmado por la administradora, sin versión exacta registrada.
- **Decisión:** evaluar primero la herramienta y sus límites técnicos. Los usos específicos serán definidos posteriormente por las áreas destinatarias.
- **Límites:** no hubo instalación de Ollama, descarga de modelos, prueba de plugins ni cambios en servicios de la VM. No se acredita GPU disponible.
- **Recuperación:** no aplica a cambios de servicios; no se realizaron.
- **Siguiente paso:** preparar instalación y controles con fuentes oficiales actuales.

## 2026-10-18 — B002 — Inicio del repositorio documental

- **Objetivo:** mantener documentación privada, reutilizable y actualizada durante el trabajo.
- **Acción:** consultar el repositorio indicado en GitHub y preparar README, reglas de continuidad, estado, plan de evaluación y matriz de compatibilidad.
- **Evidencia:** API de GitHub informó `private: true`, rama predeterminada `main` y repositorio vacío antes de esta carga inicial.
- **Resultado:** estructura documental inicial preparada; su presencia en la rama remota y el historial de Git acreditan la publicación. La comprobación posterior se comunica al cierre de la sesión.
- **Decisión:** actualizar por cada avance confirmado durante las sesiones; no implementar un monitor de la VM ni actualizaciones ficticias en segundo plano.
- **Recuperación:** restaurar una revisión anterior de documentos mediante un cambio trazable, preservando el historial.
- **Siguiente paso:** comenzar la evaluación técnica de instalación.

## Formato de nuevas entradas

### AAAA-MM-DD — BNNN — Título

- **Objetivo:**
- **Estado:** propuesto / ejecutado informado / verificado / fallido / pendiente.
- **Acción y comandos:** versión y parámetros sustituibles; sin secretos.
- **Evidencia:** salida mínima anonimizada y fuente; «listo» cuando corresponda.
- **Resultado y límites de prueba:**
- **Decisión:**
- **Recuperación:** prevista o ejecutada, diferenciadas.
- **Siguiente paso:**
