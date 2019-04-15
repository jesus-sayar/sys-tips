`gcloud docker -- push eu.gcr.io/[project_id]/[image_name]:[version]`

Subir una imagen al Registro de Contenedores de Google Cloud.

`gcloud container builds submit --config cloudbuild.yaml .`

Ejecutar manualmente desde local Google Cloud Container Builder, 
para que haga la creación de imágenes de Docker en base al fichero cloudbuild.yaml en local.

`gcloud init`

Crear una configuración para un nuevo proyecto.

`gcloud config configurations list`

Ver las configuraciones disponibles.

`gcloud config configurations describe [configuration-name]`

Ver la información de una configuración.

`gcloud config configurations active [configuration-name]`

Activar una determinada configuración.