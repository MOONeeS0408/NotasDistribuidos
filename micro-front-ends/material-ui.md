# 🧠 Material UI

Revisión de ejercicio pasado, modificaciones que se realizaron.

Bootstrap, herramienta que te da las clases

MaterialUI te da ya los elementos bien definidos.&#x20;



Pagína de Material UI: [https://mui.com](https://mui.com)

Documentación que usaremos MAterial UI Core: [https://mui.com/material-ui/getting-started/](https://mui.com/material-ui/getting-started/)



Borrar lo que se tenia&#x20;

```
cd microfrontends/ 
rm -rf .
npx create-mf-app
```



```
cd home/
npm install 
```

Configurar

```java
Pick the name of your app: home
Project Type: Application
Port Number: 3000
Framework: react
LAnguage: Javascript
CSS: CSS
```

Instalar

```
npm install @mui/material @emotion/react @emotion/styled
```

Generar el public, App y styles y volver a generar la estructura que conocemos.

Recordando: public, Entry, se puede eliminar css

```
npm start
```

No tenemos estilos pero ya esta levantado.

En la documentación -> Components, es posible ver como realizar cada componente de una interfaz gráfica



{% code title="basic-app-bar.jsx" overflow="wrap" lineNumbers="true" %}
```javascript
import { AppBar, ToolBar, Typography, Button } from '@mui/material';
import  MenuIcon  from '@mui/icons-material/Menu';


export default function BasicAppBar(){
    return (
        <AppBar position='static'>
            <ToolBar>
                <IconButton
                    size='large'
                    edge='start'
                    color='inherit' //de forma automatica cambia el color que mejor contrasta
                    aria-label='menu'
                    sx={{mr: 2 }}  //definicion de un estilo personalizado    
                >
                    <MenuIcon>

                    </MenuIcon>
                </IconButton>
                <Typography variant='h6' component='div' sx = { flexGrow = 1}
                //variant cambia el estilo a un componente de HTML como h6
                //div es un contenedor
                //mantenerlo en esa forma
                >
                    News
                </Typography>
                <Button color='inherit' Login>
                

                </Button>
            </ToolBar>
        </AppBar>
    )
}

```
{% endcode %}



{% code title="basic-app-grid.jsx" overflow="wrap" lineNumbers="true" %}
```javascript
import theme from '../styles/themes';

export default function BasicAppGrid() {
    return(
        <Grid container sx ={ {height: '100%'}}> 
            <Grid item xs= {8} sx= {{padding: 0.5}}>
                <Paper sx={ theme.customStyles.Paper }>
                    <Typography variant='h6'>
                        xs=8
                    </Typography>
                    <Typography variant='body1'>
                        content
                    </Typography>
                </Paper>
            </Grid>
            <Grid item xs= {4} sx= {{padding:0.5}}>
                <Paper sx={ theme.customStyles.Paper }>
                    <Typography variant='h6'>
                        xs=8
                    </Typography>
                    <Typography variant='body1'>
                        content
                    </Typography>
                </Paper>
            </Grid>
                <Grid item xs= {8} sx= {{padding: 0.5}}>
                <Paper sx={ theme.customStyles.Paper }>
                    <Typography variant='h6'>
                        xs=8
                    </Typography>
                    <Typography variant='body1'>
                        content
                    </Typography>
                </Paper>
            </Grid>    
            <Grid item xs= {8} sx= {{padding: 0.5}}>
                <Paper sx={ theme.customStyles.Paper }>
                    <Typography variant='h6'>
                        xs=8
                    </Typography>
                    <Typography variant='body1'>
                        content
                    </Typography>
                </Paper>
            </Grid>
        </Grid>
        
    );

}
```
{% endcode %}





{% code title="styles -> themes.jsx" overflow="wrap" lineNumbers="true" %}
```javascript
import { createTheme } from '@mui/material/styles';

const theme = createTheme({
    palette:  {//definir color primary and secondary
        primary: {
            main: '#01587C'
        }, 
        secondary: {
            main: '#0198AA'
        }, 
    },
    Typography: {
        fontFamily: 'Roboto',
        h6: {
            fontSize: '1,5rem',
            fontWeight: 600
        }, 
        body1: {
            fontSize: '1rem'
        }
    }, 
    customStyles: {
        paper: {
            padding: 2,
            border: '1px solid #0q98AA', 
            height: '100%'
        }

    }
});

export default 'theme'
```
{% endcode %}



{% code title="app.jsx" overflow="wrap" lineNumbers="true" %}
```javascript
import React from 'react';
import {createRoot} from "react-dom/client";
import BasicAppBar from './components/basic-app-bar';
import theme from '../styles/themes';
import { Box, ThemeProvider} from '@muimaterial';
import BasicAppGrid from './components/basic-app-grid';

const App = () => {
    <ThemeProvider theme={theme}>
        <Box className= 'App' sx={{ display: 'flex', flexDirection: 'column', height: '100hv'}}>
            <BasicAppBar/>
            <Box sx= {{flex: 1, overflow:'auto',nargin: 1, height:'100hv'}}>
                <BasicAppGrid/>
            </Box>
        </Box>
    </ThemeProvider>
}

const root = createRoot(document.getElementById('app'))
root.render(<App />)
```
{% endcode %}



Necesitamos instalar los iconos&#x20;

```
npm install @mui/icons-material
```



Modificando, es posible usar lo de cs con UI





Grid ayuda a poder colocar, definir en que filas y columnas.  12x12

Al crearlo, no s ve al 100%

Visualizar distribución.&#x20;

```
```



```
```



Usando, xs sabe que todas las que son ascendentes

md solo para md y xl

Tamaños: xs xm mx y xl



ára otras no hay definición





Proyectos ideas:

Chat response

Visualizar si la prsona esta conectada,&#x20;

ver si esta escribiendo o mandando mensaje de voz







E-commerce



Login

API con Py

Guardar el catalogo en&#x20;

Api gateways

RAVI para mensajes asincronos







COMPLEJIDAD CICLOMATICA: un monton de for o ciclos, hacerlo lo mas sencillo



Siguiente semana se dará sobre l documentación técnica formal, y no recuerdo





División de equipos:

* Infrestructura (5): front end y back end, todo esto en Kubernetes y no c. Se encargar de levantar el cluster, deployments y manifiestos, Tambien ntra lo de certificados de seguridad (?
* Testing (5): Calidad de código, que tenga calidad, pruebas solitarias
* Front End (6): Encargados de crear MicroFrontEnd para la autenticación
* BackEnd (6): Encargado de crear los microservicios, ayuda para que se pueda realizar por medio de OAUTH2

