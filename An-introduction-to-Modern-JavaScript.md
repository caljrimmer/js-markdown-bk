Introduction to Modern Javascript
===========================

You can code any sort of application, to run on nearly any device when you build it with Javascript.  This book is to show you how to create, build, test and deploy your own application using just javascript.

A modern Javascript developer can create any application, on any device. From the first line of code to deployment to live environment, javascript developer never has to utilise any other language.  Modern javascript isn't just about the latest revisions of the language but a fundamental shift in simplifying how a developer can create, test and deploy applications.

Javascript, released in 1995, was developed as a way to run scripts within a website. In its early days some derided the language as being simple and lacking the power and sophistication to be taken seriously. Javascript has evolved with the internet and the language has be improved over the years. 

Javascript, once just used for simple client-side scripting on web sites can now be used to develop games, create mobile applications, web applications, desktop applications, sophisticated data visualisation, complex animations and run intensive computations.


> **ES6**

>The latest version of Javascript,  ECMAScript 2015, also known as ES6, is a significant update to the language. It was the first update to the language since ES5 was standardised in 2009. All code examples in this book will utilise ES6 where appropriate. 
 
 

1.  Javascript in the Browser
---------------------------------

JavaScript is designed to run as a scripting language in a host environment. The most common host environment is a **browser**.

 Javascript can be run on any **browser**. We will be using **Chrome** as our browser of choice. Chrome has a number of developer tools that will help you develop your code. One of those tools is called **Console** and it that allows you to run Javascript directly.

To begin:

 1. Open the Chrome browser
 2. Right click and select "Inspect", and then click on "Console" tab

You now have the **Chrome** developer tools open and we can write and test our first bit of Javascript.

Let's try creating a simple pop-up with the text "hello".
 
```javascript
window.alert('hello');
```
The **window** object is where all native global JavaScript objects, functions, and variables reside in the browser. The **window** object is globally available (it is accessible from anywhere in your code). The **alert** is a function that Javascript provides to allow you to easily create pop-ups. 

A **function** in javascript is invoked with parentheses and inside the parentheses arguments can be passed.  We use a semicolon to separate statements. 

Now let's make a simple function to capture a user's response and return the value.

```javascript
function result (message) {
	return window.confirm(message);
}
result('Do you confirm this action?');
```

The console should log *true*, if ok is clicked and *false* if cancel is clicked.

So we have create a new function called **result** that returns a value that we get from another native javascript function called **confirm**. We then invoke our result function with parentheses whilst passing a string of 'Do you confirm this action?' as an **argument**.

We don't need to specify **window** when calling functions. Javascript will assume it for you. Thus these two function do the same thing.

```javascript
window.alert('hello');
alert('hello'); //Same as window.alert

window.confirm('confirm?');
confirm('confirm?'); //Same as window.confirm
```

Time to look at **data types**.  There will be code example for each which you can use **Console** in **Chrome** to verify and experiment with.

2. Data Types 
-----------------------------

Javascript allows you to define a data type of values that you define. This means you can tell Javascript whether a value is, for example, a **number** or **string**. 

Javascript, once a data type object is defined, makes available a number of different prototypal **methods** for that data type. 

A **method** is very similar to a **function** but it exists on the data type object rather than independent of it. These methods help you do operations on that particular data type.

In JavaScript there are three primary data types **String**,  **Boolean** and **Number**, three composite data types  **Object**, **Date** and **Array**, and two special data types **Null** and **Undefined**.

**2.1 Primary data types**

```javascript
//Number
const age = 16; 
const count = new Number('16');

//String
const name = "Ted";
const country = new String('USA');

//Boolean
const isChecked = true;
const isOpen = new Boolean ('true');
```

**2.1.1 Strings** 

```javascript
const word = "marvellous";
//or
const word = new String("marvellous");

word.length; //returns 10
word.toUpperCase(); //returns MARVELLOUS
word.substr(0,5);//returns marve
```

