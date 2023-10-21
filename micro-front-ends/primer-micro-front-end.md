# 🤖 Primer micro front end

Proyecto:

Estructura recomendada para el proyecto, porque es lo que suele usar las personas en front end

<pre><code><strong>|--node modules
</strong><strong>|--public
</strong>|    |--index.html
|--src
|    |--app/
|        |--index.js
|        |--App.js
|    |--components
|    |--constants
|    |--contexts
|    |--features
|        |--autentication
|            |--auth-button.jsx
|            |--auth-form.jsx
|            |--index.jsx
|            |--slice.jsx
|            |--utils.jsx
|    |--hooks
|    |--layouts
|    |--pages/routes
|    |--services
|    |--styles
|    |--types
|    |--utils
|    |--store.ts
|--.gitignore
|--package-lock.json
|--package.json
|--README.md
</code></pre>

Las API se crearán con Python.



### Creación de componentes

Componentes: parte de interfaz de usuario, lógica y apariencia propia, puede ser desde un botón hasta un página completa.



En la terminal de vs colocar:

```
npx create-mf-app
```

Con ello configurar todo lo que queremos para nuestra aplicación.

```javascript
Pick the name of your app: home
Project Type: Application
Port Number: 3000
Framework: react
LAnguage: Javascript
CSS: CSS
```

Inicializamos el proyecto siguiendo los pasos:

```
cd home/
npm install
```

Con ello se crean la carpeta node\_modules y modificar segun estructura.

Para checar la aplicación con&#x20;

```
npm start
```

Con ello te permite ver en editor o en browser



Alla alguna de home crear una nueva carpeta public que va a contener el index.html

Para corregir el error de que deje de funcionar, para ello en el archivo webpack-config.js al final linea 68 colocaba en donde se encontraba el archivo y cambiar la ruta `./src/index.html` por `./home/index.html`



Ahora se reiniciar de nuevo `npm start`

Crear carpetas donde <mark style="color:blue;">src</mark> -> <mark style="color:blue;">app</mark> -> <mark style="color:yellow;">app.jsx</mark> y <mark style="color:blue;">styles</mark> -> <mark style="color:yellow;">index.js</mark>

```
|--src
|    |--app/
|        |--App.jsx
|    |--styles
|    |    |--index.js
```

En `webserver-app`  agregar un línea entre `devServer` y `module`, esto modifica la ruta utilizada:

```javascript
entry: "./src/app/index.js",
```

En `app.js` modificar la ruta donde se encuentran y que se modificaron, línea  4:

```javascript
import "../styles/index.css";
```

Crear carpeta para componentes en donde se guardaran el archivo `header.jsx` y `footer.jsx` : &#x20;

```
|--src
|    |--app/
|        |--App.jsx
|    |--styles
|    |    |--index.js
|    |--components
|        |--header.jsx
|        |--footer.jsx
```

{% code title="header.jsx" lineNumbers="true" %}
```javascript
import React from "react"

export default function () {
    return(
        <div>
            Micro Frontend Header
        </div>
    );
}
```
{% endcode %}

{% code title="Footer.jsx" lineNumbers="true" %}
```javascript
import React from "react"

export default function () {
    return(
        <div>
            Micro Frontend Footer
        </div>
    );
}
```
{% endcode %}

Para que puedan visualizarse deberán importarse en `apps.js`, línea 4:

```javascript
import Header from './Components/Header'
import Footer from './Components/Footer'
```

En el browser podemos dar click derecho e **inspeccionar elemento** -> en la consola se mostrará un warning por como react expone el componente. Para arreglar esto tenemos que modificar la línea 2  (de app?):

```javascript
import {createRoot} from "react-dom"
```

y después agregar al final:

```javascript
const root = createRoot(document.getElementBydl('app'))
root.render(<App />)
```

#### Código completo

{% code title="app.js" lineNumbers="true" %}
```javascript
import React from 'react'
import {createRoot} from "react-dom/client"
import "../styles/index.css"
import Header from './Components/Header'
import Footer from './Components/Footer'

const App = () => {
    <div>
        <Header/>
        <div>
            Home Page Content
        </div>
        <Footer />
    </div>
}

const root = createRoot(document.getElementById('app'))
root.render(<App />)
```
{% endcode %}

