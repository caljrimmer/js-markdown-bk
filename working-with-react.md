
Working with React.js
====================

React is a JavaScript library for creating user interfaces created by Facebook and Instagram. React is takes data and properties, and renders it to HTML.

React is analogous to Web Components, the upcoming standard for custom HTML5 user interface elements. React enforce building of components and subcomponents to provide a clean separation of concerns between different sections of your web application.


Props and state
---------------------

**Props** and **state** are JS objects that provide the data which will be used to render HTML in the React component.

**What are Props**

**Props** are provided to the React component when it is defined and are passed as configuration.

```javascript
const type = 'car';
const color = 'red';

<Vehicle type={type} color={red} />
```
The vehicle has **props** which configure the type and color of the vehicle. These **props** don't change, they are immutable.

**What is State**

State is defined within the React component and can change over time. **State** is mutable while **props** are immutable. 

React components manage the their own **state** but not that of their child React components. 

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


