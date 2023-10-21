# 🌲 Branches Strategies

Estrategia que ayuda a definir que raamas se crean a lo largo de la vida de un proyecto&#x20;

## ¿Como funcionan?

Es importante definirla al inicio de un proyecto para saber como las personas involuradas se desarrollan en el mismo.

Una de las mas usadas es GitFlow

### Git Flow.

Se plantea utilizar una rama main de la cual van a surgir las demas ramas, xontempla una rama Feature que&#x20;

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>



* 1 Main
* 2 La rama hotfix? hace un seteo mas rapido del problema, aisla el problema lo configura y se va a prducción
* 3 Develop: Rama de desarrollo, genera una copia de main llamada develop en donde se prueban los cambios antes de subirlos a la rama main, entonces los feature salen a partir de Develop y despues se suben a main.&#x20;
* 4 Releases: Scrum maneja tiempos cortos de dearrollo para la entrega de un productor funcional. por ello todos los datos trabajados (features y develop) se guardan en release y de ahi a main.



Tag: es la versión.

Explicación detallada d Git Flow: [https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

### Trunk based

Solo se usa para equipos pequeños; además es la opción para personas con bastante experiencia.

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

### Enviroment branching

Se tienen la main para el desarrollo. Estas tres ramas representan ambientes reales.&#x20;

A partir de master se desplega una feature hacia pre-producción y luego hacia producción.

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

#### Cherry pick vs hotfix

Se aisla un commit y se corrige el código, y se puede volver a probar o incorporar. Es mas fácil aislar el error.

### Feature branching&#x20;

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption><p>Feature branching, una variación de Git Flow</p></figcaption></figure>

### Release branching

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption><p>Release branching, otra variación de Git Flow</p></figcaption></figure>

La principal funcion de release es probar nuevas features

En trunk braching, cuales son las que son minimas o no existen, esas son releases y development.

