# 💼 Micro front ends

Para el examen son 30 preguntas, 10 por sección, 45 minutos para contestar, aprenderse comandos y la estructura de manifiestos. 5:45 pm sábado.&#x20;

* Control de versiones
* Contenedores&#x20;
* Kubernetes.



## ¿Qué es?

Micro FrontEnd -> es un término reciente (2016), creado para dividir el Front End en pequeñas partes (responsabilidades) con diferentes objetos que podrán ser utilizados en otras partes para reutilizar código.

Es importante saber cuándo es conveniente utilizar una u otra tecnología, puede que ciertos proyectos requieran de monolitos en lugar de microservicios. &#x20;



### Ventajas.&#x20;

* Independent Deployment&#x20;
  * Despliegues independientes, se van a poder mantener en separado. Al existir un cambio en nuestra página web, solo se dará el cambio a la parte en la cual se hizo el cambio.
* Scalability
  * Se puede tener alta redundancia por componente, haciéndolo altamente escalabre y altamente disponibles.
* Freedom
  * Todos los microfront end pueden trabajar juntos a pesar de ser diferentes lenguajes y frameworks, esto es altamente convertible?
* Isolated
  * Aislamiento de las fallas, al existir falla en algún microfrontend no afectara a los demas servicios.

### Desventajas

* Complexity
  * Complejidad completamente mayor a tener un monolito, porque la comunicación se vuelve mas compleja. Para proyectos muy pequeños no es recomendado usar muchos micro front ends.
* Performance
  * Se necesita tener un buen nivel de programación.
* Code Duplication
  * Si no se tiene mucha experiencia con micro front ends es posible que dupliquemos código.
* Coordination team
  * Se ocupa bastante coordinación con los equipos porque es probable que ocupen comunicación entre los servicios de cada uno.



## REACT

Es un framework de JavaScript, creado por FaceBook en 2011 para generar respuestas en tiempo real. Tiene una curva de aprendizaje sencilla; esto lo logra haciendo que las peticiones lleguen al cliente sin tener que refrescar la página. Las dos tecnologías con las que funciona mjor: JSX y TSX

NOTA: Solo utilizaremos JavaScript.&#x20;

Node JS para instalar -> npx o yarn

Instalación de Node JS

Para descargar Node JS: [https://nodejs.org/en](https://nodejs.org/en) y escargar la Long Time Service LTSm en otras descargas usar click derecho para copiar el link de la version segun la arquitectura de la computadora.

Podemos crear aplicaciones responsivas que se desplegarán de diferente forma de acuerdo al tipo de pantalla.&#x20;



Creación de la carpeta nodejs donde se descomprimirá/descargara

```
sudo mkdir -p /usr/local/lib/nodejs
```

Descargar y ponerlo en el home para que pueda encontrar le archivo y descomprimirlo con el siguiente comando\_

```
sudo tar -xJvf  node-v-xxxxx.tar.xz -C /usr/local/lib/nodejs
```

x descomprimir

v para que diga todo lo que va a descomprimir.



con tab buscamos la dirección

<pre><code><strong>sudo ls -l /usr/local/lib/nodejs/node-v18.17.1-linux-x64
</strong></code></pre>

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

Configurar perfil

```
vim ~/.bashrc
```

Al final agregar:

```
export PATH="/usr/local/lib/nodejs/node-v18.17.1-linux-x64.tar.xz:$PATH"
```

Guia de ayuda: [https://phoenixnap.com/kb/linux-add-to-path](https://phoenixnap.com/kb/linux-add-to-path)

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>



```
source ~/.bashrc
```



```
node -v
npm -v
npx -v
```

Debian -> [https://phoenixnap.com/kb/debian-install-nodejs](https://phoenixnap.com/kb/debian-install-nodejs)

![](<../.gitbook/assets/image (71).png>)

Escribir en la terminal de vs code

```
npx create-react-app click-counter
```

{% code title="source -> Counter.js" lineNumbers="true" %}
```javascript


```
{% endcode %}

Terminal:

```
npm start 
```

Usar cualquier de las dos local o en la red.&#x20;

{% code title="source --- Counter.js" lineNumbers="true" %}
```javascript
import React, { Component } from 'react';

class Counter extends Component {
    constructor() {
        super();
        this.state = {
            counter: 0,
        }
    };

    incrementCounter = () => {
        this.setState({ counter: this.state.counter + 1});
    }

    render() {
        return(
            <div>
                <h1>Click Counter</h1>
                <p>Counter Value: {this.state.counter}</p>
                <button onClick={this.incrementCounter}>Increment</button>
            </div>
        );
    }
}

export default Counter
```
{% endcode %}

{% code title="App.js " lineNumbers="true" %}
```javascript
import React from 'react';
import './App.css';
import Counter from './Counter';

function App() {
  return (
    <div className='App'>
      <Counter />
    </div>
  );
}

export default App;
```
{% endcode %}

