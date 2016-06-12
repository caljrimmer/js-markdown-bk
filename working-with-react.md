
Working with React.js
====================

React is a JavaScript library for creating user interfaces created by Facebook and Instagram. React takes data and properties, and renders it to HTML.

React is analogous to Web Components, the upcoming standard for custom HTML5 user interface elements. React enforce building of components and subcomponents to provide a clean separation of concerns between different sections of your web application.

React is just the view layer of your web application. You cannot build a fully functioning web application with React.js alone. You can either augment other MVC frameworks with React.js (i.e. Angular 1.x or Backbone) or couching React.js in flux framework (i.e. Fluxxor, alt or Redux).

Uses of React.js
------------------

Traditionally HTML would be separated from functionality. Javascript wouldn't includes in HTML directly ()i.e. onClick()). This makes both the HTML easier to read and parse at runtime. 

React, however,  enforces all the rendering and functionality to exist in the same component. React uses its own markup language called **JSX** to tie functionality directly to markup. At runtime, the javascript and HTML are separated from each other. This allows you create an easy to maintain, self contained Component when developing. The rendered HTML remains clean and readable in the DOM.

React is very efficient when rendering HTML to the DOM. It is ideal either in low latency applications (i.e. data changes quickly) or large data sets (1000+ rows worth of data need rendering). This achieve with React's virtual DOM implementation.

React is also **Isomorphic**. This means you can write React components that with either render on the client or on the server. This gives you flexibility on how you serve your views to users of your application. Server rendered pages can render faster and also provide better meta information for being indexed by search engines.

**React Native** is a couching framework for React that lets you write applications that will run as apps on mobile devices. You can have very similar React code that can run in the browser and also on mobile applications. This allows you to build one hybrid code base that can run in multiple environments.

**React Developer Tools** is a Chrome DevTools extension. It provides a new tab called React in your Chrome DevTools. Within the tools, you can inspect and edit a component's current props and state.  Also you can easily find which component threw an error during rendering, and what state or props lead to it.

JSX
---

JSX is React.js rendering language. JSX adds XML syntax to JavaScript. You can use React without JSX but JSX makes React.js easier to read and more componentized.

The below example demonstrates how React components are broken up. A TodoContainer component contains a TodoList and TodoControls component. Each component has a defined job. The more granular the components, the easy they are to test, re-use and maintain.

React.js with JSX:
```javascript
const items = ['eggs','milk','bread'];
const addItem = event => {
    items.push(event.value);
}

ReactDOM.render(
    <TodoContainer>
        <TodoList className="list" owner="Mrs Smith" listItems={items} />
        <TodoControls className="controls" addItemHandler={addItem} />
    </TodoContainer>,
    document.getElementById('body')
);

```

JSX tags have a name, attributes, and children. If an attribute value is enclosed in quotes, the value is a string (or a number without quotes). If the attribute is wrapped in curly braces ({}) the value is a JavaScript expression or object.

JSX needs to be either compiler or transpiled before consumed by the browser. JSX isn't supported natively in the browser. This means we have to have either have a build step to convert the JSX into native Javascript (which we will discuss in the next chapter) or we provide an additional javascript polyfill script to provide browser support for our React components.

> **Note**

>React uses *className* instead of the *class*. React.js DOM components expect DOM property names like className and htmlFor, rather than DOM attributes like class or for.


Virtual DOM
--------------------

React is very efficient at rendering to the DOM because it has the concept of a **virtual DOM**. A virtual DOM combines an in-memory representation of the actual DOM with a smart diffing algorithm which compares differences in the web application model.

React provides a series of Javascript methods that create an in-memory DOM tree and performs updates in-memory when data bound to it changes (determined by a smart diffing algorithm). Updating the virtual DOM is much quicker than updating the normal DOM directly. React does the hard work in the in-memory and then, once all the work is finished, renders the result in the normal DOM.

This optimization all happens behind the scenes. You can code your JSX, Javascript and event bindings without having to worry about interacting with the virtual DOM. You will just experience the normal DOM updating very fast.

React also only interacts with specific parts of the DOM that needs to change. React., unlike say Backbone, will not re-render whole sections of the DOM but just the necessary DOM nodes where the bound data has changed.

