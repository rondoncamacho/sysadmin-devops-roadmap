Módulo 4: Redes y Firewall Básico
Este módulo abarca la configuración de interfaces de red, la verificación de conectividad y la implementación de un firewall básico en sistemas Linux. Se enfoca en la administración de redes a nivel del sistema operativo, con un enfoque en la seguridad y la optimización del acceso.

Herramientas y Requisitos del Entorno 🛠️

Entornos de Ejecución: Máquinas virtuales (VMs) con Ubuntu y Debian.

Utilidades: Se requiere la instalación de ufw, net-tools, dnsutils y tree para la gestión de red, la resolución de DNS y la visualización de la estructura de directorios.

Red: Verificación de la conectividad de red entre VMs.

Fase 1: Diagnóstico de Red y Conectividad (ip y ping)
Objetivo: Inspeccionar las interfaces de red, las direcciones IP y las rutas de enrutamiento, y verificar la conectividad entre dispositivos.

Procedimientos de Operación:
Inspección de Interfaces y Direcciones IP:

El comando ip addr muestra las interfaces de red disponibles y sus direcciones IP.

ip link proporciona un resumen del estado de las interfaces (arriba/abajo).

ip route exhibe la tabla de enrutamiento del sistema, crucial para determinar cómo se dirigen los paquetes.

Verificación de Conectividad (ping):

El comando ping se utiliza para enviar paquetes ICMP y medir la latencia y la pérdida de paquetes.

ping IP_remota

Se utiliza para confirmar la accesibilidad de otros hosts en la red o en internet.

Resultados Esperados:

Un administrador será capaz de diagnosticar problemas de conectividad básicos y validar que las interfaces de red están operativas.

Fase 2: Resolución de Nombres de Dominio (dig)
Objetivo: Auditar y diagnosticar problemas relacionados con la resolución de nombres de dominio (DNS).

Procedimientos de Operación:
Consulta de Registros DNS:

El comando dig se utiliza para interrogar servidores DNS y obtener información detallada sobre nombres de dominio.

dig google.com

Se pueden especificar tipos de registros (ej. A para direcciones IPv4, MX para servidores de correo) y servidores DNS específicos.

Análisis de Archivo de Configuración:

El archivo /etc/resolv.conf en sistemas Linux define los servidores DNS que se utilizan para resolver nombres de dominio.

Resultados Esperados:

Se verificará la correcta resolución de nombres de dominio y se podrán identificar configuraciones erróneas en el servicio DNS, lo que es crítico para el funcionamiento de aplicaciones web.

Fase 3: Monitoreo de Conexiones de Red (netstat)
Objetivo: Inspeccionar las conexiones de red activas y los puertos que están en estado de escucha en el sistema.

Procedimientos de Operación:
Identificación de Puertos y Conexiones:

El comando netstat es una herramienta clave para el monitoreo de la red.

netstat -tuln muestra los puertos TCP (-t) y UDP (-u) que se encuentran en estado de escucha (-l), utilizando notación numérica (-n).

netstat -an muestra todas las conexiones, incluyendo las establecidas.

Auditoría de Servicios:

Al combinar netstat con grep, un administrador puede auditar rápidamente qué servicios están escuchando en qué puertos.

Resultados Esperados:

Un operador podrá verificar que servicios como Nginx y SSH están escuchando en los puertos correctos y que no hay conexiones no autorizadas.

Fase 4: Configuración de Firewall (ufw)
Objetivo: Implementar un firewall básico para controlar el tráfico de red, permitiendo solo las conexiones esenciales para los servicios del servidor.

Procedimientos de Operación:
Gestión de Reglas con ufw:

ufw (Uncomplicated Firewall) es una interfaz simplificada para iptables que facilita la gestión de reglas de netfilter en el kernel de Linux.

sudo ufw status muestra el estado del firewall.

sudo ufw default deny incoming establece una política de "denegar todo" para el tráfico entrante, una práctica de seguridad esencial.

sudo ufw allow 80 permite el tráfico en el puerto 80 (HTTP) para servicios web.

Protección de Servicios:

El comando ufw limit se puede utilizar para proteger servicios como SSH contra ataques de fuerza bruta al limitar el número de conexiones por origen.

Resultados Esperados:

El servidor estará protegido contra el tráfico no deseado, y solo los servicios explícitamente permitidos serán accesibles, reduciendo la superficie de ataque del sistema.