Comando tar
------------

el comando .tar bien conocido para comprimir archivos en linux, otra función de tar es hacer backups-->

Comando para hacer backup completo:

    $ tar -cpvzf "fullbackup_`date +%d%m%Y`.tgz" -g /home/usuario/backup.snap /home/usuario/recursos/*    

Comando para hacer un backup incremental:

    $ tar -cpvzf "inc_backup_`date +%d%m%Y`.tgz" -g /home/usuario/backup.snap /home/usuario/recursos/*
    
Comando para hacer backup diferencial:
    $ tar -cpvzf "dif1_backup_`date +%d%m%Y`.tar.gz" /home/usuario/recursos/* -N 09-feb-15


Escalada de privilegios-->

Otra caracteristica curiosa es que se puede aprobechar  la creaccion de backups para escalar privilegios del sistema.


La creacion de backups necesita de privilegios, por lo tanto al usar tar para comprimir o descomprimir estaremos ejecutando este comando con permisos de root.

mediante el uso de checkpoint. si lo ejecutamos, toma checkpoint como un parametro de tar y nos crea una shell. una bin sh en este caso. 

    --checkpoint=1 checkpoint-action=exec=/bin/sh



la idea es aprobecharse de las wildcads en tar, como el asterisco, si comprimimos todo mediante "*" no sabemos exactamente que permisos tienen asignados todos los archivos que estamos comprimiendo y si a uno, por lo que sea le hemos podido asignar permisos SUID, podriamos ejecutar comandos como root temporalmente.
