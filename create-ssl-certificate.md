# Crear Certificado SSL

## Paso 1 - Crear fichero de configuración

```
$ mkdir san
$ cd san
$ touch ssl.conf
$ open -a TextEdit ssl.conf
```

Introducir el siguiente contenido:

```
[ req ]
default_bits = 4096
distinguished_name = req_distinguished_name
req_extensions = req_ext
prompt = no

[ req_distinguished_name ]
C = ES
ST = Madrid
L = Villaviciosa de Odon
O = NOMBRE DE LA EMPRESA
OU = TIC
emailAddress = sysadmins@the-cocktail.com 
CN = *.wadus.es

[ req_ext ]
subjectAltName = @alt_names

[alt_names]
DNS.1 = *.wadus.es
DNS.2 = wadus.es
```


NOTAS:

- Usa DNS. para añadir todos los posibles dominios y subdominios.
- El common name (CN) el el dominio principal que tu verificas. Asegurate que ese dominio está tambíen en [alt_names] (DNS.#).


## Paso 2 - Creamos la clave privada

`$ openssl genrsa -out private.key 4096`

## Paso 3 - Creamos el CSR

`$ openssl req -new -sha256 -out private.csr -key private.key  -config ssl.conf`

## Paso 4 - Verificamos el CSR

Usar la web [https://www.sslshopper.com/csr-decoder.html](https://www.sslshopper.com/csr-decoder.html) para verificar que el CSR está correctamente creado.

FUENTES: [https://medium.com/@rkakodker/how-to-simple-way-of-generating-wildcard-san-ssl-csrs-for-product-managers-8c25d715d86f](https://medium.com/@rkakodker/how-to-simple-way-of-generating-wildcard-san-ssl-csrs-for-product-managers-8c25d715d86f) 