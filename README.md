# Elasticsearch Helm Charts

This repository contains Helm charts for deploying Elasticsearch in a Kubernetes cluster. These charts provide a customizable and scalable way to deploy Elasticsearch with dedicated master, data, and client nodes.

## Prerequisites

Before you begin, ensure you have the following:

- **Kubernetes Cluster**: A running Kubernetes cluster (v1.18+).
- **Helm**: Helm 3 installed and configured.
- **kubectl**: Kubernetes command-line tool installed and configured.
- **Docker**: Docker installed for building images (optional, if you need to customize images).
- **Basic Knowledge**: Understanding of Kubernetes, Docker, containers, images, pods, and Helm charts.

## Installation
### Create a kubernetes namespace for grouping the pods related to Elasticsearch cluster
``` kubectl create ns es7ha ```

### Deploy the helm charts in this new namespace
``` helm install  dkp-es7-ha-master -n  es7ha  elasticsearch-master ```

``` helm install  dkp-es7-ha-client -n  es7ha  elasticsearch-client ```

``` helm install  dkp-es7-ha-data -n  es7ha  elasticsearch-data ```

### Verify that pods are up and in ready state
![image](https://github.com/ssjsk/elasticsearch-7-17-helm/assets/4144131/35a91933-ed82-4f47-9b64-d44212f37320)

### Check nodes, indices and so on within any of the pods 

``` kubectl exec -it elasticsearch-client-0 bash ```

``` curl http://elasticsearch-client:9200/_cat/indices?v ```
![image](https://github.com/ssjsk/elasticsearch-7-17-helm/assets/4144131/36f4405d-7661-41ee-86fa-2e22b7adac86)

### To uninstall helm charts

``` helm uninstall  dkp-es7-ha-data -n  es7ha ```

``` helm uninstall  dkp-es7-ha-master -n  es7ha ```

``` helm uninstall  dkp-es7-ha-client -n  es7ha ```


### Whats next?
You may adjust PVC, allocate CPU/memory etc based on your requirements? These helm charts were pulled from Elasticsearch's official helm chart and are meant to work with official elasticsearch 7.17.21+ images, I haven't tested against ES 8.X.X. This helm chart is not meant for bitnami's ES docker image, bitnami provides its own helm charts and own docker image for the same. Do reach out to me if you need any help or if you see any issue with these parameter settings.
