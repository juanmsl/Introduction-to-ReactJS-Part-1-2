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

You can declare variables that have **`JSX`** as value, as the example above in the **`line 1`**. Or you can declare functions that receive parameters and returns a **`JSX`** element. So create components using **`JSX`** its to easy.

## How can I create a component?

You create a component in declaring it in a function, or a class

{% code-tabs %}
{% code-tabs-item title="src/button/index.js" %}
```javascript
import React from 'react';

const Button = () => (
    <a href="https://en.reactjs.org/"
       className="button link"
    >
        Learn ReactJS
    </a>
);

export default Button;
```
{% endcode-tabs-item %}

{% code-tabs-item title="src/index.js" %}
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import Button from './button';

ReactDOM.render(
  <Button />,
  document.getElementById('root')
);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Yeah, that its great, but if I want a dynamic button?

You use the props of the component, the props are the properties that you pass to the component  when you use it, as similar as attributes in an HTML tag. And the component receive that properties as a dictionary.

{% code-tabs %}
{% code-tabs-item title="src/button/index.js" %}
```javascript
import React from 'react';

const Button = (props) => (
    <a href={props.url}
       className={`button ${props.className}`}
    >
        {props.content}
    </a>
);

export default Button;
```
{% endcode-tabs-item %}

{% code-tabs-item title="src/index.js" %}
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import Button from './button';

const content = (
  <section>
    <Button
      url="https://en.reactjs.org/"
      className="link"
      content="Learn ReactJS"
    />
    <Button
      url="https://en.reactjs.org/tutorial/tutorial.html"
      className="link"
      content="Tutorial: Intro to React"
    />
  </section>
);

ReactDOM.render(
  content,
  document.getElementById('root')
);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

In the example above, we create two different buttons, with the same component. So you can define props for your component to receive data that you want to show.

## Components lifecycle and features

Create functional component are great, but they cant provide me more complex context for a component, for example grid of projects requested to an API, how can I add behavior to my component, or how can I add a state so that the component depends on it, continue with the example, if component state don't have projects, the component should render a message that there are not projects available, and is component state have projects, show the projects in a grid and a filter bar.

To use a complex component, we can use a class that extends the Component of React, it inherit all methods and implements the lifecycle of a component in ReactJS.

```javascript
import React from 'react';

class ProjectsGrid extends React.Component {

}

export default ProjectsGrid;
```

First of all we create a class that **`extends`** the **React `Component`**, to use the lifecycle React component, after that we need to implement the **`render`** method, that will return the JSX, of the component.

{% code-tabs %}
{% code-tabs-item title="class" %}
```javascript
import React from 'react';

class ProjectsGrid extends React.Component {
    render() {
        return (
            <section>Im a projects grid to {this.props.name}</section>
        );
    }
}

export default ProjectsGrid;
```
{% endcode-tabs-item %}

{% code-tabs-item title="function" %}
```javascript
import React from 'react';

const ProjectsGrid = (props) => (
    <section>Im a projects grid to {props.name}</section>
);

export default ProjectsGrid;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

By the moment our component don't have a state and a big complexity, so its not too different from a functional component, as you can see in the code above, there are the same component written as a class and as a function.

Now we gonna add it a state to our component, so we'll continue with our component as a class, because with a functional component \(without hooks\) we can't handle a component state. For that we need to specify a **`constructor`** in the class, and there will be we gonna define our state. The component state should a dictionary as JSON, and you can specify any number of items you want.

```javascript
import React from 'react';

class ProjectsGrid extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            projects: []
        };
    }

    render() {
        return (
            <section>Im a projects grid to {this.props.name}</section>
        );
    }
}

export default ProjectsGrid;
```

Now that we have a state in our component, and we know that the component depends on his state, when his state change, the component will re-render. 

We gonna use a method of the lifecycle of the React Component, **`componentDidMount`** only execute after first render of the component, so we gonna use it to fetch the projects.

{% hint style="info" %}
[React lifecycle methods diagram](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)
{% endhint %}

```javascript
import React from 'react';

