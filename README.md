# Proyecto #3: Backups

> Integrantes:
>* Max Richard Lee Chung - 2019185076 
>* Miguel Ku Liang - 2019061913
>* Adriel Araya Vargas -2019312845
>* André Araya Vargas - 2020142856

## Guía de instalación
El programa necesita de la aplicación "Docker" y habilitar el servicio de "Kubernetes" para tener un clúster inicial y básico, llamado "docker-desktop". La aplicación para supervisar el comportamiento del clúster de Docker se denomina "Lens". Además, se utilizarán dos herramientas con sus respectivas carpetas dentro del proyecto para los servicios automatizados tales como Helm_charts (servicios predeterminados) y Docker_images (servicios programados).

### Instalación de helm charts
Primeramente se debe de gestionar las dependencias de los helm charts de bootstrap, back-ups y databases, los cuales serán necesarios durante toda la ejecución del proyecto. Dentro de los archivos Chart.yaml en en cada carpeta (como por ejemplo, /charts/databases/Chart.yaml), se encuentran declarados la versión, enlace del repositorio y nombre para poder extraer y descargar como un archivo comprimido los recursos de cada uno en la carpeta /charts/databases/charts.

```
#charts/bootstrap/Chart.yalm
dependencies:
  # Elastic Search Operator (includes CRDs)
  # https://www.elastic.co/guide/en/cloud-on-k8s/master/k8s-install-helm.html
  - name: eck-operator
    version: "2.6.1"
    repository: https://helm.elastic.co
```

```
#charts/databases/Chart.yalm
dependencies:
  - name: mongodb
    version: "13.6.7"
    repository: https://charts.bitnami.com/bitnami
    condition: mongodb.enabled
  - name: postgresql
    version: "12.0.0"
    repository: https://charts.bitnami.com/bitnami
    condition: postgresql.enabled
  - name: mariadb
    version: "11.5.3"
    repository: https://charts.bitnami.com/bitnami
    condition: mariadb.enabled
  - name: neo4j
    version: "5.5.0"
    repository: https://helm.neo4j.com/neo4j
    condition: neo4j.enabled 
  - name: couchdb
    version: "3.3.2"
    repository: https://apache.github.io/couchdb-helm
    condition: couchdb.enabled
```
