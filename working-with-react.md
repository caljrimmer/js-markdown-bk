
Working with React.js
====================

React is a JavaScript library for creating user interfaces created by Facebook and Instagram. React is takes data and properties, and renders it to HTML.

React is analogous to Web Components, the upcoming standard for custom HTML5 user interface elements. React enforce building of components and subcomponents to provide a clean separation of concerns between different sections of your web application.

React is just the view layer of your web application. You cannot build a fully functioning web application with React.js alone. You can either augment other MVCframeworks with React.js (i.e. Angular 1.x or Backbone) or couched React.js in a statement framework (i.e. Fluxxor or Redux).

Why use React.js
------------------

React gives you a template language called *JSX* and helper functions to effciently render HTML. That's all React outputs, HTML. Your created HTML an Javascript, are called "Components".

React.js enforces all the rendering and functionality to exist in the same component. Traditionally HTML would be seperated from functionality. Javascript wouldn't be includes in HTML directly ()i.e. onClick()). This was to make both the HTML easier to read and parse at runtime. 

React.js uses its own markup language called JSX to tie functionality directly to markup. At runtime, the javascript and HTML are sperated from each other. This allows you create an easy to maintian, self contained Component when developing. The rendered HTML remains clean and readable in the DOM.

React is very effcient when rendering HTML to the DOM. It is ideal either in low latency applications (i.e. data changes quickly) or large data sets (1000+ rows worth of data need rendering).

React is also *Isomorphic*. This mean you can write React componenets that with either render on the client or on the server. This gives you flexibility on how you serve your views to users of your application. Server rendered pages can render faster and also provide better meta information for being indexed by search engines.

JSX
---

JSX is React.js rendering language. JSX adds XML syntax to JavaScript. You can use React without JSX but JSX makes React.js easier to read and more componentised.

React.js with JSX:
```javascript
const items = ['eggs','milk','bread'];
const addItem = event => {
    items.push(event.value);
}

ReactDOM.render(
    <TodoContainer>
        <h1>Shopping List</h1>
        <TodoList className="list" owner="Mrs Smith" listItems={items} />
        <TodoControls className="controls" addItemHandler={addItem} />
    </TodoContainer>,
    document.getElementById('body')
);

```

The above example demonstrates how React components are broken up. A TodoContainer component contains a TodoList and TodoControls component. Each component has a defined job. The more granular the components, the easy they are to test, re-use and maintain.

JSX tags have a name, attributes, and children. If an attribute value is enclosed in quotes, the value is a string (or a number without quotes). If the attribute is wrapped in curly braces ({}) the value is a JavaScript expression or object.

> **Note**

>React uses *className* instead of the *class*. React.js DOM components expect DOM property names like className and htmlFor, rather than DOM attributes like class or for.


Virtual DOM
--------------------

React.js is very effcient at rendering to the DOM because it has the concept of a virtual DOM. A virtual DOM combines an *in-memory* representation of the actual DOM with a smart diffing algorthim which compares differences in the web application model.

React.js provides a series of Javascript methods that create an in-memory DOM tree and performs updates in memory when data bound to it changes (determined by the diffing algorthim). Updating the virtual DOM is much quicker than updating the normal DOM directly. React does the hard work in the in-memory DOM and then, once all work is finsihed, renders the result in the normal DOM.

This optimisation all happens behind the scenes.You can code your JSX, Javascript and data bindings without having to worry about interacting with the virtual DOM. You will just experience the normal DOM updating very fast.

React also only interacts with specific parts of the normal DOM that needs to change. React.js, unlike say Backbone, will not re-render whole sections of the DOM but just the necessary DOM nodes where the bound data changes.

Smart diffing algorithm
---------------------------------------------------

Most popular web application frameworks (i.e. Angular 1.x, Backbone) follow a MVC architecture. The views re-render when the model changes. the changes are propgated by events emitted when the model changes. Models can have a one-to-many relationship with the views, and the views can have a one-to-many relationship to the models. 

This means a model change can be reflected in a number of views, and an event triggered in a view can change multiple models. This can lead to *spaghetti events*, i.e. code that is dificult to maintains and understand. An event can create unexpected consequences. It is also difficult to test larger MVC applications, as you have to mock all the model interations. 

The smart diffing algorithm allows you to create more functional approach to developing your application. You provide the previous state and the new state and let React do the hard work. You don't have to bind to model changes, just provide the new state and let React work out the best way to render this change to the DOM.

