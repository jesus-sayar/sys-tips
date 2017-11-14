# Kubernetes

Comandos útiles en el trabajo diario con k8s.

`kubectl --namespace kube-system create secret generic telegrafconfig --from-file ./telegraf.conf`

Crear un secret

`kubectl --namespace kube-system port-forward fca-elk-2932802293-bjk29 5601:5601`

Mapea a un puerto local un servicio del cluster que no está expuesto al exterior.

`kubectl --namespace="test-monitoring" logs influxdb-f6d57b97c-bvbmn`

Ver el log de un container.
