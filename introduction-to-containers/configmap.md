---
description: Configmap, y no recuerdo.
---

# Configmap

Configmap: para los datos que no sean confidenciales que usaran los contenedores.&#x20;

* Consumido a través de variables de entorno, como líneas de comando,

Para ello debe crearse un manifiesto

```
minikube start
vim configmap.yml
```

En data es la configuración de usemos, variables de entorno siempre en mayúsculas. En esta parte no colocar datos no seguros como contraseñas o urls.

{% code title="configmap.yml" lineNumbers="true" %}
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
    name: nginx-cm
data: 
    NGINX_VERSION: 5.2.1
```
{% endcode %}

Ahora se mapea para que lo use el deployment.&#x20;

```
vim deployment.yml
```

En este se agrega la parte en `env` que sirve para poder referenciar hacia el ConfigMap

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
                env: 
                -   name: NGINX_VERSION
                    valueFrom:
                        configMapKeyRef:
                            name: nginx-cm
                            key: NGINX_VERSION
```
{% endcode %}

Primero se levantan manifiestos, recordar crearlo después de que ya exista deployment, sino marcara error.

```
kubectl apply -f configmap.yml
```

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

Para verificar que existe:

```
kubectl get configmap
```

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

```
kubectl apply -f deployment.yml
kubectl get pods
```

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

<pre><code>kubectl exec <a data-footnote-ref href="#user-content-fn-1">nginx-deployment-xxxxxxxxxxxxx</a> -- env | grep -i nginx
</code></pre>

HOSTNAME=

NGINX\_VERSION=

ERROR aqui

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>





Existen los secrets en Kubernetes para codificar blah blahs, el microservicio se conecte a bovedas o vaults HCP Vault

<mark style="color:yellow;">Importancia boveda: realiza la gestión de contraseñas, llaves en un solo lugar, dado que rota passwords, llaves y tokens.</mark>&#x20;

<figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption><p>Tipos de secrets</p></figcaption></figure>

Ahora se crea un usuario y una contraseña codificado en base 64:

```
echo -n 'admin' | base64
echo -n 'password' | base64
```

Se obtiene token y se guardan ambos datos y ahora se crea un manifiesto para secret:

```
vim secret.yml
```

{% code title="secret.yml" lineNumbers="true" %}
```yaml
apiVersion: v1
kind: secret
metadata:
    name: nginx-secret
type: Opaque
data: 
    username: <TOKEN USERNAME>
    password: <TOKEN CONTRASEÑA>
```
{% endcode %}

Modificamos nuevamente deployment&#x20;

```
vim deployment.yml
```

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
                env: 
                -   name: NGINX_VERSION
                    valueFrom:
                        configMapKeyRef:
                            name: nginx-cm
                            key: NGINX_VERSION
                -   name: USERNAME
                    valueFrom: 
                        secretKeyRef:
                            name: nginx-secret
                            key: username
                -   name: PASSWORD
                    valueFrom:
                        secretKeyRef:
                            name: nginx-secret
                            key: password
```
{% endcode %}

Y sube secret y actualiza el deployment

```
kubectl apply -f secret.yml
kubectl apply -f deployment.yml
```



{% code overflow="wrap" %}
```
kbuctl exec nginx-deployment-xxxxxxxxxxxxx name del pod obtenida anteriormente -- env | grep -i username
```
{% endcode %}



Con esto podemos ver que sin codificación la contraseña y usuario de manera sencilla ya que code64 no es muy seguro por la facilidad s

```
echo -n '<TOKEN USERNAME>' --  code54

echo “texto de ejemplo” | base64?
```

grev busca la cadena de un archivo.



***

```
kubectl deployment nginx-deployment --replicas=1
kubectl get pods
```

Con el siguiente creamos una página web:

{% code overflow="wrap" %}
```
kubectl exec <POD NAME> -- bash -c "echo 'Hello, World' > /usr/share/nginx/html/index.html"
```
{% endcode %}

Verificamos:

```
kubectl exec <POD NAME> -- curl localhost
```



¿Que pasa si se elimina el pod?

```
kubectl delete pod <POD NAME>
```

Al verificar con el pod creado con la eliminación podemos ver que se mantiene la configuración:

```
kubectl exec <POD NAME NUEVO CREADO DE LA ELIINACIÓN> -- curl localhost
```

Ahora debemos modificar de nuevo deployment.yml pero dado que ya tiene información usaremos Visual Studio Code

Volume Mount debe ir a la altura de env y -name del container, volume a la altura de containers

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
                env: 
                -   name: NGINX_VERSION
                    valueFrom:
                        configMapKeyRef:
                            name: nginx-cm
                            key: NGINX_VERSION
                -   name: USERNAME
                    valueFrom: 
                        secretKeyRef:
                            name: nginx-secret
                            key: username
                -   name: PASSWORD
                    valueFrom:
                        secretKeyRef:
                            name: nginx-secret
                            key: password
                volumeMount:
                    -   name: html-volume
                        mountPath: /usr/share/nginx/html
            volumes: 
                -   name: html-volume
                    hostPath: 
                        path: /data
                        type: DirectoryOrCreate
                    
                    
```

MountPath: ruta del contenedor que es



Se levanta:

```
kubectl apply -f deployment.yml
```



{% code overflow="wrap" %}
```
kubectl get pods
kubectl exec <POD NAME> -- bash -c "echo 'Hello world' > /usr/share/nginx/html/index.html"
kubectl exec <POD NAME> -- curl localhost 
ubectl exec <POD NAME> -- cat /usr/chare/nginx/index.html
```
{% endcode %}



```
kubectl delete pod <POD NAME> 
kubectl get pods
kubectl exec <POD NAME> cat /usr/chare/nginx/index.html
```



INGRESS



PROXY: de la red filtra a lo que accedes a internet.&#x20;

PROXY INVERSO: Filtra el tráfico de internet hacia la red propia, por ejemplo: en una red propia como acloud.example.com en donde&#x20;



EN una url&#x20;



<img src="../.gitbook/assets/file.excalidraw (3).svg" alt="" class="gitbook-drawing">

Ingress Controller: Controla el ingreso hacia los clusters.



```
minikube addons enable ingress
minikube addons in
```

Crear un nuevo manifiesto.

```
vim ingress.yml
```

{% code title="ingress.yml" lineNumbers="true" %}
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-nginx
spec:
  ingressClassName: nginx
  rules:
    - host: webapp.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: nginx-service
                port:
                  number: 80
```
{% endcode %}

<mark style="color:blue;">path: /  no importa el contexto siempre toma el mismo contenedor</mark>

<mark style="color:blue;">Tipos de path: Prefix, busca la cadena como expresion regular, otro tipo de path type lo busca exactamente.</mark>&#x20;

```
kubectl apply -f ingress.yml
kubectl apply -f service.yml
kubectl get pods
kubectl get svc
```



```
sudo vim /etc/hosts
```

Aqui se coloca la ip y su dominio, al parecer funciona como DNS

```
192.168.49.2 webapp.example.com
```

Después hacemos la petición

```
curl webapp.example.com
```



Certificado...





Este sabado examen , en inglés.&#x20;

[^1]: name del pod obtenida anteriormente