Functional react components are deterministic, i.e. you provide an input and the output will always be the same. You can wrtie tests easily because you design your application to only function one way when provided with a given state.

Props and state
------------------------

All React components use both props and state to communicate the data to be boudn to the virtual DOM. **Props** and **state** can be JS objects, functions or primitives (strings, numbers, booleans).

**Props** are provided to the React component when it is defined and are passed as configuration. Props are immutable, i.e. they don't change.

```javascript
const specs = {
    engineSize : 1.2,
    color: 'red'
};

ReactDOM.render(
  <Vehicle type="car" specs={specs} />,
  document.getElementById('body')
);

```
The vehicle has **props** (i.e. attributes) which configure the type and specs of the vehicle.

**State** is defined within the React component. They maintain the internal state of the component. React components change their own internal **state** but not that of their child or parent React components. State is mutable, i.e. state can be changed.

```javascript
import React, {Component} from 'React';

class Vehicle extend Component () {
	
	constructor (props) {
		super(props)
		this.state = {
			engineSize : 1.2,
            color: 'red',
			type : this.props.type
		}
	}
	
}

ReactDOM.render(
  <Vehicle type="car" />,
  document.getElementById('body')
);

```

We set the **state** of the React component in the class constructor.  The **state** can be informed from your **props** or they can be given a default value.

React Common Methods
---------------------------- 

React has a number of methods and variables available to aid in creating your application. There are certain methods that will use time and time again.

**constructor**
We need to augment the constructor with the props that are passed down to the React component. If we don't do this then our React application won't work. We should also set our React state in this constructor

```javascript
constructor (props) {
	super(props);
	this.state = {
		data : []
	}
} 
```

**render**

Render is mandatory for any react component. Render is where all the JSX code is placed. The render method is what gets painted to the DOM.

```javascript
render () {
	return (
		<div></div>
	)
}
```
**setState**
SetState updates the state of the React Component. The method also invokes render() to paint the new state to the DOM.

```javascript
this.setState({
	data : ['one','two','three']
})
```

**componentWillMount**

This is a lifecycle methods this is called before the component mounts on the DOM. This is useful for fetching or parsing data before the render method is called.

```javascript
componentWillMount (){
	$.get(this.props.url, (data) => {
		this.setState({
			data : data
		})
	})
}
```

**componentDidMount**

These is also a lifecycle method that are called after the component mounts on the DOM. This is useful when you wish to reference a mounted element in the DOM. 

```javascript
componentDidMount () {
	this.refs.title.disabled = true;
}

render () {
	return (
		<div>
			<input type="text" name="title" ref="title" />
		</div>
	)
}
```

**propTypes**

React allow you to define the props that you pass in to your react component. Proptypes make it easy for the you to validate and document your React application.  You will see a warning on the console if you invalidate one of your props.

```javascript
<Component
	items = {['one','two','three']}
	title = 'New Entry'
	count = {10}
/>

Component.propTypes = {
	items : React.PropTypes.array,
	title : React.PropTypes.string,
	count : React.PropTypes.number,
}
```


Counter React Component
-------------------------------

A React components does not need to have many moving parts. Infact it is better to keep your React componets simple. You should always look to make your React components do to as little as possible which will aid in make them re-usable throughout your applications.

We are going to create a simple counter component that increments a count when a button is clicked.

```javascript
import React, {Component} from 'react';

class Counter extend Component () {
    
    constructor (props) {
        super(props)
        this.state = {
            count : this.props.start
    }
    
	componentDidMount () {
		console.log('mounted');
	}

    increment () {
        this.setState({
            count : this.state.count + 1
        });
    }

    render () {
        <div>
            <div className="counter">{this.state.count}</div>
            <button onClick={::this.increment}>+</button>
        </div>
    }
    
}

Counter.propTypes = {
	start : React.PropTypes.number
}

ReactDOM.render(
    <Counter start={2} />,
    document.getElementById('body')
);

```
We create our **Counter** component class by extending the React component class. This provides us will all the baked in React methods which you can augment in your new component.

We define the component **state** in the class constructor. We use the **super** method to inherit any other props that might be passed down to the **counter** component. The only **state** we are concerned with is the **count** which we initially set to the value of the **start prop**.

Next we define a click handler called **increment()** which will update our **count** state. We use the React method **setState()** to update the new count value. **SetState()** will automatically make the **render()** method re-invoke. Therefore, the DOM will automatically update with the new count value when it is changed.

