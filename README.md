# Curso Práctico de React JS
Notas y repo del [Curso Práctico de React JS en Platzi](https://platzi.com/clases/react-ejs/)

**Proyecto**: Platzi video

### Dependencias
```bash
npm install react react-dom
npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev
npm install webpack webpack-cli html-webpack-plugin html-loader --save-dev
npm install webpack-dev-server --save-dev
npm install mini-css-extract-plugin css-loader node-sass sass-loader --save-dev
npm install eslint babel-eslint eslint-config-airbnb eslint-plugin-import eslint-plugin-react eslint-plugin-jsx-a11y --save-dev
npm install file-loader --save-dev
```

- El **Git Ignore** es un archivo que nos permite definir qué archivos NO queremos publicar en nuestros repositorios. Solo debemos crear el archivo `.gitignore` y escribir los nombres de los archivos y/o carpetas que no queremos publicar.
- Los linters como **ESLint** son herramientas que nos ayudan a seguir buenas prácticas o guías de estilo de nuestro código.
Se encargan de revisar el código que escribimos para indicarnos dónde tenemos errores o posibles errores. En algunos casos también pueden solucionar los errores automáticamente. De esta manera podemos solucionar los errores incluso antes de que sucedan.
Instalación de ESLint:


## Conceptos previos
```sh
npx create-react-app nombre-de-tu-proyecto
npm start
```
### Creación y Tipos de Componentes
Los nombres de nuestros componentes deben empezar con una letra mayúscula, al igual que cada nueva palabra del componente. Esto lo conocemos como Pascal Case o Upper Camel Case.

Los componentes **Stateful** son los más robustos de React. Los usamos creando clases que extiendan de React.Component. Nos permiten manejar estado y ciclo de vida (más adelante los estudiaremos a profundidad).

```jsx
import React, { Component } from 'react';

class Stateful extends Component {
  constructor(props) {
    super(props);

    this.state = { hello: 'hello world' };
  }

  render() {
    return (
      <h1>{this.state.hello}</h1>
    );
  }
}

export default Stateful;
```
También tenemos componentes **Stateless** o Presentacionales. Los usamos creando funciones que devuelvan código en formato JSX (del cual hablaremos en la próxima clase).

```jsx
import React from 'react';

const Stateless = () => {
  return (
    <h1>¡Hola!</h1>
  );
}

// Otra forma de crearlos:
const Stateless = () => <h1>¡Hola!</h1>;

export default Stateless;
```
### JSX: JavaScript + HTML
Estamos acostumbrados a escribir código HTML en archivos .html y la lógica de JavaScript en archivos .js.

React usa JSX: una sintaxis que nos permite escribir la estructura HTML y la lógica en JavaScript desde un mismo lugar: nuestros componentes.

```jsx
import React from 'react';

const HolaMundo = () => {
  // Esto es JavaScript:
  const claseCSSHolaMundo = 'container-red';
  const mensajeTextoHTML = '¡Hola, Mundo!';
  const isTrue = false;

  // Esto es JSX (HTML + JavaScript):
  return (
    <div className={claseCSSHolaMundo}>
      <h1>{mensajeTextoHTML}</h1>

      {isTrue ? '¡Es verdad! :D' : '¡No es verdad! :('}
    </div>
  );
}

export default HolaMundo;
```

### Props: Comunicación entre Componentes

Las Props son la forma de enviar y recibir información en nuestros componentes. Son la forma de comunicar cada componente con el resto de la aplicación. Son muy parecidas a los parámetros y argumentos de las funciones en cualquier lenguaje de programación.

```jsx
// Button.jsx
import React from 'react';

const Button = props => {
  return (
	<div>
	  <button type="button">{props.text}button>
	div>
  );
};

export default Button;
```
```jsx
// index.jsx
import React from 'react';
import Button from './components/Button';

ReactDOM.render(
  <Button text="¡Hola!" />,
  document.getElementByid('root'),
);
```
### Métodos del ciclo de vida
Los componentes en react pasan por un Montaje, Actualización, Desmontaje y Manejo de errores.
- **Montaje:** En esta fase nuestro componente se crea junto a la lógica y los componentes internos y luego es insertado en el DOM.
```jsx
Constructor(); //Este es el primer método al que se hace un llamado, aquí es donde se inicializan los métodos controladores, eventos del estado.
getDerivedStateFromProps();//Este método se llama antes de presentarse en el DOM y nos permite actualizar el estado interno en respuesta a un cambio en las propiedades, es considerado un método de cuidado, ya que su implementación puede causar errores sutiles.
render();//Si queremos representar elementos en el DOM en este método es donde se escribe esta lógica, usualmente utilizamos JSX para trabajar y presentar nuestra aplicación.
ComponentDidMount();//Este método se llama inmediatamente que ha sido montado en el DOM, aquí es donde trabajamos con eventos que permitan interactuar con nuestro componente.
```
- **Actualización:** En esta fase nuestro componente está al pendiente de cambios que pueden venir a través de un cambio en “state” o “props” esto en consecuencia realizan una acción dentro de un componente.
```jsx
getDerivedStateFromProps();//Este método es el primero en ejecutarse en la fase de actualización y funciona de la misma forma que en el montaje.
shouldComponentUpdate();//Dentro de este método se puede controlar la fase de actualización, podemos devolver un valor entre verdadero o falso si queremos actualizar o no el componente y es utilizado principalmente para optimización.
render();//Se llama el método render que representa los cambios en el DOM.
componentDidUpdate();//Este método es invocado inmediatamente después de que el componente se actualiza y recibe como argumentos las propiedades y el estado y es donde podemos manejar nuestro componente.
```
- **Desmontaje:** En esta etapa nuestro componente “Muere” cuando nosotros no necesitamos un elemento de nuestra aplicación, podemos pasar por este ciclo de vida y de esta forma eliminar el componente de la representación que tiene en el DOM.
```jsx
componentWillUnmount();//Este método se llama justo antes de que el componente sea destruido o eliminado del DOM.
```
- **Manejo de Errores:** Cuando nuestro código se ejecuta y tiene un error, podemos entrar en una fase donde se puede entender mejor qué está sucediendo con la aplicación.
```jsx
getDerivedStateFromError();//Una vez que se lanza un error este es el primer método que se llama, el cual recibe el error como argumento y cualquier valor devuelto en este método es utilizado para actualizar el estado del componente.
componentDidCatch();//Este método es llamado después de lanzarse un error y pasa como argumento el error y la información representada sobre el error.
```
> Algo que debemos tener en cuenta es que un componente NO debe pasar por toda las fases, un componente puede ser montado y desmontado sin pasar por la fase de actualización o manejo de errores.

[Ver más info](https://medium.com/@danieruone/gu%C3%ADa-b%C3%A1sica-para-entender-componentes-en-react-js-9a0b07edb1f8)

### State - Events

"React nos permite responder a las interacciones de los usuarios con propiedades como `onClick`, `onChange`, `onKeyPress`, `onFocus`, `onScroll`, entre otras.

Estas propiedades reciben el nombre de la función que ejecuta el código que responde a las interacciones de los usuarios. Seguramente, esta función usará la función this.setState para actualizar el estado de nuestro componente.
```jsx
class Button extends React.Component {
  state = { count: 0 }

  handleClick = () => (
     this.setState({ count: this.state.count + 1 })
  );

  render() {
    const { count } = this.state;

    return (
      <div>
        <h1>Manzanas: {count}</h1>
        <button onClick={this.handleClick}>Sumar</button>
      </div>
    );
  }
}
```
> Recuerda que los nombres de estos eventos deben seguir la nomenclatura camelCase: primera palabra en minúsculas, iniciales de las siguientes palabras en mayúsculas y el resto también en minúsculas."

