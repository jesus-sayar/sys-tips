## Commands

Lista de comandos útiles para el trabajo con sistemas.

### Nginx

`curl --header "Host: foobar.com" "http://localhost:80"`

Ejecutando este comando desde la maquina donde hay un Nginx. Podemos verificar que el Nginx funciona correctamente
y saltarnos los balanceadores que hay por encima.

`cat site.access.log | cut -d ' ' -f 4 | cut -d : -f2 | uniq -c`

Devuelve todas las peticiones

**Útil cuando** queremos saber si un comportamiento anómalo de nuestro aplicativo es debido a una alta cantidad de peticiones.

`awk '{print $9}' site.access.log | sort | uniq -c | sort`

Devuelve un lista con el numero de respuestas por codigo HTTP de respuesta (200, 400, 500, etc...).

**Útil cuando** queremos saber si nuestro aplicativo esta respondiendo adecuadamente a las peticiones.

`awk -F\" '{print $2}' access.log | awk '{print $2}' | sort | uniq -c | sort -r`

Devuelve las URLs mas solicitadas.

`awk -F\" '($2 ~ /XYZ/){print $2}' access.log | awk '{print $2}' | sort | uniq -c | sort -r`

Devuelve las URLs mas solicitadas que contienen XYZ.

### Miscellaneous

`find . -type f -size +50M`

Encuentra todos los ficheros del sistema que ocupan más de 50M.

**Útil cuando** se llena el disco de una máquina que no debería. Puede ser un log, pueden ser ficheros temporales… Esto nos ayuda a ver si hay algo raro.

`du -hcsx *`

Nos muestra los directorios con mayor uso de disco.

**Útil cuando** tenemos problemas de disco y no sabemos por que directorio empezar a buscar

`lsof`

Clasicazo. Muestra un listado de ficheros abiertos del sistema (el modo de apertura, la ruta absoluta del fichero, el tipo de nodo asociado…)

**Útil cuando** quieras saber el estado de un fichero o si está siendo utilizado por alguna parte del sistema.

`mysql -u root -p -h localhost app_dev < app_prod.20151202.sql`

Comando para importar un dump de la base de datos a tu mysql.

**Útil cuando** utilizas una base de datos mysql y quieres cargar un dump de una DB de producción a tu local.

`find /path/* -mtime +5 -exec rm {} \;`

Comando para borrar los ficheros creados en los últimos 5 días. Este es un poco fuerte.

**Útil cuando** disponemos de una máquina en la que sabemos a ciencia cierta que no se han modificado ficheros importantes y tenemos problemas de espacio.

`tail -400f shoryuken.log`

Este es básico. Con este comando visualizamos logs en tiempo real.

**Útil cuando** queremos comprobar en tiempo real si nuestro site está recibiendo peticiones y las está respondiendo correctamente. También es útil concatenarle el comando GREP para ver si hay mas 404 de lo normal, por ejemplo.

### Networking

`curl -4 http://wttr.in/vigo?m`

**Útil cuando** quieres saber el tiempo de tu ciudad sin levantar la vista de la consola.

`curl -kH ‘Host: www.marca.com' -i http://54.243.158.73/`

Con este comando realizamos una petición cURL para forzar una DNS.

**Útil cuando** queremos confirmar que el problema de acceso a un dominio es debido a un fallo en su DNS.

`echo “GET https://www.google.es/" | vegeta attack — rate=5 — duration 30s | vegeta report`

Vegeta es una herramienta para probar como se comporta un site en función de la carga que recibe. Muy útil.

**Útil cuando** queremos estresar un site y ver como se comporta

`netstat -pton | grep 8082`

Solo linuxeros. Comprobamos el puerto X (en este caso 8082)

**Útil cuando** tenemos un servicio que se comunique con dicho puerto y comprobamos si la interfaz de comunicación falla en este punto.

`netstat -pton | grep 8081 | grep -v WAIT | grep -v unicorn | wc -l`

Este es de mis favoritos. Devuelve la cantidad de peticiones en cola del aplicativo, en unidades de peticiones.

**Útil cuando** necesitas comprobar si tus webservers están encolando.

`dig http://marca.com/`

Comando que proporcina información sobre el DNS de un dominio.

**Útil cuando** necesitamos comprobar el correcto funcionamiento de una DNS.