class ProjectsGrid extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            projects: [],
            message: "There are not projects"
        };
    }
    
    componentDidMount() {
        fetch("https://api.url/projects")
            .then((response) => {
                const data = response.json();
                this.setState({
                    projects: data
                });
            })
            .catch(function(error) {
                this.setState({
                    error: "Error: " + error.message
                });
            });
    }

    render() {
        return (
            <section>Im a projects grid to {this.props.name}</section>
        );
    }
}

export default ProjectsGrid;
```

As you can see in the example above, you can only **set the state in the constructor,** after that, you **can not modify the state directly**, to update it, you use the method **`setState`** inherit from the **React Component** class. Its not necessary to send all state again in **`setState`** method, only specify the keys that will change; when you call **`setState`**, the method will re-render, because the state change.

{% hint style="info" %}
[React Component State and Lifecycle](https://en.reactjs.org/docs/state-and-lifecycle.html)
{% endhint %}

Now we gonna render the projects grid depends on the state, as we describe at the beginning of the example.

```javascript
import React from 'react';

class ProjectsGrid extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            projects: [],
            message: "There are not projects"
        };
    }
    
    componentDidMount() {
        fetch("https://api.url/projects")
            .then((response) => {
                const data = response.json();
                this.setState({
                    projects: data
                });
            })
            .catch((error) => {
                this.setState({
                    error: "Error: " + error.message
                });
            });
    }

    render() {
        if(this.state.projects.lenght > 0) {
            return null; // Return projects grid
        } else {
            return (
                <section>
                    <p>{this.state.message}</p>
                </section>
            );
        }
    }
}

export default ProjectsGrid;
```

Now if there are no projects, it will show the message **`"There are not projects"`**, and if the fetch result cause an error, the error will be the error message. But if there are projects to show, render the projects grid.

To render a list we need to **`map`** each item to a **`JSX`** element, and each element need as parameter a unique key.

{% hint style="info" %}
[Map function documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
{% endhint %}

```javascript
import React from 'react';
import Project from './project';

class ProjectsGrid extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            projects: [],
            message: "There are not projects"
        };
    }
    
    componentDidMount() {
        fetch("https://api.url/projects")
            .then((response) => {
                const data = response.json();
                this.setState({
                    projects: data
                });
            })
            .catch((error) => {
                this.setState({
                    error: "Error: " + error.message
                });
            });
    }
    
    renderProjects = () => {
        return this.projects.map((project, i) => {
            return (
                <Project
                    key={i}
                    name={project.name}
                    cost={project.cost}
                />
            );
        });
    }

    render() {
        if(this.state.projects.lenght > 0) {
            return this.renderProjects();
        } else {
            return (
                <section>
                    <p>{this.state.message}</p>
                </section>
            );
        }
    }
}

export default ProjectsGrid;

```

Lets go for parts...

In **`line 2`** I import the Project component, to render a specific project

In **`lines 28-38`** I create a method in class **`ProjectsGrid`** to render my projects list

In **`line 29`**, pass to map function, a function that receive the **`current item`** of the list, and the **`index`** of that item in the list, this to use that index as unique **`key`** for the project in **`line 32`**.

In **`line 42`** I call the method **`renderProjects`** to render my projects.

{% hint style="info" %}
[More about React component](https://en.reactjs.org/docs/react-component.html)
{% endhint %}

And thats it, we have created a complex component, that haven't project, but when it render himself at the first time, it fetch the projects to an API, and then render those projects, to use a class component is the same thing as functional component.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import ProjectsGrid from './projectsGrid';

ReactDOM.render(
  <ProjectsGrid />,
  document.getElementById('root')
);
```

## Babel

To work I use Babel to help with Javascript to use the functionalities that ECMAScript provides me, off course you can use typescript if you want, but for this guide I'll use Babel.

{% hint style="info" %}
Read more about [Babel](https://babeljs.io/) or [TypeScript](https://www.typescriptlang.org/)
{% endhint %}

