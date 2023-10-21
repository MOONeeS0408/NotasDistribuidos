# Testing

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
'use client';

import { useState } from 'react';
import { Container, Typography, TextField, Button } from '@mui/material';

export default function Home() {
  const [num1, setNum1] = useState(0);
  const [num2, setNum2] = useState(0);
  const [result, setResult] = useState(0);

  const add = () => {
    setResult(parseInt(num1) + parseInt(num2));
  };

  const substract = () => {
    setResult(parseInt(num1) - parseInt(num2));
  };

  const multiply = () => {
    setResult(parseInt(num1) * parseInt(num2));
  };

  const divide = () => {
    setResult(parseInt(num1) / parseInt(num2));
  };

  return(
    <Container
      sx={{
        display: 'flex',
        flexDirection: 'column',
        alignItems: 'center',
        justifyContent: 'center',
        height: '100vh',
        padding: '0 2rem',
      }}
    >
      <Typography
        variant='h1'
        sx={{
          fontSize: '4rem',
          fontWeight: 'bold',
          marginBottom: '1rem'
        }}
        data-testid='result'
      >
        {result}
      </Typography>
      <TextField
        type='number'
        variant='outlined'
        label='num1'
        sx={{
          margin: '0.5rem 0',
          padding: '0.5rem',
          fontSize: 'large',
          width: '13rem',
          borderRadius: '10px',
        }}
        inputProps={{ 'data-testid': 'num1' }}
        value={num1}
        onChange={(e) => setNum1(e.target.value)}
      />
      <TextField
        type='number'
        variant='outlined'
        label='num2'
        sx={{
          margin: '0.5rem 0',
          padding: '0.5rem',
          fontSize: 'large',
          width: '13rem',
          borderRadius: '10px',
        }}
        inputProps={{ 'data-testid': 'num2' }}
        value={num2}
        onChange={(e) => setNum2(e.target.value)}
      />
      <Button
        onClick={add}
        sx={{
          fontSize: 'large',
          padding: '0.5rem',
          width: '13rem',
          margin: '0.5rem 0',
          border: '1px solid black',
          borderRadius: '10px',
        }}
        data-testid='add'
      >
        Add
      </Button>
      <Button
        onClick={substract}
        sx={{
          fontSize: 'large',
          padding: '0.5rem',
          width: '13rem',
          margin: '0.5rem 0',
          border: '1px solid black',
          borderRadius: '10px',
        }}
        data-testid='subtract'
      >
        substract
      </Button>
      <Button
        onClick={multiply}
        sx={{
          fontSize: 'large',
          padding: '0.5rem',
          width: '13rem',
          margin: '0.5rem 0',
          border: '1px solid black',
          borderRadius: '10px',
        }}
        data-testid='multiply'
      >
        multiply
      </Button>
      <Button
        onClick={divide}
        sx={{
          fontSize: 'large',
          padding: '0.5rem',
          width: '13rem',
          margin: '0.5rem 0',
          border: '1px solid black',
          borderRadius: '10px',
        }}
        data-testid='divide'
      >
        divide
      </Button>
    </Container>
  );
}

```
{% endcode %}



Linea 45 con la linea  `data-testid='result'` se usa para etiquetar los elementos. En los text Fields se usa InputProps, value y OnChanges. Nos permite buscar con mayor facilidad&#x20;



Primero debemos instalar unas dependencias.&#x20;



npm install --save-dev @testing-library/react @testing-library/jest-dom&#x20;

npm install jest-enviroment-jsdom



npm run test



Importante conocer los tipos de pruebas que hacemos

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

<mark style="color:blue;">Pruebas unitarias:</mark> creadas por le mismo desarrollador, pueden ser manuales o automatizadas, generar casos de prueba y ejecutarlas.&#x20;

Ejemplo: realizar una prueba que 2 + 2 realmente da 4 y no se concatene y dé como resultado 22

<mark style="color:blue;">Pruebas de integración / pruebas de API:</mark> conjunto de pruebas unitarias.

Ejemplo: uno desarrolla un login, y otra persona desarrolla otro módulo, en el branch de release de verifica que todas las funcionalidades funcionen en conjunto.&#x20;

<mark style="color:blue;">Pruebas Unitarias de UI / pruebas End-to-end o E2E:</mark> es sobre el API especifico, se generan obre la Interfaz gráfica, sobre las url, prueba completa del back-end hasta front-end

<mark style="color:blue;">Manual Testing:</mark> pruebas que no pueden ser probadas de manera automatica, también se suelen llamar Smoke test  o Pruebas de regresión (regretion test). Pruebas mas especializadas.&#x20;





index.text.js

Fire event - poder ejecutar una interfaz grafica

Render para renderizar fuera de la app principal

Screen permite conocer los IDs de nuestras pantallas principales?&#x20;



act - no recuerdo&#x20;

```javascript
import Home from '../app/page';
import '@testing-library/jest-dom';
import { fireEvent, render, screen } from '@testing-library/react';
import { act } from 'react-dom/test-utils';
```



Se realizan pruebas unitarias, empezando con la aplicación principal.&#x20;



Estas pruebas unitarias van con una funcionalidad especifica, se realizan aserciones es decir en base a una teoría se comprueba.&#x20;

```javascript
describe('Calculator', () => {
  it('renders a calculator', () => {
    render(<Home />);

    expect(screen.getByTestId('result')).toBeInTheDocument();
    expect(screen.getByTestId('num1')).toBeInTheDocument();
    expect(screen.getByTestId('num2')).toBeInTheDocument();
    expect(screen.getByTestId('add')).toBeInTheDocument();
    expect(screen.getByTestId('subtract')).toBeInTheDocument();
    expect(screen.getByTestId('multiply')).toBeInTheDocument();
    expect(screen.getByTestId('divide')).toBeInTheDocument();
  });
```

Espero que en mi pantalla, un texto con Id result aparezca en la pantalla, si el elemento no existe la prueba unitaria fallará.  Todo tiene que existir.&#x20;





it - permite realizar pruebas unitarias.&#x20;

```javascript
  it('add numbers', () => {
    render(<Home />);

    const num1input = screen.getByTestId('num1');
    const num2input = screen.getByTestId('num2');
    const addButton = screen.getByTestId('add');
    const resultArea = screen.getByTestId('result');

    fireEvent.change(num1input, {target: {value: 5}})
    fireEvent.change(num2input, {target: {value: 8}})

    act(() => {
      addButton.click();
    });
    
    expect(resultArea).toHaveTextContent('13');
  });
```

Con act hacemos que se realice laccion del botón.

Fireevent.change fuerza los valores para comparar el resultado obtenido y esperado.&#x20;





cd microfrontends/8\_tsting...

npm run test



PACKAGE.JSON

Agregar siempre&#x20;

```json
    "test": "jest --watch"
```







Si hay algo qu falle no la a&#x20;

compilador ayuda a la atraducciñon



Portable,&#x20;



configuracion para next js.&#x20;

Carpeta con binarios -> out



PAra carpeta out no se versiones, se crea un artefacto, artefacto, esta&#x20;



3 octetos, el rpiemro es para cambios menores,



x \* (y) logs,





PAra despegar en un contenedor...

Docker file.



Copiar todos los binarios.

docker ps

docker build&#x20;





Rdocker start deploy app&#x20;





xample kubectl port-forward service---7deployment-app-service 8080:8080











