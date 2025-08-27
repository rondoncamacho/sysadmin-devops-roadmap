Módulo 2: Gestión de Permisos y Administración de Procesos
Este módulo se enfoca en la implementación de controles de acceso y la administración de procesos en entornos de servidor Linux. Los procedimientos detallados se basan en la comprensión de la gestión interna del sistema de archivos (inodes) y la tabla de procesos del kernel.

Herramientas y Requisitos del Entorno 🛠️

Entornos de Ejecución: Máquinas virtuales (VMs) con Ubuntu y Debian, accesibles a través de la terminal o SSH.

Utilidades: Se requiere la instalación de htop y tree para el monitoreo avanzado y la visualización de la estructura de directorios (sudo apt install htop tree).

Red: Verificación de conectividad de red entre VMs.

Usuarios: Se recomienda el uso de una cuenta no-root para los procedimientos de prueba, como testuser.

Fase 1: Implementación de Permisos de Acceso (chmod y chown)
Objetivo: Configurar permisos de archivos y directorios para asegurar recursos del servidor, controlando el acceso a usuarios y grupos.

Procedimientos de Operación:
Auditoría de Permisos:

Inspeccionar los permisos de un archivo o directorio con el comando ls -l.

Utilizar ls -li para visualizar el número de inode, que almacena los metadatos de permisos.

Gestión de Permisos con chmod:

Notación Numérica: Aplicar permisos de lectura y escritura para el propietario y solo lectura para el grupo y otros (644).

chmod 644 archivo.txt

Notación Simbólica: Añadir o remover permisos específicos.

Otorgar permisos de ejecución al propietario de un script: chmod u+x script.sh

Remover permisos de escritura para el grupo: chmod g-w archivo.txt

Gestión de Propietarios y Grupos con chown:

Cambiar el propietario de un archivo:

sudo chown nuevo_usuario archivo.txt

Modificar recursivamente el propietario de un directorio y su contenido:

sudo chown -R www-data:www-data /var/www/html

Resultados Esperados:

La aplicación de estos comandos asegurará que los archivos sensibles, como configuraciones o registros, solo sean accesibles por los usuarios autorizados, y que los scripts ejecutables tengan los permisos adecuados para su operación.

Fase 2: Monitoreo y Administración de Procesos (ps, top, htop, kill)
Objetivo: Monitorear el estado del sistema, identificar procesos problemáticos y resolver problemas de sobrecarga.

Procedimientos de Operación:
Monitoreo en Tiempo Real:

ps: Listar procesos con detalles de usuario, PID y uso de recursos: ps aux

top: Visualizar un listado dinámico de los procesos más intensivos en CPU y memoria. Utilizar Shift + P para ordenar por CPU.

htop: Proporciona una interfaz interactiva para el monitoreo. Permite buscar procesos (F3), ver la jerarquía en forma de árbol (F5) y enviar señales de forma sencilla (F9).

Control de Procesos:

kill: Finalizar un proceso mediante su ID (PID).

Finalización estándar (gentil): kill PID

Finalización forzada (sin preguntar): kill -9 PID

killall: Finalizar todos los procesos con un nombre específico:

killall stress

Resultados Esperados:

Un operador será capaz de identificar procesos que están consumiendo recursos de manera anormal y tomar acciones correctivas inmediatas para restablecer la estabilidad del sistema.

Fase 3: Optimización de la Prioridad de Procesos (nice y renice)
Objetivo: Ajustar la prioridad de ejecución de procesos para una mejor gestión de la carga del sistema, evitando que tareas de baja prioridad afecten el rendimiento de servicios críticos.

Procedimientos de Operación:
Asignación de Prioridad en el Inicio (nice):

Iniciar una tarea con una prioridad baja (valor nice alto, por ejemplo 15) para que el kernel le asigne menos tiempo de CPU:

nice -n 15 stress --cpu 4

Modificación de Prioridad en Ejecución (renice):

Cambiar la prioridad de un proceso que ya se está ejecutando. Esto es útil para bajar o subir la prioridad de un proceso existente.

Bajar la prioridad: renice 10 -p PID

Aumentar la prioridad (requiere sudo): sudo renice -5 -p PID

Resultados Esperados:

Los administradores pueden ejecutar tareas de mantenimiento intensivas, como respaldos o análisis de datos, sin comprometer el rendimiento de los servicios de misión crítica que se ejecutan en el mismo servidor.

Proyecto Integrado: Servidor Seguro con Monitoreo
Objetivo: Combinar los conocimientos del módulo para simular un escenario de servidor real, aplicando permisos, monitoreo y resolución de problemas.

Procedimientos de Implementación:
Configuración del Entorno:

Instalar un servicio web (sudo apt install nginx) para simular un entorno de producción.

Crear una estructura de directorios y archivos para el servicio, asegurando que los permisos de los archivos y los propietarios sean los correctos.

Ejecución y Troubleshooting:

Monitorear los procesos de Nginx con htop o ps.

Simular una sobrecarga de CPU con la herramienta stress.

Utilizar renice para ajustar la prioridad de la carga de trabajo y killall para terminarla, demostrando la capacidad de respuesta a un incidente.

Permisos:

0	0	---	Ningún permiso.
1	1	--x	Solo permiso de ejecución.
2	2	-w-	Solo permiso de escritura.
3	2 + 1	-wx	Permiso de escritura y ejecución.
4	4	r--	Solo permiso de lectura.
5	4 + 1	r-x	Permiso de lectura y ejecución.
6	4 + 2	rw-	Permiso de lectura y escritura.
7	4 + 2 + 1	rwx	Permiso de lectura, escritura y ejecución.
