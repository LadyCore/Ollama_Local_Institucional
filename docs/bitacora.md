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

## 2026-10-18 — B003 — Revisión de seguridad y confidencialidad

- **Objetivo:** preparar fundamentos verificables para explicar protección de datos ante DIRINFO.
- **Estado:** revisión documental verificada; controles propuestos, no ejecutados.
- **Acción:** consultar fuentes oficiales de privacidad, FAQ, autenticación, Linux, diagnóstico, herramientas y política de seguridad del proyecto.
- **Evidencia:** URLs y conclusiones en [seguridad y confidencialidad](seguridad-confidencialidad.md).
- **Resultado:** distinguir inferencia local de nube, ausencia de autenticación local y responsabilidades de plugins/host. Definir controles de red, acceso, persistencia, privilegios, recursos y mantenimiento con pruebas de aceptación.
- **Decisión propuesta:** comenzar con datos sintéticos, modo local y exposición restringida; verificar salida efectiva antes de admitir datos reales.
- **Límites:** no se instalaron componentes ni modificaron servicios; no hay certificación de cumplimiento ni plugin validado.
- **Recuperación:** no aplica a la VM; cambio exclusivamente documental.
- **Siguiente paso:** seleccionar versión y convertir los controles en un procedimiento de instalación y prueba.

## 2026-10-18 — B004 — Candidatos para Moodle 4.5.8 y Ollama

- **Objetivo:** identificar funciones disponibles para orientar la elección posterior de usos.
- **Estado:** investigación documental verificada; ensayo pendiente.
- **Acción:** consultar MoodleDocs 4.5, fichas y versiones de Marketplace y repositorios de autores.
- **Evidencia:** enlaces, releases y builds en [matriz](compatibilidad-moodle.md).
- **Resultado:** proveedor incluido y cuatro plugins con soporte declarado 4.5/Ollama; distinción de Stable/Alpha y puntos de seguridad de cada candidato.
- **Decisión propuesta:** comenzar por conexión core; escoger luego editor, chat o RAG según evaluación. No asumir compatibilidad exacta del entorno ni cadenas de datos completamente locales sin ensayo.
- **Límites:** sin instalación, auditoría completa de código o prueba funcional. No se crearon cursos.
- **Recuperación:** no aplica a VM; actualización documental.
- **Siguiente paso:** instalar y validar Ollama antes de ensayar integraciones; revisar paquete exacto y dependencias del candidato elegido.

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
