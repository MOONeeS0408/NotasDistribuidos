
**ENTREGA DE PROYECTO PRIMER MARTES DE LA PRIMERA SEMANA DE FINALES 5 DE DICIEMBRE**
**ENTREGA DE CALIFICACIONES PRESENCIAL 14 DE DICIEMBRE**
Tienen que venir los integrantes, si alguno falta no se tomara en cuenta para calificación. 


# Swagger
## Documentacion de API

Flask 3.0.0

En la nueva versión de flask las siguientes herramientas no funcionan para poder hacer el json automaticamente; sin embargo, en la nueva versión de Flask estas herramientas ya no funcionan. 
```
flask-restfulplus
```
```
flask-restx
```

Para poder ver todos los endpoints.


Usaremos flask-swagger-ui   4.11.1

recordar instalar usando py3

Realizaremos modificaciones en nuestro app.py

SWAGGER_URL
API_URL -> ruta del archivo de configuración .json

get_swagger_ui_blueprint -> recordar que usamos blueprint anteriormente.



Al pedir http://localhost:5000/swagger se puede ver las funcionalidades del API
Se pueden ver los metodos que se tienen, los tipos de respuestas que se pueden obtener. 


Al darle execute, ejecuta la petición, y muestra todas las respuestas e incluso se puede descargar. 

## Cómo configurar el Swagger.
El archivo de configuración .json 

Primero generar una carpeta llamada satc en donde vamos a colocar el swagger.json
Usaremos v2.0

---
**Sematic Released Version**: Convención para poder deetrminar la versión de tu software. 

Usando 3 octetos:
          1    .    0    .    0 
    major breaks         minorfix/patches

Hay herramientas que te permiten identificar en base a los cambios, puede ser incluso en base al Git. Por ello es importante seguir un estandar en commits para poder identificar más facilmente los cambios realizaos. 

*Ejemplo: Herramientas como Jira*
*FIX (Unique_ID): Description*
*FEAT*
*BREAK*
*MAJOR*
*MINOR*
*HELPFIX*
*BUGFIX*

---

Todo el archivo de configuración lo toma el swagger par apoder mostrarlomas bonito sobre la funcionalidad.

---
---

# COMO CONFIGURAR NUESTRO BACK END A NUESTRO FRONT

AXIOS nos permitirá acceder de manera automatica al API

Usar una carpeta *utils*  con un rchivo API.jsx

Aqui se importa axios

```
API_BASE_URL = 'http://localhost:5000/api'
```


Creamos una función de tipo aincrona porque estamos esperando que se realice la petición

Usar una ocnstante response = await axios.get();

dentro del get colocamos la ruta para ello usamos comillas invertidas *`${API_BASE_URL}/books`*



Una función asincrona por cada función a realizar. 



En el componente se observa todo los errores y el handle qu realize para poder mandarlo a llamar...



En nuestro archivo principal page importamos todo



mapa -> diccionario, se usa book_id como el numero para poder identificar la tarjeta aunque no aparezca en ella. 




CORS -> impide hacer peticiones de una web a otra
Cross-Origin: https://aws.amazon.com/es/what-is/cross-origin-resource-sharing/

Para cambiar esto se instala una nueva dependencia llamada Flask-Cors

En app.py agregar una linea, no estoy segura de los parentesis...
```
CORS(app, resources={r'/api/books': ('origins':'http://localhost:3000') }) 
```


# Redireccionamiento sin Route
Revisar ruteo, para ello debe colocarse una carpeta con el contexto en este caso books, en la cual se crea un archivo page.jsx en el cual en la parte en donde se quiere que redireccione colocamos un Link href='/books'





GENERAR INTERFAZ GRAFICA 



