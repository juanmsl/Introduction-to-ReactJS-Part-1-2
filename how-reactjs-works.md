# How ReactJS works

Now before start coding, lets read some theory to understand ReactJS better.

## What is ReactJS?

As we know to work in frontend, we have to know 3 basic stuff, _**HTML**_ that is the structure of your app, _**CSS**_ that are the styles and how your page looks like and at last _**Javascript**_ that is the behavior of the webpage. Commonly, we separate that code into folders, _**HTML**_ in the _public_ folder, _**CSS**_ in a _styles_ folder, and in a _scripts_ folder all _**Javascript**_, right?

**But why we do this?**

* To separate code, and have scalability...
* To have an order in the code...
* To separate in modules to reutilize them...
* etc.

With **ReactJS**, we Introduce all that together in components, defining the structure, how it looks like and behavior of that component. It provides more advantages to reutilize those components in different projects and allow a big scalability en each project.

![](.gitbook/assets/diapositiva3.png)

In Frontend development, you must divide any mockup, wireframe, design, page, etc; into blocks or components to know how to structure your webpage.

**ReactJS** want to help you to create components to represent that hierarchy of components, adding states to them, and updating that component according to the state, allowing specify the behavior of the component.

## How does it Work?

React Render the components into a single element in the HTML. If you open your **`index.html`** file in the public folder you can see something particular; in the **`body`** element, there are only one element with id **`root`**. The **`#root`** element is where all your React App will be rendered.

```markup
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="logo192.png" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>React App</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    
    <div id="root"></div>  <------ This is the ROOT element for your React App
    
  </body>
</html>
```

Then all you have to do is in _**Javascript**_, use the _virtualDom_ of React to render your App into **`#root`** element in the _**HTML**_.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <section>
    <h1>Hello World!, Im using ReactJS, and Its awesome!!!</h1>
  </section>,
  document.getElementById('root')
);
```

But.... **¿What is all that?**

![](.gitbook/assets/descarga.gif)

We know the DOM \(Document Object Model\)

> The **Document Object Model** \(**DOM**\) connects web pages to scripts or programming languages by representing the structure of a document. Know more about DOM [here](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model).
>
> Such as the HTML representing a web page.

ReactJS, use a virtualDOM in memory because, when DOM changes the web browser have to re-draw all webpage and it is cost for the machine, and takes time for the user; so, React use a VirtualDom to render all those components, and when an specific component change, only that component and his hierarchy will be rendered.

For that reason we use the library **`react-dom`**, so if you can see we use te method render of that library, to render a React component, into an HTML element.

```javascript
const element = <h1>Hello</h1>;
const container = document.getElementById('root');

ReactDOM.render(element, container);
```

{% hint style="info" %}
[ReactDOM by ReactJS](https://en.reactjs.org/docs/react-dom.html)
{% endhint %}

Okey... Okey... but... **¿Its that HTML is Javascript?**

**Yeah!!!** It is, well... not exactly, it is [**`JSX`** \(Javascript XML\)](https://en.reactjs.org/docs/introducing-jsx.html)

With JSX React join the structure _**HTML**_, and the behavior _**Javascript**_, into one! And to use it, you only have to import **`react`** library.



