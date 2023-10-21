---
description: EXAMEN  Sábado 9 a las 6:00 - 6:30 pm de la tarde, opción múltiple
---

# Minikube

## Instalación de cluster

Descargar kubectl en: [https://kubernetes.io/docs/tasks/tools/](https://kubernetes.io/docs/tasks/tools/)

Seleccionar la arquitectura de la CPU, en este caso para x86 64

{% code overflow="wrap" %}
```
 curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Validar el binario, para comprobar que sea el software deseado.

{% code overflow="wrap" %}
```
 curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

3. Instala a través del usuario root y su mismo grupo, le da el permiso 755, y marca la ubicación.

{% code overflow="wrap" %}
```
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
{% endcode %}

Una vez con esto se ha terminado de instalar&#x20;

```
rm kubectl
kubectl version --client
```

Y con esto se muestra, y la versión del cliente debe de coincidir.

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

## Instalación de minikube

Descarga en: [https://minikube.sigs.k8s.io/docs/start/](https://minikube.sigs.k8s.io/docs/start/)

Minikube emula un cluster de kubernetes en tu local.&#x20;

Para empezar a instalar, uno para bajar el binario y el otro para instalar.

{% code overflow="wrap" %}
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

### ¿Cómo crear el cluster de minikube?

Generalmente solo se utiliza start, con los parámetros se limita el uso de recursos

```
minikube start
minikube start --cpus 2 --memory 2048
```

Pods, contenedores, basados en imagenes que se descargan, levantar los pods y contenedores, y simular que es un cluster

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

### Configuraciones para autocompletar ciertas funciones.&#x20;

```
sudo dnf -y install bash-completion
```

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

.bashrc contiene lo necesario para cargar variables de entorno, por ello lo vamos a modificar.

{% code overflow="wrap" %}
```
echo 'source <(kubectl completion bash)' >> ~/.bashrc
```
{% endcode %}

<mark style="color:red;">Tener cuidado con > porque reemplaza.</mark>

```
echo 'alias k=kubectl' >> ~/.bashrc
```

{% code overflow="wrap" %}
```
echo 'complete -o default -F __start_kubectl k' >> ~/.bashrc
```
{% endcode %}

Salir y volver a entrar en la terminal osar el comando para volver a cargar el perfil.

```
source ~/.bashrc
```

Revisamos el contenido de bashrc&#x20;

```
cat ~/.bashrc
```

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Para ver los nodos asociados al cluster:

<pre><code><strong>kubectl get nodes
</strong></code></pre>

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

PODS: Puede tener uno o mas contenedores asociados, esencialmente solo contiene a un contenedor.&#x20;

Creación de pods, para ello generalmente se usan manifiestos.

{% code overflow="wrap" %}
```
kubectl run frontend --image=nginx:latest
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

El pod solo contiene un contendedor con iamgen nginx&#x20;

Para poder observar el pod:&#x20;

```
kubectl get pod 
```

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

En Kubernetes: si un contenedor se muere intenta revivir: <mark style="color:blue;">self-healing</mark>. En docker si se muere ya no revive

Manifiestos: creación de objetos dentro del cluster de kubernetes, para ello se usa un archivo .yaml&#x20;

Objeto deployment: que se va usar en el pod y el numero de replicas del pod. Ayuda a la disponibilidad, balanceador de carga para que al iniciar al pod se da de manera igual en todas las replicas.

Para el deployment se puede usar:&#x20;

```
vim deployment.yml
vim deployment.yaml
```

Ahora colocamos lo siguiente, donde la Sintaxis es -> Llave: Valor

{% code title="deployment.yml" lineNumbers="true" %}
```yaml
apiVersion: apps/v1
kind: Deployment
metadata: 
    name: nginx-deployment
spec: 
    replicas: 3
    selector: 
        matchLabels: 
            app: nginx
    template:
        metadata:
            labels: 
                app: nginx
        spec: 
            containers: 
            -   name: nginx
                image: nginx:latest
                ports: 
                -  containerPort: 80
```
{% endcode %}

matchLabels nos ayudará a identificar los pods. Selector para que los servicios detecten de forma correcta el pod, deben ser únicas por objeto o puede causar problemas por las etiquetas.

El guión en name es para indicar listas.

Para aplicar el manifiesto se usa:

```
kubectl apply -f deployment.yml
```

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Para ver deployment:

```
kubectl get deployment
```

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

```
kubectl get pods
```

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

Si se mata alguno de los pods creados de las replicar, Kubernetes lo revive :hushed:

Escalar arriba o abajo los deployments, para ello:

{% code overflow="wrap" %}
```
kubectl scale deployment nginx-deployment --replicas 5
kubectl get pods
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

Si son menos de las que se tenían Kubernetes mata los demás:

{% code overflow="wrap" %}
```
kubectl scale deployment nginx-deployment --replicas 1
kubectl get pods
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

Limite de pods por nodo, 100

#### Services en Kubernetes

3 tipos de servicios que se pueden colocar en deployment para acceeder a ellos:&#x20;

* ClusterIP genera una IP interna en Kubernetes y nombre de dominio, no puede ser accedido desde fuera del cluster. <mark style="color:yellow;">(NO EXPUESTOS)</mark>
* NodePort: Crea Port forwading, Identifica un puerto del container y mapea hacia el nodo donde se ejecuta, casi no se usa.&#x20;
* LoadBalancer: crea un balanceador virtual o físico con una IP publica que se puede adjnutar a un nombre de dominio de internet, solo para POD que puedan sr expuestos. <mark style="color:yellow;">(EXPUESTOS)</mark>

```
kubectl run backend --image=nginx
kubectl get pods
```

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Dado que no hay servicio no se puede hacer porque nadie le habla ya que esta aislado. :cry:

```
kubectl exec frontend curl -- backend
```

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

Se crea un manifiesto

```
vim service.yml
```

En este manifiesto

{% code lineNumbers="true" %}
```yaml
apiVersion: v1
kind: Service
metadata: 
    name: nginx-service
spec: 
    selector: 
        app: nginx
    ports: 
    -   protocol: TCP
        port: 80
        targetPort: 80
    type: ClusterIP
    
```
{% endcode %}

Las etiquetas deben ser iguales al Deployment al que deba conectarse

Se realiza igual que en Deployment.

```
kubectl apply -f service.yml
```

```
kubectl get service
```

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

```
kubectl exec frontend -- curl nginx-service
```

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

Si se hace hacia el backend lo deniega porque no esta expuesto

```
kubectl exec frontend -- curl backend
```



etchost, para simular dns.&#x20;



Modificamos el service.yml para NodePort:

```yaml
apiVersion: v1
kind: Service
metadata: 
    name: nginx-service
spec: 
    selector: 
        app: nginx
    ports: 
    -   protocol: TCP
        port: 80
        targetPort: 80
        nodePort: 30000
    type: NodePort
```

Con esto ahora tendremos el servicio configurado

```
kubectl apply -f service.yml
kubectl get svc
```

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

```
kubectl exec frontend -- curl nginx-service
```

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Se identifica la ip, que generalmente es la misma `192.168.49.2` en  mi caso es 10.0.2.15

```
minikube ip
```

Se realiza un curl hacia la IP

```
curl 192.168.49.2:30000
```



Por último para Load Balancer:

Se usa para la lista de plugins preconfigurados que se pueden usar

```
minikube addons list
```

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

El que nos interesa es metallb, y debemos habilitarlo

```
minikube addons enable metallb
```

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

Se verifica que este habilitada con la lista de addons, que son los que extienden la&#x20;

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

Configurar los Load Balancer

```
ip a
```

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>



```
vim metallb-configmap.yml
```



```yaml
apiVersion: v1
kind: ConfigMap
metadata: 
    namespace: metallb-system
    name: config
data: 
    config: |
        address-pool:
        -   name: default
            protocol: layer
            addresses:
            -   192.168.49.10 - 192.168.49.20

```

```
kubectl apply -f metallb-configmap.yml
```

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

```
vim service.yml
```

{% code title="service.yml" lineNumbers="true" %}
```yaml
apiVersion: v1
kind: Service
metadata: 
    name: nginx-service
spec: 
    selector: 
        app: nginx
    ports: 
    -   protocol: TCP
        port: 80
        targetPort: 80
    type: LoadBalancer
```
{% endcode %}

Se verifica que cambie el servicio

```
kubectl apply -f service.yml
kubectl get svc
```

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

```
minikube ip
```









rm-rf/ ls