Smart diffing algorithm
---------------------------------------------------

Most popular web application frameworks (e.g. Angular 1.x, Backbone) follow a MVC architecture. The views re-render when the model changes. The changes are propagated by events emitted when the model changes. Models can have a one-to-many relationship with the views, and the views can have a one-to-many relationship to the models. 

This means a model change can be reflected in a number of views, and an event triggered in a view can change multiple models. This can lead to **spaghetti events**, i.e. code that is difficult to maintains and understand. An event can create unexpected consequences. It is also difficult to test larger MVC applications, as you have to mock all the model interations. 

The smart diffing algorithm allows you to create more functional approach to developing your application. You provide the previous state and the new state and let React do the hard work. You don't have to bind to model changes, just provide the new state and React will work out the best way to render this change to the DOM.

Props, state and context
------------------------

All React components use both props and state to communicate the data to be bound to the virtual DOM. **Props** and **state** can be JS objects,  functions or primitives (strings, numbers, booleans).

**Props**

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

**State**

**State** is defined within the React component. They maintain the internal state of the component. React components change their own internal **state** but not that of their child or parent React components (although state can be passed down as props to a component's children). 

State is mutable, i.e. state can be changed.

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

**Context**

**Context** provides you with the ability to pass data through the component tree without having to pass the **props** down manually. This has the advantage of you writing less code to achieve the same affect. The disadvantage is that **context** makes your components more coupled and less reusable. 

```javascript
class Parent extend Component () {
	
	static childContextTypes = {
	    item: React.PropTypes.string
	}
	
	getChildContext () {
	    return {
	      item: this.props.item
	    };
	}
	
	render () {
	    return (
	      <div>
	        <Child />
	      </div>
	    );
	}
}

```

We define a **childContextTypes** and **getChildContext()** which inform the context of all child React components (in this case the **Child** component).

```javascript
class Child extend Component {

	render() {
	    return (
		    <p>Item is {this.context.item}</p>
	    );
	}
	
}

Child.contextTypes = {
	item: PropTypes.string.isRequired
}
```

In the **Child** component we can we can reference the **items** which have been passed down via context. 

Isomorphic javascript
-------------------------

Isomorphic javascript JavaScript is shared code that runs on both the in the browser and on the server. React is isomorphic ready. It means you can use the same React component on for server side rendering and for client side rendering.

The advantages of server side rendering include:

 - On first page load, serve server-rendered HTML which is inflated with data. This is quicker than loading the HTML, pulling in the JS and then making requests back to the server for more data. It will increase the speed of your application when it first loads.
 - Search engine optimization is improved as crawlers can access the raw html to decide what your application does. It is provides the least resistance for getting your application indexed well in a search engine.
 - A server rendered React component can seamlessly become a client side rendered application after initial load. This retains all the advantages of client-side rendered apps (e.g. low data transfer between server and client, mobile optimization) 

**Client-side**

Client-side rendering of React component which creates a DOM element in the browser.
```javascript
ReactDOM.render(
    <Component />,
    document.getElementById('body')
);
```

**Server-side**

Server-side rendering of React component which creates a string which can be sent to the browser and parsed.
```javascript
React.renderToString(<Component />);
```
Later in the book we will look at how to create a Node server which will demonstrate how to serve this string representation of the your React component to the browser.

Common React methods
---------------------------- 

React has a number of methods and static variable available to help you creating your application. There are certain React methods that will use time and time again.

**constructor**
We need to augment the class constructor with the props that are passed down to the React component. If we don't do this then our React application won't be able to access the props. We should also set our React state in this constructor

```javascript
constructor (props) {
	super(props);
	this.state = {
		data : []
	}
} 
```

**Render**

Render is where all the JSX code is placed. The render method return the code that gets painted to the DOM. Render can also reference children React components.

```javascript
render () {
	return (
		<div>
			<ChildComponent />
		</div>
	)
}
```
**SetState**
**SetState** updates the state of the React Component. The method also invokes **render()** to paint the new state to the DOM.

```javascript
this.setState({
	data : ['one','two','three']
})

render () {
	return (
		<p>{ this.state.data }</p>
	)
}
```

**ComponentWillMount**

This is a lifecycle methods this is called before the component mounts on the DOM. This is useful for fetching or parsing data before the **render()** method is called.

```javascript
componentWillMount (){
	$.get(this.props.url, (data) => {
		this.setState({
			items : data
		})
	})
}

render () {
	return (
		<p>{ this.state.items }</p>
	)
}
```

**ComponentDidMount**

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

**PropTypes**

React allow you to define the props that you pass in to your react component. Proptypes make it easy for you to validate and document your React application.  A warning will appear in the console if you invalidate one of your props.

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


An example React component
------------------------------------

React components should not have many moving parts. In fact it is better to keep your React components simple. You should always look to make your React components to do as little as possible which will aid in make them re-usable throughout your applications.

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
We create our **Counter** component by extending the React component class. This make all the baked in React methods available in your new component.

We define the component **state** in the class constructor. We use the **super** method to inherit any other **props** that might be passed down to the **counter** component. The only **state** we are concerned with is the **count** which we initially set to the value of the **start** prop.

Next, we define a click handler called **increment()** which will update our **count** state. We use the React method **setState()** to update the new count value. **SetState()** will automatically make the **render()** method re-invoke. Therefore, the DOM will automatically update with the new count value when it is changed.

We define our **render()** method. React component's expect there to be a **render()** method defined. This **render()** method informs the virtual DOM on how to map changes to bound data to the DOM. We use curly brackets ({}) to inject the **count** state value in to the DOM.  

**Render()** also provides a way of binding events to the DOM. We have used the **onClick** even handler to bind the **increment()** method to a click on the button.

Finally we inject the component in the the body of our HTML document. **ComponentDidMount()** will fire and console out the message "mounted".

> **Tip**
> 
> The onClick method uses a double colon (::) **Bind Operator** to provide context mapping to our **increment()** method. This makes the **this** in the **increment()** method to have the correct context and map to **setState()**

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

There are two kinds of components that can be created. **Stateless** and **stateful** components.

**Stateless Components** (or dumb components) contains only props, no state. All the logic and handlers are provided props they receive from a **stateful component**. The majority of rendering and formatting logic happens in **stateless components**.

**Stateful Components** contain both props and state. They manage the applications state and provide handlers for children **stateless components**.  A **stateful component** generally handles client to server communication (e.g. XHR, web sockets).

Your application will be made of a small number of **stateful components** and a larger number of **stateless components**. The aim is to keep all the state management in as few places as possible.

You can create simpler applications just by creating a collection of React components that manage their own state. This can become difficult to work with as your application grows.

**Flux Architecture**

Flux is a code architecture to structure larger React applications. Flux architecture aim is to remove state management outside your React components.

Flux was developed by Facebook as a way to move away from the more standard MVC (model-view-controller) towards an architecture with an uni-directional (one-way) data flow.  

```javascript
//MVC
model <-> view

//Flux
store -> view -> action -> dispatcher -> back to store
```

The MVC approach meant that the view could change a model and the model change a view, this could create **spaghetti events** that are difficult to debug. It is possible to use Javascript frameworks like Backbone or Angular (1.x) to use React for the view components and follow MVC patterns. This can work well in certain applications. 

The Flux approach, however, enforces the rule that the view never informs the model/store. A view, dispatcher and store have distinct inputs and outputs. It is a more functional approach to coding that relieves on an immutable data store and the props of a React Components to pass down the new state. This can help you produce more deterministic, and thus easier to maintain applications. 

Flux manages your state by passing **actions** through props to your components. These actions are **dispatched** via handlers. This creates a new **store** informed from the received **action**, which is passed back to the component for binding with the DOM.

**Store**

A **store** is just a simple object literal. It has no listeners bound to it (like a model).

```javascript
const store = {
	items : [],
	lastUpdated : ''
};
```

It gets amended when a **dispatcher** interacts with it.

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
An action will always have at least a type and a value but can have additional parameters.

**Dispatcher**

The **dispatcher** manages data flow in your application. It provides a bridge between the **store** and the **actions**. It has no logic of its own. The dispatcher uses the **type** of the action to inform the store what it should do with the **value**. 

Whilst you could create all your own flux management code, there are a number of libraries that provide helper methods and scaffolding to make your Flux architecture applications. These include:

 - Fluxxor
 - Redux
 - Alt

Each follows the same paradigms but have different ways of implementing flux. It is worth reading about which suits the application you are trying to build.


Todo React Web Application
----------------------------------------

Before we start, we need to have a base index.html page to instantiate our React application.

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
We include React and also a JSX transformer script. We can do JSX transformation as a build step (which we will demonstrate in the next chapter) but we will add a javascript shim here for brevity. We also have a container element which will contain the React application.

We provide a **text/jsx** type for our script which is used by the JSX Transformer. This can be removed when we have our JSX transpliation as part of the build tools. 

**Creating the Todo Container**

First, we create a **TodoContainer** React component. This will be our parent React container and instansiate all the children React components of our application. **TodoContainer** is our smart component as it has **state**.

```javascript
import React, {Component} from 'react';
import TodoInput from './TodoInput';
import TodoList from './TodoList';

class TodoContainer extends Component({
    
    constructor (props) {
        super(props);
        this.state = {
            items : this.props.items
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
                <h1 className="todo-title">{this.props.title}</h1>
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
	title : React.PropTypes.string,
	items : React.PropTypes.array
}

ReactDOM.render(
    <TodoContainer 
	    title='Todo List' 
	    items=['get milk', 'walk the dog']  
	/>,
    document.getElementById('container')
);
```

We extend a React class to create a **TodoContainer** parent component that takes a **title** and **items** props. The **render()** method paints the **title** and invokes two React Components called **TodoList** and **TodoInput**.

We create the application state in the parent which contains the **items** array and also the handler methods (**addListItem()**, **removeListItem()**) for the state. These are passed down as props to the children components.

We inject **TodoContainer** in to the container element with the **title** set as "Todo List".

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

The **validateInput()** method validates that the inputed todo is not an empty string before passing it through the **addItem** handler which updates the items array state in the parent **TodoContainer**. We have introduced the **this.refs** locator which allows your react component to pick out a DOM element which is decorated with a **ref** attribute.

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

The **ListItems** are iterated through when the component is instantiated in the DOM. Clicking on the list element removes the item from the items array state in the parent **TodoContainer**.


Loading data into React
----------------------------

We can fetch data from external resources to populate our react components. React doesn't care how we provide it with date. We can provide inline data or, fetch data using http request or web sockets.  

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
				<li className="todo-list-item">{person.name} {person.surname}</li>
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
In the example, use JQuery's ajax methods to fetch random names to populate a React component.

**ComponentWillMount** and **ComponentWillUnmount** are lifecycle methods native to React. The first is called before the React component writes to the DOM and the latter when the component is removed from the DOM.

We request the **persons** data via **$.get()** in **ComponentWillMount** and we then set the state of the component. This request happens before component mounts and the will re-render the list items when the request is successful.

We map the **persons** array to return **li** elements that we inject into the DOM. React tracks what data is bound to which **li** element.

We can tidy the request object up when we unmount the component by invoking **abort()** in **ComponentWillUnmount()**.

Testing React Components
-------------------------------------

We should be testing all our components to give us confidence when developing and deploying applications. Testing React components is made easy with React's Test Utilities. 

**Components to be test**

We can create React components in the Virtual DOM and then simulate interacting with these components. We can mock data, interactions and how the component would render in the DOM.
 
 - The rendering of a React component given a particular state.
 - The behaviour of a React component and how it affects the state.
 - The state or the application (the default values and expected state)

The rendered React Component uses behaviour to amend state which affects the rendered Component. You should cover all this in your tests to provide you app with extensive test coverage. 

 - All components will be rendered. Thus you will need rendering tests for each component.
 - Some components will have events bound to them which will affect the state. Thus you will will need behavioural tests for all components with bound events.
 - State can be interacted with by multiple components. Smart components manage this state (or in the case of Flux, the store). We need to make sure we understand how the state should change with both interactions from events but also from data fetched from external sources.

**Test harnessing frameworks**
We can't test our components just using React TestUtils alone. We need an assertion framework (**expect**), a reporting framework (**mocha**) and a headless browser environment to instantiate our components (**JSdom**).

**Setup Tests**

We need to create **NPM** script to run our tests. We shall cover **NPM** and **Node** in detail in our next chapter.  Our NPM script just allows us to run our test from the **command line** or to automate our testing in a continuous integration solution.

Don't worry too much about how this works at the moment, it will be described in more detail in the next chapter. For the moment let us just understand how to write our React tests.

We need to create an entry script called setup.js which starts **JSDom** (our headless browser).

```javascript
//setup.js
import jsdom from 'jsdom';

global.document = jsdom.jsdom('<!doctype html><html><body></body></html>');
global.window = document.parentWindow;
```

This script just creates a fake DOM for us to place our React component in. It is like having an index.html page served by a web server but much quicker as it only exists in memory.

**Global** is a **Node** enviroment variable that does a similar function as **window** in the browser. We copy the **window** object to **global** so that is can be accessed and used in your tests.

When **mocha** (our test reporting framework) runs our tests, it pulls in the **setup.js** first before our tests. The complete setting up of your test environment will be documented in the next chapter.

```
/tests
    - setup.js
    /TodoContainer
        - behaviour.spec.js
        - state.spec.js
        - render.spec.js
```

We arrange our tests by component and suffix the name with **.spec.js** . This is just a naming convention but it highlights what files contain tests and which contain app related code. It also means we can **glob** (search by name) the test files easily to include them in our test harness. 

**Render Test** 

We are going to test the **TodoContainer** we built earlier.  First we look at how our component renders. We are interested the DOM structure and that it instantiates correctly.

```javascript
//render.spec.js

import React from 'react';
import addons from 'react/addons';
const TestUtils = React.addons.TestUtils;
import expect from 'expect';
import TodoContainer from './TodoContainer';

describe('TodoContainer render',() => {
	it('Component elements should exist',() => {
	});
});
```

We include our React component, the **TestUtils** from React and the **expect** framework for making assertions. 

The **describe()** and **it()** functions are parsed by **mocha** to produce test reporting in the console. **Describe()** provides descriptive and grouping context to your tests and **it()** is the individual tests themselves.

```javascript
describe('TodoContainer render',() => {

	const items =  ['get milk', 'walk the dog'];
    const title = 'New List'

    before('render and locate element',() => {
    
	    this.renderedComponent = TestUtils.renderIntoDocument(
	    	<TodoContainer title={title} items={items} />
	    );
    
        this.todos = TestUtils.findRenderedDOMComponentWithClass(
	        this.renderedComponent,
	        'todos'
	    );
	    
        this.todoInput = TestUtils.findRenderedDOMComponentWithClass(
	        this.renderedComponent,
	        'todo-input'
	    );
    
        this.todoTitle = TestUtils.findRenderedDOMComponentWithClass(
	        this.renderedComponent,
	        'todo-title'
        );
    
        this.todoItems = TestUtils.scryRenderedDOMComponentsWithClass(
	        this.renderedComponent,
	        'todo-list-item'
        );
    
    });
    
});
```

We next create a **before()** function that is run before each of our tests.  We render **TodoContainer** into the Virtual DOM and then pick out the elements that we are interested in testing. 

**FindRenderedDOMComponentWithClass()** finds one element buy className and **scryRenderedDOMComponentsWithClass()** find multiple elemtents by className.

Our test suite is now ready to run assertions with **expect**.

```javascript
   it('Component elements should exist', () => {
	    expect(this.todos).toExist();
	    expect(this.todoItems).toExist();
   });
 
   it('title should be "' + title+ '"',() => {
	   expect(this.todoTitle.textContent).toBe(title);
   });
 
   it('There should be "' + items.length+ '" list items',() => {
       expect(this.listItems.length).toBe(items.length);
   });
 
   it('The list item names should be Correct',() => {
	   expect(this.listItems[0].textContent).toBe(items[0]);
	   expect(this.listItems[1].textContent).toBe(items[1]);
   });

```

We have tested that our components main container exists and then we test the content of those containers.

If these tests pass then we know with confidence that our component will render the correct items, if it is give the correct props.

**Behaviour test**

We put our behaviour tests in a new file called **behaviour.spec.js**. We have the same imported files and the same **before()** function as our **render.spec.js** tests.

Behaviour tests are to look at how a user would interact with our React component. We will be looking at adding and deleting the todo items.

```javascript
//behaviour.spec.js

describe('Todo Behaviour ', () => {

	...before()...

	it('click to li to add todo item', () => {
		const input = this.todoInput.querySelectAll('input');
		const btn = this.todoInput.querySelectAll('button');
		input.value = 'wash car';
	    TestUtils.Simulate.click(btn);
	    expect(this.listItems.length).toBe(3);
	    expect(this.listItems[2].textContent).toBe('wash car');
	});
	
	it('click to li to delete todo item', () => {
		expect(this.listItems[0].textContent).toBe('get milk');
	    expect(this.listItems.length).toBe(2);
	    TestUtils.Simulate.click(this.listItem[0]);
	    expect(this.listItems.length).toBe(1);
	    expect(this.listItems[0].textContent).toBe('walk the dog');
	});
	
});
```

We create a new todo called 'wash car' in the first test but simulating the input value and click. 

The second test is reset by the **before()** method (i.e. the 'wash car' no longer exists). In the second test, we delete the 'get milk' item by simulating a click on the list item.

We have confidence that our user interactions work correctly. Next we look at the state of our React component.

**State test** 

Finally, we test that the state is correct on the initialising our component. We test on state changes  by firing the handler methods that touch our state. Our Todo components state interaction all exist in the smart component (.i.e. our parent **TodoContainer** component).

```javascript
describe('Todo State', () => {

	before()...

	it('Correct default state', function() {
	    expect(this.renderedComponent.getState().items).toExist();
	});

	it('Default state to instantiate with...', function() {
	    expect(this.renderedComponent.getState().items.length).toBe(2);
	    expect(this.renderedComponent.getState().items[0]).toBe('get milk');
	    expect(this.renderedComponent.getState().items[1]).toBe('walk the dog');
    });

	it('addListItem state change', function() {
	    this.renderedComponent.addListItem('wash the car');
	    expect(this.renderedComponent.getState().items.length).toBe(3);
	    expect(this.renderedComponent.getState().items[2]).toBe('wash the car');
	});
	
	it('removeListItem state change', function() {
	    this.renderedComponent.removeListItem('get milk');
	    expect(this.renderedComponent.getState().items.length).toBe(1);
	    expect(this.renderedComponent.getState().items[0]).toBe('walk the dog');
	});

});
```

We have now tested our state is correct when instansiated from props. We also test that our state handling methods of **addListItem()** and **removeListItem()** correctly change the state.

**Using tests to help build better React components**

Breaking up your tests mean you can concentrate on building your understanding of your application before creating React Components.

You can create your different application states and define your handler methods (i.e. **addListItem**, **removeListItem**) first. You test these before committing to building your components. Therefore you are building test for your **smart components** first.

Once you know your states, then you can mock out your **render tests**. You will know all the possible states of your component and can render test against them. You Todo app can have some or no list items, it has a title and it always has a input field and button. We test that these all exist and that the content is correct in relation to the state.

Finally you test the bound events which fire your handler methods. The final part of your tests will be the **behaviour** of your component. You are testing the resultant DOM after a component event has been triggered.

Summary
-----------

In this chapter we have looked at React Components and why they we were created. We have looked at how structure our React applications, how to test them and coding paradigms that we should follow.

We have introduced:

- The **smart diffing algorithm** and **virtual dom** which makes React very efficient at rendering and binding data to the DOM.
- How to use **JSX** as a markup language to create your HTML.
- The difference between **props** and **state**.
- **Isomorphic** Javascript and it's advantages  of performance, search engine indexing and common code base.
- **Flux** architecture to help you create larger React applications.
- Loading data into our React components from external resources.
- Testing our React components

In the next chapter, we will look at how to create server-side Javascript and the frameworks that are available to us. We will build a simple web server and a API for storing information into a NoSQL DB.