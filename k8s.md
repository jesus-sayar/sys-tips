# Kubernetes

Comandos útiles en el trabajo diario con k8s.

`kubectl create -f deployment.yaml`

Crear un recurso desde su definición en un fichero.

`kubectl --namespace kube-system create secret generic telegrafconfig --from-file ./telegraf.conf`

Crear un secret

`kubectl --namespace kube-system port-forward pod_name 5601:5601`

Mapea a un puerto local un servicio del cluster que no está expuesto al exterior.

`kubectl --namespace="monitoring" logs pod_name`

Ver el log de un container.

`kubectl --namespace="monitoring" exec pod_name -c container_name -it -- bash`

Abrir una consola en el contenedor de un Pod.

`kubectl cp [ruta_al_fichero_local]  [namespace]/[pod_name]:[ruta_destino] -c [container_name]`

Copiar un fichero local, a un directorio en un container.

