
**ENTREGA DE PROYECTO PRIMER MARTES DE LA PRIMERA SEMANA DE FINALES 5 DE DICIEMBRE**

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

*Ejemplo: Herramientas como Jira
FIX (Unique_ID): Description
FEAT
BREAK
MAJOR
MINOR
HELPFIX
BUGFIX*
--- 

Todo el archivo de configuración lo toma el swagger par apoder mostrarlomas bonito sobre la funcionalidad.

---
---
# React

## 



GENERAR INTERFAZ GRAFICA 