We define our **render()** method for the React component. React componets expect there to be a render method defined. This **render()** method informs the virtual DOM on how to map changes to bound data to the DOM. We use curly brackets ({}) to inject the **count** state value in to the DOM.  

**Render()** also provides a way of binding events ot the DOM. We have used the onClick even handler to bind the **increment()** method to a click on the button.

Finally we inject the component in the the body of our HTML document. **ComponentDidMount()** will fire and console out the message 'mounted'.

> **Tip**
> 
> The onClick method uses a double colon **Bind Operator** to provide context mapping to our **increment()** method. This makes the **this** in the **increment()** method to have the correct context and map to **setState()**

Structuring your React Application
-----------------------------------------

React components are meant to be re-useable and as simple as possible. A React component should ideally only do one thing.  Your application will end up being a parent component that is broken up into many maintainable and testable subcomponents.

```javascript
<Table>
	<TableHeader />
	<TableBody>
		<TableRow />
	</TableBody>
	<TableFooter />
</Table>
```

There are two kind of components that can be created. Stateless and stateful components.

**Stateless Components** (or dumb components) contains only props, no state. All the logic and handlers is provided props they receive.

**Stateful Components** contain both props and state. They manage the applications state and provide handlers for children stateless components. A stateful component generally handles client-server communication (XHR, web sockets). The majority of visualization and formatting logic happens in stateless components.

Your application will be made of a small number of stateful components and a larger number of stateless components. The aim is to keep all the state management in as few places as possible.


Todo React Web Application
----------------------------------------

Before we start, we need to have a base index.html page to instansiate our React aplication.

```html
<html>
  <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0-alpha1/react-with-addons.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0-alpha1/JSXTransformer.js"></script>
  </head>
  <body>
    <div id="container"></div>
    <script type="text/jsx"></script>
  </body>
</html>
```
We include React and also a JSX transformer script. We can do JSX transformation as a build step (which we will demonstrate later) but we will add a shim here for brevity. We also have a container element which will contain the React application.

We provide a **text/jsx** type for our script which is used by the JSX Transformer. This can be removed when we have our JSX transpliation as part of the build tools. 

**Creating the Todo Container**

First, we create a Todo Container React component. This will be our parent React container and instansiate all the children React components of our application.

```javascript
import React, {Component} from 'react';

class TodoContainer extends Component({
    
    constructor (props) {
        super(props);
        this.state = {
            items : ['get milk', 'clean car']
        }
    }

    addListItem (item) {
        this.setState({
            items : [...this.state.items, item]
        });
    }

    removeListItem (item) {
        const index = this.state.items.findIndex(x => x === item);
        this.setState({
            items : this.state.items.splice(index, 1)
        })
    }

    render () {
        return (
            <div className="todos">
                <h1>{this.props.title}</h1>
                <TodoInput addItem={::this.addListItem} />
                <TodoList 
                    items={this.state.items} 
                    removeItem={::this.removeListItem}
                />
            </div>
        );
    }
});

TodoContainer.propTypes = {
	title : React.PropTypes.string
}

ReactDOM.render(
    <TodoContainer title="Todo List" />,
    document.getElementById('container')
);
```

We extend a React class to create a **TodoContainer** parent component that takes a **title** prop. The **render()** method paints the title and invokes two undefined React Components called **TodoList** and **TodoInput**.

We create the application state in the parent which contains the **items** array and also the handler methods for the state. These are passed down as props to the children components. This means we only have to manage state in one place (i.e. the parent component).

We inject **TodoContainer** in to the container element with the title set as "Todo List".

```javascript

class TodoInput extends Component({

    constructor (props) {
        super(props);
    }

    validateInput () {
        const value = this.refs.addItem.value;
        if (!value === '') {
            this.props.addItem(value);
        }
    }

    render () {
        return (
            <div className="todo-input">
                <input type="text" ref="addItem" placeholder="Enter Task" />
                <button onClick={::this.validateInput}>Add Task</button>
            </div>
        );
    }
});

TodoInput.propTypes = {
	addItem : React.PropTypes.func
}

```
We create our **TodoInput** component which adds new todo items. We pass the addItems **prop** to the component through the constructor.

The **validateInput()** method validates that the inputed todo is not an empty string before passing it through the **addItem** prop. We have introduced the **this.refs** locator which allows your react component to pick out a DOM element which is decorated with a **ref** attribute.