### Props

Una propiedad es aquella que permite alterar el aspecto de algun componente, todas las propiedad html permite usarse en react, la estructura de una propiedad puede ser como la siguiente:

```javascript
<img alt='' src = ' de donde obtiene la img' width='' weight=''>
```

En <mark style="color:blue;">styles</mark> -> <mark style="color:yellow;">index.css</mark> colocar al final:

{% code title="index.css" lineNumbers="true" %}
```css
.site-container {
    background-color: #015301;
    color: white;
    padding: 20 px;
    text-align: center;
    font-size: 24 px;
}
```
{% endcode %}

Modificar header y footer para agregarlo:

{% code title="Header.jsx" lineNumbers="true" %}
```javascript
import React from "react"

export default function () {
    return(
        <div className="site-container">
            Micro Frontend Header
        </div>
    );
}
```
{% endcode %}

{% code title="Footer.jsx" lineNumbers="true" %}
```javascript
import React from "react"

export default function () {
    return(
        <div className="site-container">
            Micro Frontend Footer
        </div>
    );
}
```
{% endcode %}



Estados: es un componente que permite ser dinámicos y ... e cinlsuo responder a no recuerdo TT



Seguir agregando estilo al archivo quedando de la siguiente manera:

{% code title="index.css" lineNumbers="true" %}
```css
Aqui
van
las 
lineas
por 
default





.site-container {
    background-color: #015301;
    color: white;
    padding: 20 px;
    text-align: center;
    font-size: 24 px;
}

.Counter{
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 20 px;
}

.Counter h1 {
    font-size: 4rem;
    margin-top: 20px;
}

.Counter button {
    font-size: 2rem;
    padding: 10px 20px;
    background-color: aliceblue;
    color: white;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.3s;
}

.Counter button:hover {
    background-color: blueviolet;
}
```
{% endcode %}

Se crea otro nuevo componente: `counter.jsx`

```javascript
import {useState} from 'react'

export default function Counter {
    const [number, setNumber] = useState(0);
    return (
        <div className="Counter">
            <h1>[number]</h1>
            <button onClick={() => {
                setNumber[number + }
            }>
            </button>

        </div>
    );
}
```

REvisar lo del button

<mark style="color:red;">AQUI EMPIEZA UN CAOS</mark>



Modificar counter en lugar de content en app.js

Module federation, comportir todo lo de micro front end a los demas.&#x20;







En terminal de vs code&#x20;

```
npx create-mf-app
```

```
name: about
Type: Application
Port number: 3001
Framework: react
LAnguage: Javascript
CSS: CSS
```

Mismos pasos

```
cd about/
npm install
npm start
```



webconfig





.public/



entry: "./src/app/index.js"



reinicar&#x20;



impo



Hacer lo mismo que lo anterior, organizar en carpetas y cambiar rutas





En webpack-config buscar plugins -> ModuleFederation -> exposes colocar:

```javascript
"./Header": "./src/components/Header.jsx",
 "./Footer": "./src/components/Footer.jsx", 
"./styles": "./src/styles/index.css" 
```

Agregar:  `remoteentry.js` y verificar que la url entra&#x20;



En about entrar a  plugins -> ModuleFederation -> remote

<mark style="color:yellow;">NOTA: quien los manda es exposes, quien lo recibe es remote.</mark>

Colocar en remote:&#x20;

```
home: "home@http://localhost:3000/remoteEntry.js"
```

En about app importar y se agregan en  App quedando completo:

```javascript
import React from 'react'
import {createRoot} from "react-dom/client"
import "../styles/index.css"

import Avatar from '../components/Counter'
import Header from './home/Header'
import Footer from './home/Footer'
import styles from './home/styles'

const App = () => {
    <div className="container">
        <Header/>
        <Avatar/>
        <Footer/>
    </div>
}

const root = createRoot(document.getElementById('app'))
root.render(<App />)
```



Si se deja de correr el que contiene Header y Footer no será posible observarlo.

