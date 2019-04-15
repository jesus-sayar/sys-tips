## Commands

### Nginx

#### Peticion curl con cabeceras
`curl --header "Host: foobar.com" "http://localhost:80"`

#### Get total requests by status code
Devuelve un lista con el numero de respuestas por codigo HTTP de respuesta (200, 400, 500, etc...)
`awk '{print $9}' /var/log/nginx/access.log | sort | uniq -c | sort -rn`

#### get top requesters by IP
`awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -rn | head | awk -v OFS='\t' '{"host " $2 | getline ip; print $0, ip}'`

#### get top requesters by user agent
`awk -F'"' '{print $6}' /var/log/nginx/access.log | sort | uniq -c | sort -rn | head`

#### get top requests by URL
`awk '{print $7}' /var/log/nginx/access.log | sort | uniq -c | sort -rn | head`

#### get top URL returning 404 Not Found
`awk '$9 ~ /404/ {print $7}' /var/log/nginx/access.log | sort | uniq -c | sort -rn | head`

#### get all request of last 10 minutes
awk -v date=$(date +[%d/%b/%Y:%H:%M --date="-10 minutes") '$4 > date' /var/log/nginx/access.log

### Miscellaneous

#### Ver logs en tiempo real
**Útil cuando** queremos comprobar en tiempo real si nuestro site está recibiendo peticiones y las está respondiendo correctamente. También es útil concatenarle el comando GREP para ver si hay mas 404 de lo normal, por ejemplo.

`tail -400f shoryuken.log`

#### Encuentra todos los ficheros del sistema que ocupan más de 50M.
`find . -type f -size +50M`

#### Directorios con mayor uso de disco.
`du -hcsx *`

#### listado de ficheros abiertos del sistema.
Útil cuando quieras saber el estado de un fichero o si está siendo utilizado por alguna parte del sistema.
`lsof`

### MySQL

#### Importar un dump de la base de datos a tu mysql.
`mysql -u root -p -h localhost app_dev < app_prod.20151202.sql`

### Networking
#### Test de carga con Vegeta
`echo “GET https://www.google.es/" | vegeta attack — rate=5 — duration 30s | vegeta report`

#### Comprar el estaedo del puerto X
**Útil cuando** tenemos un servicio que se comunique con dicho puerto y comprobamos si la interfaz de comunicación falla en este punto.
`netstat -pton | grep 8082`

#### Comprar cantidad de peticiones en cola del aplicativo
**Útil cuando** necesitas comprobar si tus webservers están encolando.
`netstat -pton | grep 8081 | grep -v WAIT | grep -v unicorn | wc -l`

### DNS

#### Información sobre el DNS de un dominio.
`dig http://marca.com/`

#### Servidores DNS donde está alojado un dominio
`host -t ns marca.com`

```
marca.com name server a1-235.akam.net.
marca.com name server a10-66.akam.net.
marca.com name server a28-64.akam.net.
marca.com name server a3-65.akam.net.
marca.com name server a18-67.akam.net.
marca.com name server a7-66.akam.net.
```

#### Valores del dominio en el servidor de DNS
`host -t a marca.com a1-235.akam.net.`

```
Using domain server:
Name: a1-235.akam.net.
Address: 193.108.91.235#53
Aliases:
marca.com has address 193.110.128.82
```
