# Preparación de instalación de Ollama

Fecha: 2026-10-18. Estado: comprobación previa ejecutada y salida verificada; dependencia Zstandard e instalación de Ollama pendientes.

## Base del laboratorio

Entorno registrado: CentOS Stream 9 x86_64, 6 CPU virtuales, 8,5 GiB de RAM visible y 63 GB libres en raíz en la muestra inicial. La primera evaluación se dimensiona para un modelo pequeño y una solicitud a la vez; memoria efectiva y rendimiento requieren medición. No se acredita GPU disponible en el invitado.

La instalación se realizará dentro de la VM con privilegios administrativos y recuperación previa disponible. La clonación anunciada permanece pendiente de confirmación. Moodle, PHP y MySQL no requieren actualización para instalar el servicio independiente.

## Requisitos y parámetros pendientes

- Paquete oficial Linux amd64 y versión identificada antes de ejecutar la instalación.
- Herramientas de descarga y certificados TLS; `tar` y soporte Zstandard para el archivo `.tar.zst` si se utiliza ese método.
- Acceso HTTPS durante la preparación para obtener software y modelo, o transferencia de artefactos previamente descargados y verificados. La descarga se distingue de la inferencia local posterior.
- Usuario de servicio dedicado, servicio systemd y directorio de modelos con permisos exclusivos del servicio según necesidad. Ubicación y límites de CPU/RAM pendientes de definición.
- Configuración inicial: escucha `127.0.0.1:11434`, nube deshabilitada con `OLLAMA_NO_CLOUD=1` y carga acotada. La restricción efectiva de salida de red requiere un control adicional y ensayo.
- Modelo local: identificador, licencia, tamaño y consumo pendientes de selección. No se requiere cuenta de un servicio de IA para la primera prueba local con un modelo público descargable.

Fuente: [instalación Linux oficial](https://docs.ollama.com/linux) y [configuración y operación](https://docs.ollama.com/faq). La configuración del servicio debe quedar preparada antes de la primera operación controlada; el instalador automático puede iniciar el servicio y requiere considerar ese efecto al elegir el método.

## Comprobación previa de solo lectura

Ejecución dentro de la VM:

```bash
rpm -q curl tar zstd ca-certificates
command -v ollama
ss -ltn '( sport = :11434 )'
getenforce
```

Interpretación: paquetes ausentes se registran para instalación; falta de salida de `command -v` indica que el ejecutable no está en el PATH, sin excluir otras instalaciones; el puerto requiere revisión si aparece ocupado. SELinux permanece habilitado según su estado inicial; cualquier impedimento se diagnostica sin deshabilitarlo como solución general.

## Cierre de preparación

### Resultado de comprobación previa

Salida aportada el 2026-10-18:

- `curl`, `tar` y `ca-certificates`: instalados.
- `zstd`: paquete no instalado.
- `command -v ollama`: sin salida; ejecutable no encontrado en PATH.
- Puerto TCP 11434: sin sockets de escucha en la consulta.
- SELinux: `Enforcing`.

### Preparación de la dependencia

Paso pendiente, ejecutado como root dentro de la VM:

```bash
dnf install zstd
rpm -q zstd
```

La transacción debe limitarse al paquete y sus dependencias necesarias; cualquier eliminación o cambio ajeno al objetivo requiere revisión antes de aceptar. La salida de instalación y consulta acredita el cierre de este paso. SELinux conserva el modo Enforcing.

Evidencia requerida: recuperación disponible, herramientas presentes, ausencia de conflicto con servicio previo, versión y modelo seleccionados, configuración de servicio y recursos definida. La instalación aún no se considera ejecutada.
