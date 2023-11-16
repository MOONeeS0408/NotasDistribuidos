# Page 2



1. Revisión del repositorio, personas que trabajaron
   1. seguir una branch strategy.
2. Logeo&#x20;
3. Tratamiento de Errores / Error Handling
   1. critical, high, medium, low
   2. CAsos de prueba para los errores.
4. Responsive
   1. PRorzar moviles sobre computadora
   2. no bootstrap, no css, solo MUI
5. Directory Structure
   1. La establecida para el curso
   2. commit igual seguir una convención.
6. Unit test / Pruebas unitarias
   1. Una imagen pero si esta mal se tiene que repetir
   2. UAT documentacion  ded los casos de prueba.
   3. carpeta de test para la realizacion de pruebas unitarias,
   4. PRobado por fiabilidad que exista o no exista, o por funcionalidad.
7. Deploy (en kubernetes)
   1. Despliegue en cualquier contenedor
8. Documentation &#x20;
   1. Se puede entregar después de la primera revisión.
   2. archivo o url
9. Tecnologías (al menos las usadas en clase)

Al final de la revisión se podrá entregar de nuevo y será en equipo.



<mark style="color:yellow;">Se tiene una semana después de terminar los temas para entregar.</mark>

<mark style="color:yellow;">Para la primera revisión se contaran 10 dias, después ya se consideraran las revisiones cada semana, total de revisiones 3.</mark>



Si alguno de los puntos no se realiza, no se va a contar para las siguientes revisiones.&#x20;







\--------------

Micro Front Ends PRojects

Evalluation Criteria



Repository Guidelines

1.  Repository establishment:&#x20;

    a. Begin by creating a **well-organized** repository.

    b. Ensure the utilization of a **clear and consistent branch strategy**
2.  Branch strategy implementation:

    a. Establish a branch strategy that aligns with project requirements.

    b. Adhere to the  defined branch strategy to foster a streamlined development process.
3. Evident  Repository
   1. visible, documentacion correcta



```


|--FEATURE_MODULE
|    |--node_modules
|    |--app/
|        |--layout.js
|        |--page.jsx
|    |--public
|    |--components
|    |--tests
|        |--index.test.js
|--.gitignore
|--Dockerfile
|--deployment.yml
|--service.yml
|--next.config.js
|--jest.config.js
|--jsconfig.json
|--package-lock.json
|--package.json
|--README.md
```

{% code overflow="wrap" %}
```

import COMPONENTS from LIBRARY

export default function MODULE_COMPONENT {

    return(
        Here should be defined the components or elements from the library such as MUI to create every part that 
    
    )
};
```
{% endcode %}

































