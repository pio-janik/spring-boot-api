# spring-boot-api

The repository contains three different directories:
* The argocd directory contains manifests that configure clusters.
* The config directory contains manifest files with configurations for the Helm chart.
* The helm-chart directory contains the chart.

## Requirements
The project assumes that we have a configured cluster with ArgoCD installed.
To install resources in the cluster, you need to run the command kubectl apply -f argocd.

## Assumptions
* ArgoCD is based on manifest YAML files, so its installation and configuration probably can be automated.
* ArgoCD sources could be pointed to a tag version rather than a branch name; [SemVer](https://semver.org/) could be used.
* One cluster was used to complete the task and is divided logically. In a real-world scenario, ArgoCD could be installed in a specific cluster, with two other clusters for specific environments.
* In the deployment object, we can define affinity and anti-affinity to distribute pods across distinct nodes.
* We can specify nodeSelector to assign the deployment object to the proper node pool.
* Ingress does not work properly:
    * The Ingress class needs to be defined, and Ingress needs an Ingress controller (optional) - [nginx ingress controller](https://kubernetes.github.io/ingress-nginx/)
    * To export the host name to the DNS zone, we can use External DNS to sync - [External DNS](https://github.com/kubernetes-sigs/external-dns)
