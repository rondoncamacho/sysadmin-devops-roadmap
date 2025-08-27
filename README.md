Módulo 1: Implementación de la Gestión de Archivos y Comandos del Sistema
Este módulo detalla los procedimientos para la administración de archivos en entornos Linux, centrado en comandos esenciales para la operación y el mantenimiento de sistemas. Se aplican conceptos teóricos sobre la gestión interna del sistema de archivos (inodes, dentry cache) a escenarios reales de administración.

Herramientas y Requisitos del Entorno 🛠️

Entornos de Ejecución: Máquinas virtuales (VMs) con Ubuntu y Debian, con acceso a través de la terminal o SSH.

Utilidades:

Instalar tree: sudo apt update && sudo apt install tree

Verificar conectividad de red entre VMs.

Fase 1: Navegación y Creación de Estructuras
Objetivo: Establecer estructuras de directorios y archivos, y comprender la operación de comandos fundamentales a nivel de kernel.

Procedimientos de Implementación:
Configuración Inicial:

En cada VM, crear el directorio de trabajo: mkdir ~/sysadmin_curso && cd ~/sysadmin_curso.

Verificar el usuario actual (whoami), el directorio de trabajo (pwd) y el contenido del directorio (ls -l).

Creación de Estructura de Servicio:

Para replicar un entorno de servidor, ejecutar el siguiente comando en ambas VMs:
mkdir -p servidor/{logs,public,config,backups}.

Generar archivos representativos:
touch servidor/logs/{access.log,error.log} servidor/public/index.html servidor/config/nginx.conf

Validar la estructura creada con un ls recursivo (ls -R servidor) o con la utilidad tree (tree servidor > arbol_dia1.txt).

Gestión de Archivos de Muestra:

Simular la generación de registros: touch servidor/logs/app{1..3}.log.

Documentación de Procedimientos:

Documentar el proceso de creación de la estructura y la navegación:
echo "# Sección 1: Navegación y Creación\n- Estructura servidor/{logs,public,config,backups} implementada.\n- Navegación y listado de inodos verificados." > notas_sem1.md

Guardar la salida del árbol de directorios para referencia: tree servidor >> arbol_dia1.txt.

Fase 2: Manipulación de Archivos
Objetivo: Gestionar archivos y directorios mediante la manipulación, copia, movimiento y eliminación.

Procedimientos de Ejecución:
Copia de Archivos (cp):

Realizar copias de seguridad de registros:
cp servidor/logs/access.log servidor/backups/access_$(date +%F).bak

Realizar copia de directorios de manera recursiva:
cp -r servidor/public servidor/backups/public_bak

Movimiento y Renombrado (mv):

Mover un archivo de registro a una ubicación diferente:
mv servidor/logs/app2.log servidor/backups/

Renombrar un archivo de configuración para versionado:
mv servidor/config/nginx.conf nginx_$(date +%F).conf

Eliminación de Archivos (rm):

Eliminar archivos temporales de forma interactiva:
touch servidor/temp.txt
rm -i servidor/temp.txt

Eliminar directorios y su contenido de forma recursiva:
mkdir servidor/temp_dir && touch servidor/temp_dir/test.txt
rm -r servidor/temp_dir

Documentación de Procedimientos:

Actualizar las notas de la operación:
echo "- Sección 2: Gestión\n- Logs copiados a backups\n- Configs movidas y renombradas\n- Archivos temporales eliminados" >> notas_sem1.md

Actualizar el árbol de directorios después de las operaciones:
tree servidor > arbol_dia2.txt

Fase 3: Visualización y Edición de Contenido
Objetivo: Inspeccionar y modificar archivos de configuración y registros de forma segura y eficiente.

Procedimientos de Ejecución:
Visualización (cat y less):

Concatenar y visualizar contenido de archivos pequeños:
echo -e "Entrada de registro 1\nEntrada de registro 2" > servidor/logs/sample.log
cat servidor/logs/sample.log

Paginación para archivos extensos (ej. syslog):
less /var/log/syslog (Usar / para buscar, n para siguiente, g/G para inicio/fin y q para salir.)

Edición (nano):

Modificar un archivo de configuración:
nano servidor/config/nginx.conf

Contenido de Ejemplo para nginx.conf:

server_name lazi0-web;
port 8080;
log_path /logs;
Ctrl+O para guardar y Ctrl+X para salir.

Documentación de Procedimientos:

Describir las acciones realizadas:
echo "- Sección 3: Visualización/Edición\n- Concatenación de registros con cat\n- Edición de configs con nano" >> notas_sem1.md

Fase 4: Búsqueda de Archivos
Objetivo: Localizar archivos según criterios específicos, optimizando la gestión de espacio y la detección de problemas.

Procedimientos de Ejecución:
Búsquedas por Criterio (find):

Buscar archivos por nombre:
find ~/sysadmin_curso -name "*.log"

Localizar archivos de gran tamaño (ej. +10MB):
dd if=/dev/zero of=servidor/bigfile.bin bs=1M count=15
find ~/sysadmin_curso -size +10M

Identificar archivos modificados recientemente:
find ~/sysadmin_curso -mtime -1

Ejecución de Comandos en Resultados (-exec):

Listar archivos encontrados:
find ~/sysadmin_curso -name "*.log" -exec ls -l {} \;

Copiar archivos encontrados a una ubicación de respaldo:
find servidor/logs -name "*.log" -exec cp {} servidor/backups/logs/ \;

Documentación de Procedimientos:

Registrar la operación de búsqueda:
echo "- Sección 4: Búsqueda\n- Archivos encontrados con find.\n- Copiados y eliminados con -exec" >> notas_sem1.md

Fase 5: Integración y Documentación Final
Objetivo: Aplicar los conocimientos de las fases previas en un proyecto integrado y generar una documentación completa y auditable.

Procedimientos de Implementación:
Proyecto Integrado de Servidor Web:

Ampliar la estructura de directorios:
mkdir -p servidor/{logs/archive,public/html,config,backups}
touch servidor/logs/{access.log,error.log,archive/old_$(date +%F).log}

Configurar un archivo de ejemplo: nano servidor/config/nginx.conf.

Realizar un respaldo de la configuración:
cp -r servidor/config servidor/backups/config_$(date +%F)

Mover logs antiguos al archivo:
mv servidor/logs/old_*.log servidor/logs/archive/

Buscar y eliminar archivos de gran tamaño generados en la fase anterior:
find servidor -size +10M -exec rm {} \;

Transferir archivos entre VMs si se requiere:
scp servidor/config/nginx.conf user@192.168.56.102:~/sysadmin_curso/servidor/config/

Resultados Esperados:

Estructura del servidor implementada, operativa y documentada.

Procedimientos de copia, movimiento y búsqueda aplicados de forma consistente.

Evidencias y notas del proceso actualizadas en los archivos del proyecto.
