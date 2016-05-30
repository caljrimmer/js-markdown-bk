
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
<TodoContainer>
    <h1>Shopping List</h1>
    <TodoList className="list" owner="Mrs Smith" listItems={items} />
    <TodoControls className="controls" addItemHandler={addItem} />
</TodoContainer>
```

React.js without JSX:
```javascript
const items = ['eggs','milk','bread'];
const addItem = event => {
    items.push(event.value);
}
React.createElement(
    TodoContainer,
    React.createElement("h1", null, "Shoppping List"),
    React.createElement(TodoList, { className: "list", listItems: items})
    React.createElement(TodoControls, { className: "controls", addItemHandler: addItem})
);
```

The above example demonstrates how React components are broken up. A TodoContainer component contains a TodoList and TodoControls component. Each component has a defined job. The more granular the components, the easy they are to test, re-use and maintain.

JSX tags have a name, attributes, and children. If an attribute value is enclosed in quotes, the value is a string (or a number without quotes). If the attribute is wrapped in curly braces ({}) the value is a JavaScript expression or object.

> **Note**

>React uses *className* instead of the *class*. React.js DOM components expect DOM property names like className and htmlFor, rather than DOM attributes like class or for.


React.js Virtual DOM
--------------------

React.js is very effcient at rendering to the DOM because it has the concept of a virtual DOM. A virtual DOM combines an *in-memory* representation of the actual DOM with a smart diffing algorthim which compares differences in the web application model.

React.js provides a series of Javascript methods that create an in-memory DOM tree and performs updates in memory when data bound to it changes (determined by the diffing algorthim). Updating the virtual DOM is much quicker than updating the normal DOM directly. React does the hard work in the in-memory DOM and then, once all work is finsihed, renders the result in the normal DOM.

This optimisation all happens behind the scenes.You can code your JSX, Javascript and data bindings without having to worry about interacting with the virtual DOM. You will just experience the normal DOM updating very fast.

React also only interacts with specific parts of the normal DOM that needs to change. React.js, unlike say Backbone, will not re-render whole sections of the DOM but just the necessary DOM nodes where the bound data changes.

Addition advantages of the smart diffing algorthim
---------------------------------------------------

Most popular web application frameworks (i.e. Angular 1.x, Backbone) follow a MVC architecture. The views re-render when the model changes. the changes are propgated by events emitted when the model changes. Models can have a one-to-many relationship with the views, and the views can have a one-to-many relationship to the models. 

This means a model change can be reflected in a number of views, and an event triggered in a view can change multiple models. This can lead to *spaghetti events*, i.e. code that is dificult to maintains and understand. An event can create unexpected consequences. It is also difficult to test larger MVC applications, as you have to mock all the model interations. 

The smart diffing algorithm allows you to create more functional approach to developing your application. You provide the previous state and the new state and let React do the hard work. You don't have to bind to model changes, just provide the new state and let React work out the best way to render this change to the DOM.

Functional react components are deterministic, i.e. you provide an input and the output will always be the same. You can wrtie tests easily because you design your application to only function one way when provided with a given state.


Props and state
---------------------

**Props** and **state** are JS objects that provide the data which will be used to render HTML in the React component.

**What are Props**

**Props** are provided to the React component when it is defined and are passed as configuration. Props are immutable, i..e. they don't change.

```javascript
const type = 'car';
const color = 'red';
<Vehicle type={type} color={red} />
```
The vehicle has **props** (i.e. attributes) which configure the type and color of the vehicle.

**What is State**

State is defined within the React component. They maintain the internal state of the component. React components change their own internal **state** but not that of their child or parent React components. State is mutable, i.e. state can be changed.

```javascript
import React from 'React';

class Vehicle extend React.Component () {
	
	constructor (props) {
		super(props)
		this.state = {
			speed : 0,
			type : this.props.type
		}
	}
	
	goFaster () {
		this.setState({
			speed : speed + 10
		})
	}

	render () {
		const color = this.props.color || 'blue';
		const type = this.props.type || 'boat';
		const speed = this.state.speed;
		return (
			<p>The {this.props.color} {this.state.type} has a speed of {this.state.speed} mph. <a onClick={this.goFaster} href="">Click me to go Faster</a></p>
		)
	}
}
```

We set the **state** of the React component in the constructor.  The **state** can be informed from your **props** or they can be given a default value.

We update the **state** using the **setState()** method. This will automatically call the **render()** method to create the HTML.

**Types of Components**

**Stateless Components** contains only props, no state. All the logic revolves around the props they receive. This makes them very easy to follow (and test for that matter). We sometimes call these dumb-as-f*ck Components (which turns out to be the only way to misuse the F-word in the English language).

**Stateful Components** contain both props and state. We also call these state managers. They are in charge of client-server communication (XHR, web sockets, etc.), processing data and responding to user events. These sort of logistics should be encapsulated in a moderate number of Stateful Components, while all visualization and formatting logic should move downstream into as many Stateless Components as possible.

**What is Flux**

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