To create a string data type, we declare a variable wrapped in either double (") or single quotes ('), or we can use the **String()** function.

 In the example above, we use **length** to get the number of characters in a string, **toUpperCase()** to return the string in uppercase characters and **substr()** to return a the first 5 characters.

**2.1.2 Booleans**

```javascript
let value = false;
//or
let value = new Boolean('false');

function toggleChecked (isChecked) {
	if (isChecked) {
		return false;
	} else {
		return true;
	}
}
//or short-hand using a ternary operator
function toggleChecked (isChecked) {
	return (isChecked) ? false : true;
}

value = toggleChecked(value) // value is false;
value = toggleChecked(value) // value is true;
```

To create a **boolean** (i.e. true or false) data type, we declare a container of either true or false, or we can use the **Boolean()** function. 

**Booleans** are often used in Javascript. In the example, we are using them to toggle a value (i.e. hide or show, done or not done, etc.).

**2.1.3 Numbers**

```javascript
const total = 9;
//or
const total = new Number('9');

const price = 11.99;

Number.isInteger(total) // returns true;
Number.isInteger(price) // returns false;
Math.sqrt(total); //returns 3
Math.ceil(price); //returns 12
Math.floor(price); //returns 11
```

To create a **number** data type, we declare a container of either an integer or a decimal, or we can use the **Number()** function.

We then have the ability to perform numerical or mathematical functions and methods on the value.  In the example above we use **isInteger()** to determine if value is an integer, **Math.sqrt()** to return the square root of a value, **Math.floor()** to round down to the nearest integer and **Math.ceil()** to round up to the nearest integer.

Javascript allows us to replicate most mathematical computations. 

```javascript
function add (a,b) {
	return a + b;
}

function subtract (a,b) {
	return a - b;
}

add(1,2) //returns 3
subtract(2,1) // returns 1

```
We have created functions to **add** and **subtract** two operands (a and b).  When we invoke the function, a new calculated value is returned.

If we tried to pass a string as an argument:

```javascript
add('name',3) // returns 'name3'
subtract('name',3); // returns NaN
```

Javascript stops behaving predictably if we mix data types. With **subtract**, it returns **NaN** (i.e. Not a Number) and with **add**, it returns a new string of the 'name' with a suffixed '3'.

We can only do numeric or mathematical work on Number data types.

**2.2 Composite data types**

```javascript
//Object
const person = { 
	name: 'Ted',
	age : 16
};

//Date
const today = new Date();

//Array
const colors = ["red","blue","green"];
const fruits = new Array("apple","orange","banana");
```

**2.1.1 Objects**

```javascript
const object = {
	name : "Ted",
	count : 1,
	isChecked : true,
	list : ['blue','red','yellow'],
	addToCount : function () {
		return ++this.count;
	},
	nested : {
		colour : "blue"
	}
}

object.addToCount(); //returns 2
object.addToCount(); //returns 3

object.hasOwnProperty('count'); //returns true
object.hasOwnProperty('notThere'); //returns false
```
To create a **object** data type, we declare a container with curly brackets {}. Inside the object you can define values of any sort of data type. The values are written as name:value pairs (name and value separated by a colon). This is called an **object literal**. **Object literals** encapsulate data, enclosing it in a tidy package.

In the example above we have defined an **object** with a string, number, boolean, another object and also a function.

Notice that in the function, we reference the object with the **this** keyword. The **this** keyword is very useful in Javascript. It allows us to be **self-referential** (refer to different parts of the same object).

The defined object is also **stateful**. In the example, we can increment the **count** value by invoking the **addToCount()** function. The defined object remembers what the internal values as long as it exists.

An object data type also has it's own prototype methods. In the example above, we use the **hasOwnProperty()** method to check what values the object contains.

ES6, the latest Javascript engine, has give us additional ways of defining an **object literal**.

```javascript
const keyName = 'surname';
const newObject = {
    value, // Shorthand for value: value
    add(a,b) { // Shorthand for functions
     return a + b;
    },
    [keyName]: 'Smith' // dynamic key names
}
```

We can amend **object literal** values at any time. We can also add or remove values.

```javascript
let amendable = {
	name: 'Ted'
	age: 32
}

amendable.name = 'Edward'; //name value is now Edward
amendable.job = 'Accountant'; //adds job key and value

delete amendable.age; //removes age key and value
```

**2.2.2 Dates**

```javascript
const today = new Date();
const christmas = new Date('12/25/2015');

today.getDate() // returns date of today (i.e. 1-31);
today.getMonth() // returns month of today (i.e. 1-12);
today.getHours() // returns hour of today (i.e. 0-23);
```

To create a **date** data type, we declare a container with the **Date()** function. 

We then have the ability to perform date operations on the data type.  In the example above we use **getDate()** to return the date of today, **getMonth()** to return the month of today, **getHours()** to return the hour of today.

We also can define a date in the future or past by passing a date to the **Date()** function. We must pass the date in the US format (i.e. month before day).

**2.2.3 Array**

```javascript
const strings = ['blue','red','yellow'];
const numbers = [20,30,40];
const mixedList = [1,'blue',false];

//or
const numbers = new Array(20,30,40)

strings.length; //returns 3

numbers.map((num) => {
	return num / 10; 
}); //returns [2,3,4]

mixedList.forEach((item) => {
	console.log(typeof(item)) 
}); //returns number, string, boolean
```

To create an **array** (i.e. a list) data type, we declare a container with square brackets [], or we can use the **Array()** function. Inside the **array** you can define values of any sort of data type. The values are separated by commas.

In the example above we have defined an 3 different **arrays**. One with string data types, then number data types and finally a mix of different data types.

Arrays have many prototype methods to help you work with them. You are able to count the items in an array with **length**, to loop through **arrays** with **forEach()** or even transform the values of an array with **map()**.

Arrays can be used to create lists of objects:

```javascript
const collection = [
	{id:1, name:'Ted'},
	{id:2, name:'Fred'},
	{id:3, name:'Ned'}
]
```
When an we have **array** of objects, particularly if they have been return from a database, then we can refer to the array as a **collection** and the objects as **models**.

**2.3 Special data types**

```javascript
const value;
console.log(value); //returns undefined

const nullValue = null;
console.log(nullValue); //returns null
``` 

The **null** data type is the absence of other valid data types. You can remove the contents of a variable (without deleting) by assigning it the null value.

The **undefined** data type when a variable that has been declared but no value is assigned to it.

**2.8 Javascript is Loosely Typed**

Javascript is loosely typed. This means you can change the data type of a defined container at anytime. Most programming languages do not allow you to do this. 

```javascript
var changeable = 1; //Data type is a number
changeable = 'Ted'; //Data type is now a string
```
In the example, we change the variable **changeable** to not just have a different value but also to have a different data type. It is advisable, even though you can, not to change your data type whilst drafting your code. It can be confusing to maintain and extend your code.

3. Variables
--------------

Javascript allows us to define variables to store data types or functions. Variables allow us to structure our code and to manage **scope**. **Scope** is the ability to access functions or variables from within our code. 

There are 3 ways to define a variable. **Var**, **let** or **const**. All variables must be identified with unique names.

**3.1 Define a var**

```javascript
var z;
var x = 1;
var y = 2;
z = x + y; // z equals 3 now
```

You can define a **var** with a value or without a value and populate it later. A **var** exhibits **functional** and **global** scoping. We will discuss scope later in the book.

**3.2 Define a let**

```javascript
let sentence;
let name = "Ted";
sentence = "My name is " + y; // sentence equals "My name is Ted"
```

Defining **let** is similar to a **var** declaration. **Let**, unlike **var**, cannot be **hoisted** and it also exhibits **block** scope as well as **functional** and **global** scope. We hoisting later in the book. 

**3.3 Define a const**

```javascript
const PI = 3.14;
```

Defining a **Const** means the value can not be changed. It is used, as it's name suggests, to define constants. **Const**, like **let**, also cannot be hoisted and it exhibits block scope as well as **functional** and **global** scope.

**3.3 Define globally**

```javascript
name = 'Ted'; //same as window.name = 'Ted'
x = 1; //same as window.x = 1
```

It is possible to declare a variable without using **var**, **let** or **const**. This will set the variable to the **global** scope, which means the variable is available everywhere in your application. 

Defining a variable to the **global** scope is a bad practice as it easy for the variable to be overwritten and it can make your code less maintainable and testable.

Declaring a container this way adds the container on to the window object and it becomes globally available. This is considered bad practice because relying too much on global containers can result in collisions between various scripts on the same page.

4. Operators
------------------

**4.1 Comparison Operators**

Comparison operators are used in statements to determine equality or difference between values. The response is generally a **boolean** (i.e. true or false).

Operator | Description 
------- | -------------
== 		| Equal  
===   	| Equal to value and data type
!=    	| Not Equal
!==   	| Not Equal to value and data type
>    	| Greater than
\>=    	| Greater than or equal to
<    	| Less than
<=    	| Less than or equal to  
?    	| ternary    

```javascript
const x = 2;

x == 2;  //returns true
x == '2';  //returns true (only checks value not type)
x == 3;  //returns false

x === 2;  //returns true
x === '2';  //returns false (checks values and type)
x === 3;  //returns false

x != 2;  //returns false
x != 1;  //returns true

x > 1;  //returns true
x > 2;  //returns false

x >= 1;  //returns true
x >= 2;  //returns true

x < 2;  //returns false
x < 3;  //returns true

x <= 2;  //returns true
x <= 3;  //returns true

(x === 2) ? 'option 1' : 'option 2' // returns option 1
(x !== 2) ? 'option 1' : 'option 2' // returns option 2

```

The **ternary** operator (.i.e. **?**) reacts to the previous comparision statement to return a result. In the example above, if the statement before the **ternary** operator is true, then the first option is returned, if it is false, then the second option is returned.

```javascript
const x = 5;
(x === 5) ? 'option 1' : 'option 2' // returns option 1
(x !== 5) ? 'option 1' : 'option 2' // returns option 2

function toggleOn(booleanValue) {
	return (booleanValue) ? 'on' : 'off'; 
} // returns on if true, off if false

```

**4.2 Logical Operators**

Logical operators are used to combine comparison operators. The response is generally a **boolean** (i.e. true or false).

Operator | Description 
------- | -------------
\|\|    | or 
&&    	| and 
!    	| not

```javascript
const name = 'Ted';
name === 'Fred'; //returns false
(name === 'Ted' || name === 'Fred'); //returns true
(name === 'Ted' && name === 'Fred'); //returns false
!(name === 'Fred'); //returns true

const x = 10;
(typeof(x) === 'number' && x === 10); //returns true
```

Logical and comparison operators are often used with **if()** and **switch()** statements

```javascript
function yourTeam (colour) {
	if (colour === 'red') {
		return 'Your team is Liverpool';
	}else if (colour === 'blue') {
		return 'Your team is Everton';
	}else{
		return 'No suggestion of your team';
	}
}

//or

function yourTeam (colour) {
	switch (colour) {
		case 'red':
			return 'Your team is Liverpool';
			break;
		case 'blue':
			return 'Your team is Everton';
			break;
		default:
			return 'No suggestion of your team'; 
	}
}

yourTeam('red') // returns Your team is Liverpool
yourTeam('blue') // returns Your team is Everton
yourTeam('green') // returns No suggestion of your team
```

5. Creating a simple calculator web application
-----------------------------------------

A web application consists of **HTML**, **CSS** and **Javascript**. 

**HTML** provides the scaffolding of the page. **HTML** provides a library of tags that are used as containers for content. **HTML** also links to **CSS** and **Javascript** files.

**CSS** provides the styling of the page. **CSS** associates styles to **HTML** tags.  **CSS** can amend fonts, colours, margins, padding, height, width, images and positions. It can also provide provide animation.

**Javascript** is what makes a web page dynamic and responsive to the user. **Javascript** turns static content in to a tool. It allows the creation of applications to create whatever is desired. It turns a website into a web application

**5.1 Get Started** 

To make a web application, we will need a text-editor to write the code. Any text editor would work (i.e. Notepad or TextEdit) but there are a number of excellent free options that will help in drafting code more efficiently. The best free options are:

 - Atom - https://atom.io/
 - Sublime - http://www.sublimetext.com/
 - Brackets - http://brackets.io/

Next, we  create a new directory to store our web application files in. Let us name it **example-web-page** and save it. Create two files called **index.html** and **script.js**

Create and save **index.html** with the following content:
```html
<html>
	<head>
		<title>Web Application</title>
	</head>
	<body>
		<div id="container"></div>
	</body>
	<script src="script.js"></script>
</html>
```
The **HTML** contains a **div** called with id of **container**. This will hold our web application. We have used the **title** tag to name our web application.

The **script** tag is placed near the bottom of the HTML file. This is because all the HTML needs to be loaded before the Javascript is parsed.

Create and save **script.js** with the following content:

```javascript
function render (id, msg) {
	const el = window.document.getElementById(id);
	el.innerHTML = msg;   
}

render('container','Hello World');
```
To view the web application, click on the **index.html** file to open it in a browser. The web app will render 'Hello World' in the browser.

In the **script.js** we have created the **render()** function which takes two arguments. The first selects where in the HTML we want the message to appear. The second is the message itself. The **window.document.getElementById** function locates any element in the HTML by its ID. We can then set the element's content using **innerHTML**.

**5.2 Adding inputs**

We now updated the **index.html** with form fields to capture information provided by the user. This will provide the information we need for the calculator.

```html
<html>
	
	<head>
		<title>Web Application</title>
	</head>
	
	<body>
		<div id="container">
			
			<form>
				<input id="operand-a" type="text" value="0" />
				<select id="operator">
					<option value="add">Add</option>
					<option value="subtract">Subtract</option>
					<option value="multiply">Multiply</option>
					<option value="divide">Divide</option>
				</select>
				<input id="operand-b" type="text" value="0" />
			</form>
			    
		</div>
	</body>
	
	<script src="script.js"></script>
	
</html>   
```

The **input** elements capture free-typed information and the **select** is a drop down that gives the user limited options to choose from. The **inputs** will provide the calculator with our two operands (number) and the **select** will provide our operator (i.e. add, subtract, etc.)

```javascript

function render (id, msg) {
	const el = window.document.getElementById(id);
	el.innerHTML = msg;   
}

function getSelectValue (id) {
	const el = window.document.getElementById(id);
	return el.options[el.selectedIndex].value;   
}

function getInputValue (id) {
	const el = window.document.getElementById(id); 
	return el.value;   
}

getSelectValue('operator') // returns add
getInputValue('operand-a') // returns 0
getInputValue('operand-b') // returns 0   

```

We have created 2 new functions in **script.js**. The **getInputValue()** function returns the value of the input field and the **getSelectValue()** function returns the value of the selected drop-down option.

We now have functions to both collect information and render information in our web application. Next, we shall make the web app responsive

**5.3 Adding responsiveness**

```html
<html>
	
	<head>
		<title>Web Application</title>
	</head>
	
	<body>
		<div id="container">
			
			<form>
				<input id="operand-a" type="text" value="0" />
				<select id="operator">
					<option value="add">Add</option>
					<option value="subtract">Subtract</option>
					<option value="multiply">Multiply</option>
					<option value="divide">Divide</option>
				</select>
				<input id="operand-b" type="text" value="0" />
				<button id="calculate">Calculate</button>
			</form>
			
			<div id="result"></div>
			    
		</div>
	</body>
	
	<script src="script.js"></script>
	
</html> 
```

We have create two new elements. The first is a div with id of **result** which will contain the result of the calculation. The second is a **submit** input which we shall use to trigger the calculation.

```javascript
function render (id, msg) {
	const el = window.document.getElementById(id);
	el.innerHTML = msg;   
}

function getSelectValue (id) {
	const el = window.document.getElementById(id);
	return el.options[el.selectedIndex].value;   
}

function getInputValue (id) {
	const el = window.document.getElementById(id); 
	return el.value;   
}

function getInputValue (id) {
	const el = window.document.getElementById(id); 
	return el.value;   
}

function getAll (e) {
	e.preventDefault();
   	const a = getInputValue('operand-a');
	const b = getInputValue('operand-b'); 
	const operator = getSelectValue('operator');
	render('result', a + operator + b);
}

function listenToClick (id) {
	const el = window.document.getElementById(id); 
	el.addEventListener('click', getAll);
};

listenToClick('calculate');
``` 
We have created a **listenToClick()** function to utilise **addEventListener** which binds the a click event on the **calculate button**. When clicked, the **getAll()** function grabs the values from the **inputs** and **select**, combines them and then uses **render()** to write the value to the **result** div.

The **preventDefault()** function prevents the browser defaulting it's default behaviour, which is to post the form and reload the page. The **e** we have passed as an argument comes from **addEventListener** 

**5.4 Calculation functionality**

```javascript
function render (id, msg) {
	const el = window.document.getElementById(id);
	el.innerHTML = msg;   
}

function getSelectValue (id) {
	const el = window.document.getElementById(id);
	return el.options[el.selectedIndex].value;   
}

function getInputValue (id) {
	const el = window.document.getElementById(id); 
	return el.value;   
}

function getInputValue (id) {
	const el = window.document.getElementById(id); 
	return el.value;   
} 

function calculate (a,b,operator) {
	a = new Number(a);
	b = new Number(b);
	switch (operator) {
		case 'add':
			return a + b;
			break;
		case 'subtract':
			return a - b;
			break;
		case 'multiply':
			return a * b;
			break;
		case 'divide':
			return a / b;
			break;
		default:
			return false
	}   
}

function getAll (e) {
	e.preventDefault();
   	const a = getInputValue('operand-a');
	const b = getInputValue('operand-b'); 
	const operator = getSelectValue('operator');
	render('result', calculate(a,b,operator));
}

function listenToClick (id) {
	const el = window.document.getElementById(id); 
	el.addEventListener('click', getAll);
};

listenToClick('calculate'); 
```
After our final edits to **script.js**, the simple web app is now complete. The final **calculate()** function takes three arguments of a, b and operator. The **switch** statement chooses the correct operation based on the operator name. The **Number()** function converts a and b from string data type into a number data type so that calculations can be performed. The resultant value is then returned.

To view the web application, click on the **index.html**. Enter two numbers either side of the operator and click on the **calculate button**. The calculated value should be rendered on the page.

**5.5 Refactoring**

Refactoring means that we tidy and minimise our code. It is important to try and limit repetition in your Javascript code. Your code should also be easy to read and re-useable. 

```javascript
const app = {
	
	find: function (id) {
		return window.document.getElementById(id);
	},        
	
	render : function (id, msg) {
		const el = this.find(id);
		el.innerHTML = msg;	
	},
	
	getValue : function (id, type) {
		const el = this.find(id);
		if (type === 'select') {
			return el.options[el.selectedIndex].value
		}else{
			return el.value; 
		} 
	},
	
	calculate : function (a,b,operator) {
		a = new Number(a);
		b = new Number(b);
		switch (operator) {
			case 'add':
				return a + b;
				break;
			case 'subtract':
				return a - b;
				break;
			case 'multiply':
				return a * b;
				break;
			case 'divide':
				return a / b;
				break;
			default:
				return false
		}   
	},
	
	getAll : function (e) {
		e.preventDefault(); 
		const result = this.calculate(
			this.getValue('operand-a', 'input'),
			this.getValue('operand-b', 'input'),
			this.getValue('operator', 'select')
		);
		this.render('result', result);
	},
	
	listenToClick : function (id) {
		const el = this.find(id); 
		el.addEventListener('click', this.getAll.bind(this));
	}
	
}

app.listenToClick('calculate');
```

We will discuss techniques we have use in our refactor in later chapters. In essence, we have wrapped our code in an **object literal** called **app**. This makes our code re-useable and contained. We have also removed any superfluous or repetitious code. We use the **this** keyword to be self-referential. 