# ▶ Props, Stats y CustomEvents

Grid: ayudan a tener una mejor vista de la aplicación.

Ejemplo:&#x20;

md = 8 significa que solo hacia abajo son 8, y xs solo mostrará una columna

## Comunicación entre micro front ends

Formas para comunicar microfront ends, y también para comunicar .. entre sí. Los primeros dos son los que generalmente se usan, los otros tres son mas complicadas pero sirven para aplicaciones más complejas.

1. Props y States
2. CustomEvents
3. Redux
4. Message Broker (Rabbit MQ)
5. API GW

Ejemplo, un microfront end de un botón redirecciona a otro micro front end con el que se comunica.



Facil observar el comportamiento con e.stados, porque se pude ver las propiedad que se llama, si son muchos micro se vuelve complejo.&#x20;

Props y States es una comunicación unidireccional,&#x20;





### Props and States





Creción app1



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



{% code overflow="wrap" %}
```
npm install @mui/material @mui/icons-material @emotion/react @emotion/styled
```
{% endcode %}

Eliminamos index.css

movemos l index al public



Configurar webpack-config

template, Entry y quitar el import del css





Crear carpeta component,&#x20;

data puede ser cualquir string, que se va a mostrar en el componente.

Para app2

{% code title="App.js" overflow="wrap" lineNumbers="true" %}
```javascript
import React from 'react'
import {createRoot} from "react-dom/client";
import { Box, Container, Typography } from '@mui/material'
import SharedComponent from 'app1/SharedComponent'

const App = () => {
    const {datafrontApp2} =useState('Hello from Appp1')
   return(
    <Container>
    <Box textAlign='center' my={4}>
        <Typography variant='h3' gutterBottom  >
            Micro front ends communication using Props
        </Typography>
        <SharedComponent data= { data} /> 

    </Box>
    </Container>
   );
};

const root = createRoot(document.getElementById('app'));
root.render(<App />)
```
{% endcode %}

Checar linea 14 con Shared component.



Ahora para exponer el componente ir a webpack-config ir a pluigns y colocar en module federation



```
expose: [
    "./SharedComponent": "/src/"

]?
```

...&#x20;

REvisar el manifiesto que aparece con el etntry en el buscador



Creamos segunda app: SharedComponent

{% code title="ShaderComponent.jsx" overflow="wrap" lineNumbers="true" %}
```javascript
import { Box, Paper } from '@mui/material'
import ShareIcon from '@mui/icons-material/Share'
import React from 'react'

function SharedComponent({ data }) {
    return(
        <Paper elevation={3} styled={{padding: '20px', textAlign: 'center', background: 'F5F5F5'}} >
            <Box>
                <ShareIcon fontSize= 'large' color='primary'/>
                <Typography variant='h5' component='div'>
                    Shared Component
                </Typography>
               <Typography variant='body1' paragraph>
                    <strong> data from App1: </strong> {data}
                </Typography>
            </Box>
        </Paper>
    );
};

export default SharedComponent;
```
{% endcode %}



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





{% code overflow="wrap" %}
```
npm install @mui/material @mui/icons-material @emotion/react @emotion/styled
```
{% endcode %}

Eliminamos index.css



En la config, public, entry,&#x20;



debe tener el mismo nombre que la app

```javascript
remote {
    app1: "pp1@http://localhost:3000/remoteEntry.js"

}

```







### CUSTOM EVENT



custom events es mas engorroso, porque puedes no saber de donde viene o como aplicarlo

Eventos personalizados no son recomendados para app pequeñas

En terminal

npx create-mf app

custom-event-app





Componente

{% code title="custom-event-msg.jsx" %}
```javascript
import React from 'react';
import { Box, Button } from '@mui/material'
import ShareIcon from '@mui/material/Share'

export default function customEventMsg() {
    const handleClick =() => {
        const custonEvent = new CustomEvent('customEventMsg', {
            detail: {message: 'Hello from custom-event-app' }
        });
        window.dispatchEvent(customEvent);

    };

    return(
        <Box>
            <Button
                variant= 'contained'
                color = 'success'
                onClick={handleClick}
                starticon ={<ShareIcon fontSize = 'large'/>}
            >
                Share event
            </Button>
        </Box>
    )
}
```
{% endcode %}

Para gestionar eventos personalizados no recuerdo pero son 3 partes:&#x20;

Dispatch, algo mas y listener.&#x20;



El contained event tiene rell



En modo federation n exposes

```javascript
'./CustomEventMsg' = "./src/components/customEventMsg.jsx" 
```

reinicio de server con start y revisamos manifiesto.



Nuevo micro front end, aplicación principal: _**main-app**_

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



{% code overflow="wrap" %}
```
npm install @mui/material @mui/icons-material @emotion/react @emotion/styled
```
{% endcode %}

Eliminamos index.css



en plugins  -> remote



{% code overflow="wrap" %}
```
custom_event_app: "custom_event_app@http://localhost:30000/remoteEntry.js"
```
{% endcode %}



Si el nombre de la aplicación como en este caso estan con guions medios deberá colocarse aquí con guiones bajos.

Esto lo podemos revisar en el manifiesto con las variable que aparece.













dispath setea, ahora usamos el evento personalidad de los eventos con los que cuenta React.

Base para el siguinete:

```javascript
import React from 'react';
import {createRoot} from "react-dom/client";
import { Box, Container, Typography } from '@mui/material';
import SharedComponent from 'app1/SharedComponents';

const App = () => {
    
};

const root = createRoot(document.getElementById('app'));
root.render(<App />)
```







```
```





Para la siguiente clase vamos a terminar el códiog de esto y ruteos y idk avanzados.&#x20;









Use state lo modifica, el estado, en este caos un cadna vacia

use effecta permite uso del evento personalizado





Dispatcher

Listener; verifica que tenga un detalle y un mensaje





Listener prmitir volver y quitar o entendí (?





No se recomienda usar eventos personalizados





Comunicación bidireccional lo qu puede complicar la comunicaci{on con loops, y&#x20;

