# Microservicios

Monolito: cuando se trabaja en equipo se veía riesgo debido a las funcionalidades, ejemplo: si una persona A trabaja con una funcionalidad X y una persona B trabaja con una funcionalidad Y, y ambas funcionalidades trabajan con el mismo modulo es posible que existan conflictos entre ellos.



SOA

separa el monolito por servicios determinados. Pero de un servicio completo, desde la interfaz grafica hasta el repo.&#x20;

ser agnostico,  (?



En un 60% esta basado en SOA



nada de lo que existe alrededor.&#x20;

El micro servicio tiene la ventaja de generar un servicio independiente de una tecnología que no sea la misma.&#x20;

Tomar en cuenta el hardware, permite usar muchas tecnologías, pero el mantenimiento se vuelve complicado, generalmente usado para tecnologías de nube.&#x20;



API: expone el end point, permitiendo la interacción con un sistema externo.

APIs Restful: C.R.U.D ? peticiones tipo https, se mandan al API, ejemplo Postman, Insomnia.&#x20;

¿Que peticiones maneja Restful?

POST - creación

GET - obtener del API

PUT - Reemplazar y si no lo encuentra lo crea

DELETE

PATCH

UPDATE?&#x20;



Crear un Flask framework? para usar react, no usar Django?





Flask ayudara a crear estos, microframework. peticiones seguras a traves de https.&#x20;





Proimer microservicio.

Instalación de Python.

{% embed url="https://www.python.org/downloads/" %}



Download Gzipped source tarball y usar `wget [link]`

```
wget https://www.python.org/ftp/python/3.12.0/Python-3.12.0.tgz 
```



```
python --version
```

```
sudo dnf -y groupinstall 'Development Tools'
```

descargar plugin de python para ayudar.



DEscomprimiendo&#x20;

```
tar -xvf Python... 3.12.0.tgz
```

x extract, v - todo, f file &#x20;

```
cd Python-3.12.0
```

```
./config --enable-optimizations
```





```
sudo make install
```



```
python --version
python3.12 --version
```



```
ls -l
sudo rm -rf * PYthon-3.12.0.*
ls 
```



```
mkdir first_api
cd first_api/
python3.12 -m venv venv
```

Creacion entorno virtual

Activar&#x20;

```
source venv/bin/activate
```

Desactivar

```
deactivate
```





Actualizar

```
pip3 install --upgrade pip
```

Pip lo hace solo con el usuario actual.&#x20;



Instalar flask, 3.0.0

```
pip3 install flask 

```



Para verficiar

```
pip3 list
deactivate
pip3 list


```

S confirma no alterar el SO

source  venv/bin/activate

generar un archivo en first\_api



En el interprete seleccionar el qu viene del entorno virtual que es venv/bin/python3.12





{% code title="app.py" overflow="wrap" lineNumbers="true" %}
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')

def hello_world():
    return 'Hello World!'
    
if  __name__ == '__main__':
    app.run()

```
{% endcode %}



flask run  o bien python \[nombrearchivo]

python app.py

























