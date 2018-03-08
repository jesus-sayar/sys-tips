# SSL

## Generar certificado SSL

	1. Generamos un CSR con openssl (una petición de certificado).
	2. Solictiamos el certificado a una entidad certificadora y pagamos el certificado.
	3. La entidad certificadora mandará un email al dueño del dominio para confirmar que quieren crearlo y no es una petición falsa.
	4. El dueño del dominio confirma un email que le llega a ese buzón.
	5. Se genra el certificado.
	6. Lo instalamos.

## Entidades certificadoras

### Amazon

	- Es gratis porque sólo puedes usar los certificados con sus balanceadores.

	- No puedes descargarlos ni meterlos en un nginx

## Otros comunes

	- RapidSSL
	- Symantec
	- Comodo