```javascript

class TodoList extends Component({

    constructor (props) {
        super(props);
    }

    removeTodoItem (event) {
        const value = event.target.innerText;
        this.props.removeTodo(value)
    }

    render () {

        const ListItems = this.props.items.map(item => {
            return (
                <li onClick={::this.removeTodoItem}>{item}</li>
            )
        });

        return (
            <ul className="todo-items">
                {ListItems}            
            </ul>
        );
    }
});

TodoInput.propTypes = {
	removeTodo : React.PropTypes.func,
	items : React.PropTypes.array
}

```

The **render()** method has the **ListItems** array which is mapped from the original **items** array passed down through the props. 

The **ListItems** are iterated through when the component is instantiated in the DOM. Clicking on the list element removes the item from the items array.

Loading data into React
----------------------------

We can fetch data from external resources to populate our react components. Let's use JQuery's ajax methods to fetch random names and populate a React component.

```javascript
import React, { Component } from 'react';
import $ from 'jquery';

class NameList extends Component({
	
	constructor (props) {
		this.state = {
			persons : []
		}
	}
	
	componentDidMount () {
	    this.request = $.get(
		    this.props.url, 
		    (results) => {
			    this.setState({
			        names: results 
			    });
		    }
	    );
	}

    componentWillUnmount () {
	    this.request.abort();
    }

	render () {
		const Persons = this.state.persons.map((person) => {
			return (
				<li>{person.name} {person.surname}</li>
			)
		});
		return (
			<ul>{Names}</ul>
		)
	}

});

NameList.propTypes = {
	url : React.PropTypes.string
}

ReactDOM.render(
    <NameList url="http://uinames.com/api/?amount=10" />,
    document.getElementById('body')
);
```

**ComponentWillMount** and **ComponentWillUnmount** are lifecycle methods native to React. The first is called before the React component writes to the DOM and the latter when the component is removed from the DOM.

We request the **persons** data via **$.get()** in **ComponentWillMount** and we then set the state of the component. This request happens before component mounts and the will re-render the list items when the request is successful.

We map the **persons** array to return list elements that we inject in the DOM.

We can tidy the request object up when we unmount the component by invoking **abort()** in **ComponentWillUnmount()**.


Flux Architecture
----------------------------

Flux is an architecture rather than a framework. It provides a way to structure your React web applications so that they are maintainable and easy to debug.

Flux was developed by Facebook as a way to move away from the more standard MVC (model-view-controller) towards a pattern with a uni-directional data flow. 

```javascript
//MVC
model -> view -> model

//Flux
store -> view -> action -> dispatcher -> store
```

The MVC approach meant that the view could change a model and the model change a view, this could create spaghetti events that were difficult to debug.

The Flux approach enforces the rule that the view never informs the model/store. A view, dispatcher and store have distinct inputs and outputs. It is a more functional approach to coding that makes it easier to test and debug our code.

**Store**

A **store** is just a simple object literal. It has no listeners bound to it (like a model) but just gets amended when a **dispatcher** interacts with it.

```javascript
const store = {
	items : [],
	lastUpdated : ''
};
```

**Actions**

An **action** is a method that is generally initiated from a **view** (but can also be initiated by server interactions). The **action** will contain a **value** which is the data you wish to augment the store with and a **type** which informs the **dispatcher** how to deal with that data.

```javascript
const addItemAction = {
	type : 'INSERT_ITEM',
	value : {
		task : 'Buy socks',
		created : new Date()
	}
})
```
The example action method has a **type** of 'UPDATING_LIST', and a **value** which has a task and the date it was created. An action will always send a payload with atleast a type and a value. It is possible to add additional parameters.

**Dispatcher**

The **dispatcher** manages data flow in your application. It provides a bridge between the data **store** and the **actions**. It has no logic of its own. The dispatcher uses the **type** of the action to inform the store what it should do with the **value** via a callback. 

```javascript
const dispatcher = function(action) {
    switch (action.type) {
      case 'INSERT_ITEM':
	      store.items.push(action.value);
	      store.lastUpdated = action.value.created;
      default:
	      return store;
}
```

**View**

The view is just your React component that has been enriched with actions.

```javascript
import { addItemAction } from 'actions'
class List extends React.Component () {
	
	constructor (props) {
		this.addItem = this.handleAddItem.bind(this);
	}

	addItem () {
		this.dispatch({
			type : 'ADD'
		});
	}
	
}
```

**Testing React**

**Redux**