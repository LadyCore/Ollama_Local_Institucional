# Preparación de instalación de Ollama

Fecha: 2026-10-18. Estado: cliente verificado y cuenta dedicada creada; corrección del shell ejecutada sin advertencias, comprobación del registro y configuración del servicio pendientes.

## Base del laboratorio

### Componentes independientes

Ollama no forma parte de la distribución estándar de Moodle 4.5 y requiere instalación independiente en el sistema operativo. Moodle 4.5 incluye el subsistema de IA y el conector `aiprovider_openai`, que puede configurarse para comunicarse con Ollama local mediante su API compatible. Los modelos se descargan por separado. MooChat es una actividad adicional para Moodle y su instalación corresponde a una etapa posterior.

La [documentación oficial de Moodle 4.5](https://docs.moodle.org/405/en/Ollama) establece como requisitos separados Moodle en funcionamiento, Ollama instalado y un modelo disponible. La presencia del conector en Moodle no acredita instalación del motor ni disponibilidad de modelos.

Entorno registrado: CentOS Stream 9 x86_64, 6 CPU virtuales, 8,5 GiB de RAM visible y 63 GB libres en raíz en la muestra inicial. La primera evaluación se dimensiona para un modelo pequeño y una solicitud a la vez; memoria efectiva y rendimiento requieren medición. No se acredita GPU disponible en el invitado.

La instalación se realizará dentro de la VM con privilegios administrativos y recuperación previa disponible. La clonación anunciada permanece pendiente de confirmación. Moodle, PHP y MySQL no requieren actualización para instalar el servicio independiente.

## Requisitos y parámetros pendientes

- Paquete oficial Linux amd64 v0.40.6 identificado para descarga; extracción e instalación pendientes.
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

Paso ejecutado como root dentro de la VM y verificado mediante salida de instalación y consulta:

```bash
dnf install zstd
rpm -q zstd
```

La transacción debe limitarse al paquete y sus dependencias necesarias; cualquier eliminación o cambio ajeno al objetivo requiere revisión antes de aceptar. La salida de instalación y consulta acredita el cierre de este paso. SELinux conserva el modo Enforcing.

Resultado: `zstd-1.5.5-1.el9.x86_64` instalado desde BaseOS. Una instalación, sin actualizaciones ni eliminaciones informadas en la transacción.

### Descarga del paquete identificado

Fuente: [release oficial v0.40.6](https://github.com/ollama/ollama/releases/tag/v0.40.6), publicada el 2026-10-16 y señalada como última release no preliminar por la API de GitHub al consultar. Archivo `ollama-linux-amd64.tar.zst`, tamaño 1438364593 bytes. Digest publicado: `sha256:c164ab8b1b28e2a247c29719b8e404c423c5b83ae64c3ab4e59d50c7ff7fc5e0`.

Método de preparación: descarga del archivo versionado, comprobación de hash y posterior extracción manual. La descarga no ejecuta el instalador ni inicia el servicio. La identificación de release no constituye auditoría completa de seguridad.

Comandos ejecutados y salida de descarga y SHA-256 verificada:

```bash
curl -fL --retry 3 -o /var/tmp/ollama-linux-amd64-v0.40.6.tar.zst https://github.com/ollama/ollama/releases/download/v0.40.6/ollama-linux-amd64.tar.zst
sha256sum /var/tmp/ollama-linux-amd64-v0.40.6.tar.zst
```

El hash debe coincidir con el digest publicado antes de extraer o ejecutar. La extracción, el usuario, el servicio y sus restricciones corresponden al paso posterior. El archivo temporal de preparación se incluye en el inventario de almacenamiento y limpieza.

Resultado: descarga finalizada y SHA-256 `c164ab8b1b28e2a247c29719b8e404c423c5b83ae64c3ab4e59d50c7ff7fc5e0`, coincidente con el digest publicado. Los intentos anteriores incluyeron errores de transcripción en URL (HTTP 404) y una descarga vacía por uso de `-fl` en lugar de `-fL`; la descarga correcta reemplazó ese archivo.

### Extracción del paquete verificado

Paso ejecutado como root, según el método manual de la guía Linux oficial:

```bash
tar --zstd -xf /var/tmp/ollama-linux-amd64-v0.40.6.tar.zst -C /usr
```

Resultado observado: retorno al prompt sin mensajes de error. El primer intento omitió `.zst` en el nombre y terminó sin encontrar el archivo; el segundo utilizó el nombre completo y finalizó sin errores visibles. Este paso coloca los archivos del paquete en `/usr`; no crea ni inicia por sí mismo el servicio systemd.

Comprobación del ejecutable ejecutada:

```bash
/usr/bin/ollama --version
```

Resultado observado: `Warning: could not connect to a running Ollama instance` y `Warning: client version is 0.40.6`. Cliente ejecutable y versión confirmados; el servicio aún no está iniciado. Esta consulta no acredita funcionamiento de inferencia.

### Usuario del servicio

Cuenta y grupo creados como root; `id ollama` confirma uid 995, gid 994 y pertenencia al grupo propio. Se observó advertencia por ruta de shell mal transcrita; el shell sin inicio de sesión interactivo requiere corrección.

```bash
useradd -r -U -m -d /usr/share/ollama -s /sbin/nologin ollama
id ollama
```

Si la cuenta ya existe, su configuración requiere comprobación antes de continuar; no se elimina ni reemplaza automáticamente. El servicio se configurará para ejecutarse con esta cuenta, sin privilegios de root.

Corrección ejecutada sobre la cuenta existente; comprobación con `getent` pendiente:

```bash
usermod -s /sbin/nologin ollama
getent passwd ollama
```

La última columna debe ser `/sbin/nologin`. Esta corrección no requiere recrear la cuenta ni cambiar su uid/gid.

Resultado observado: un intento intermedio utilizó una barra final en la ruta y produjo advertencia. El comando final `usermod -s /sbin/nologin ollama` regresó al prompt sin mensajes; lectura del registro de cuenta pendiente.

Pendientes de preparación: lectura del registro de cuenta, configuración de red y recursos, selección de modelo y recuperación disponible. La versión del cliente no acredita servicio operativo ni inferencia validada.
