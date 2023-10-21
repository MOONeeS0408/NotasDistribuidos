---
description: 'Documentación de Kubernetes: https://kubernetes.io/docs/home/'
---

# Introduction to Kubernetes

## What is Kubernetes?

* Is an opensource plataform for  a container orchestration
* Provides a robust solution for managing containerized workflows
* Is a powerfull system that allows managing containerized applications and services.

Kubernetes es una tecnología basada en nube que permite gestionar, escalar y mantener contenedores.&#x20;

Google fue el primer que desarrollo en sus primeras fases y después pasó a Cloud Native Computing Foundation (CNCF). Ellos se encargan dce las nuevas certificaciones.

<img src="../.gitbook/assets/file.excalidraw (1).svg" alt="" class="gitbook-drawing">



### Control Plane&#x20;

* kube-apiserve: End point para gestionar el cloudster. kubectl gestionar archivos de kubernetes, como login y no se que mas alv :joy: :cry:

kublconfig

* etcd: base de datos tipo llave valor de alta disponibilidad para guardar la configuración.
* Kube-scheduler: es importante para el control plane, describe en que nodo se ejcutan los contenedores, de otra manera Kubernetes no sabe en que conteendor se guarda.&#x20;
  * Capacidad de los nodos: determina cual de ellos es mejor.
* kube-controller-manager / cloud-controller-manager : Controla la nube en la que se ejecuta.&#x20;
  * Node controller
  * Job controller



### Nodes (antes workers)

* Kubelet: uno de los mas importantes, permite comunicación entre todos los nodos todos exponen un endpoint, y usan el protocolo de Kubelet.&#x20;
* Kube-proxy: para conexiones fuera del cloudster.
* Container runtime: Puede ser Docker, CRI-O o Containerd

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>





<img src="../.gitbook/assets/file.excalidraw (2).svg" alt="" class="gitbook-drawing">

La próxima clase es MINIKUBE

Para los cursos se recomienda: [https://www.w3schools.com](https://www.w3schools.com)



Manage Kubernetes environment and networking
