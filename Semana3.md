Módulo 3: Gestión de Usuarios y Conectividad Segura (SSH)
Este módulo se centra en la administración de usuarios y la configuración de acceso remoto seguro en sistemas Linux. Se cubren los procedimientos para la creación de usuarios con privilegios limitados, la configuración del demonio SSH (sshd), y la implementación de autenticación basada en claves públicas para fortalecer la seguridad.

Herramientas y Requisitos del Entorno 🛠️

Entornos de Ejecución: Máquinas virtuales (VMs) con Ubuntu y Debian, con acceso a través de la terminal o SSH.

Utilidades: Se requiere la instalación de openssh-server para la conectividad remota y tree para la visualización de directorios.

Red: Verificación de la conectividad de red entre VMs.

Fase 1: Administración de Usuarios (adduser, passwd, usermod)
Objetivo: Crear y gestionar cuentas de usuario de manera segura, entendiendo la estructura del sistema de usuarios del kernel.

Procedimientos de Operación:
Creación y Verificación de Usuarios:

Crear una nueva cuenta de usuario con adduser. Este comando gestiona de forma interactiva la creación del usuario, su directorio home y la configuración de la contraseña.

sudo adduser nuevo_usuario

Inspeccionar la información del usuario en /etc/passwd y la gestión de contraseñas en /etc/shadow.

Asignación de Privilegios sudo:

Otorgar privilegios de administrador a un usuario sin compartir la contraseña de root mediante el comando usermod.

sudo usermod -aG sudo usuario

La validación de los permisos se realiza mediante el sudo -l, que lista las reglas de sudo para el usuario actual.

Resultados Esperados:

Un entorno multiusuario con cuentas de acceso diferenciadas, donde los privilegios de administrador se conceden de forma granular para evitar el uso del usuario root.

Fase 2: Conexión Remota Segura con SSH
Objetivo: Configurar el servicio sshd para permitir conexiones remotas seguras entre servidores y deshabilitar métodos de autenticación no seguros.

Procedimientos de Operación:
Configuración del Demonios SSH (sshd_config):

El archivo de configuración principal de SSH se encuentra en /etc/ssh/sshd_config.

Se recomienda cambiar el puerto por defecto (22) para reducir el riesgo de ataques automatizados y deshabilitar el acceso de root y la autenticación por contraseña.

sudo nano /etc/ssh/sshd_config

Port 2222

PermitRootLogin no

PasswordAuthentication no

Conexión entre VMs:

Utilizar el comando ssh para establecer una conexión remota segura.

ssh usuario@IP_remota

Para usar el puerto personalizado: ssh -p 2222 usuario@IP_remota

Resultados Esperados:

El servidor solo permitirá conexiones a través de un puerto no estándar y no aceptará autenticación por contraseña, lo que reduce drásticamente la superficie de ataque.

Fase 3: Autenticación por Claves Públicas
Objetivo: Implementar un método de autenticación más seguro que las contraseñas, basado en pares de claves públicas y privadas.

Procedimientos de Operación:
Generación de un Par de Claves:

Crear un par de claves (id_rsa y id_rsa.pub) utilizando ssh-keygen.

ssh-keygen -t rsa -b 4096

Copia de la Clave Pública:

Transferir la clave pública al servidor remoto para permitir el acceso sin contraseña con ssh-copy-id. Este comando gestiona la creación del archivo authorized_keys.

ssh-copy-id -p 2222 usuario@IP_remota

Resultados Esperados:

Los usuarios podrán acceder a los servidores de forma segura sin necesidad de introducir una contraseña, lo que simplifica la automatización y protege contra ataques de fuerza bruta.

Proyecto Integrado: Servidor Seguro con Usuarios y SSH
Objetivo: Consolidar los conocimientos para configurar un servidor con un modelo de seguridad robusto, basado en usuarios con privilegios limitados y acceso remoto por claves SSH.

Procedimientos de Implementación:
Creación de Estructura de Proyecto:

mkdir -p /srv/webapp/{logs,public,config}

Configuración de Usuarios:

Crear un usuario de administración (sysadmin) y otorgarle privilegios de sudo.

Configuración de SSH:

Configurar sshd para que solo acepte autenticación basada en claves.

Despliegue y Pruebas:

Generar y copiar las claves SSH desde el usuario sysadmin en una VM a la otra.

Demostrar la transferencia segura de archivos con scp.

Validar que el acceso de root está deshabilitado.
