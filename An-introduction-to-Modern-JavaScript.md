Introduction to Modern Javascript
===========================

You can code any sort of application, to run on nearly any device when you build it with Javascript.  This book is to show you how to create, build, test and deploy your own application using just javascript.

A modern Javascript developer can create any application, on any device. From the first line of code to deployment to live environment, javascript developer never has to utilise any other language.  Modern javascript isn't just about the latest revisions of the language but a fundamental shift in simplifying how a developer can create, test and deploy applications.

Javascript, released in 1995, was developed as a way to run scripts within a website. In its early days some derided the language as being simple and lacking the power and sophistication to be taken seriously. Javascript has evolved with the internet and the language has be improved over the years. 

Javascript, once just used for simple client-side scripting on web sites can now be used to develop games, create mobile applications, web applications, desktop applications, sophisticated data visualisation, complex animations and run intensive computations.


> **ES6**

>The latest version of Javascript,  ECMAScript 2015, also known as ES6, is a significant update to the language. It was the first update to the language since ES5 was standardised in 2009. All code examples in this book will utilise ES6 where appropriate. 
 
 
Writing some Javascript
------------------

JavaScript is designed to run as a scripting language in a host environment. The most common host environment is a browser.

 Javascript can be run on any browser. We will be using Chrome as our browser develop on. Chrome has a number of developer tools that will help you develop your code. One of those tools is called "Console" and it that allows you to run Javascript directly.

To begin:

 1. Open the Chrome browser
 2. Right click and select "Inspect"
 3. Click on "Console" tab

You now have the Chrome developer tools open and we can write our first bit of Javascript.

Let's try creating a simple pop-up with the text "hello".
 
```javascript
window.alert('hello');
```
The **window** object is where all native global JavaScript objects, functions, and variables reside in the browser. The **alert** is a function that Javascript provides to allow you to easily create pop-ups. 

A **function** in javascript is invoked with parentheses and inside the parentheses arguments can be passed. 

we use a semicolon to separate statements. 

Now let's make a simple function to capture a user's response and return the value.

```javascript
const result = (message) => {
	return window.confirm(message);
}
result('Do you confirm this action?');
```

The console should log *true*, if ok is clicked and *false* if cancel is clicked.

So we have create a new function called **result** that returns a value that we get from another native javascript function called **confirm**. We then invoke our result function with parentheses whilst passing a string of 'Do you confirm this action?' as an argument.

We also use the **const** keyword to declare our function. Const  creates a read-only reference to the function. This means the function can not be amended after it has been declared.

We don't need to specify **window** when calling functions. Javascript will assume it for you. Thus these two function do the same thing.

```javascript
window.alert('hello');
alert('hello'); //Same as window.alert

window.confirm('confirm?');
confirm('confirm?'); //Same as window.confirm
```


>The **window** object is global and contains all native Javascript functions and variables. 

>A **function** can be passed arguments and is invoked with parentheses.

Data Types 
-----------------------------

In JavaScript there are 5 different data types that can contain values. String, Boolean, Number, Object and Function:

```javascript
const age = 16; //Number
const name = "Ted"; // String
const isChecked = true; //Boolean
const obj = {count: 1, name: "MyApp"}; // Object
const add = (a,b) => { return a + b; } // Function
```

There also two other data types that are subsets of Object. Date and Array:

```javascript
const dateOfBirth = new Date('28/12/1980'); //Date
const teams = ["reds","blues","greens"]; // Array
```

Finally there are 2 data types that cannot contain values. Null and Undefined:

```javascript
const noValue; //Undefined as we have no value
const nullValue = null; //Null
```

Javascript, once a data type object is defined, Javascript makes available a number of different methods for that data type. A method is very similar to a function but it exists on the data type object rather than independent of it. These methods help you do work on that particular data type.


Strings 
-----------------------------

```javascript
const word = "marvellous";

word.length; //returns 10
word.toUpperCase(); //returns MARVELLOUS
word.substr(0,5);//returns marve
```

To create a string data type, we declare a variable wrapped in either double (") or single quotes (').

Once the string data type is defined, we can then use a number of methods to do work on strings. In the example above we use **length** to get the number of characters in a string, **toUpperCase()** to return the string in uppercase characters and **substr()** to return a the first 5 characters.

```javascript
//This is a Function
const StringLength = (str) => {
	return str.length;
}
StringLength("marvellous") // returns 10

//This is a method
const string = "marvellous";
string.length; //returns 10
```

Booleans
-----------------------------

```javascript
let value = false;
const toggleChecked = (isChecked) => {
	if (isChecked) {
		return false;
	} else {
		return true;
	}
}
//or short-hand
const toggleChecked = (isChecked) => {
	return (isChecked) ? false : true;
}

value = toggleChecked(value) // value is false;
value = toggleChecked(value) // value is true;
```

To create a boolean data type, we declare a container of either true or false. Note that we do not wrap true or false in quotations as this would turn the boolean into a string.

Booleans are often used in Javascript. In the example, we are using them to toggle a value (i.e. hide or show, done or not done, etc.).


Numbers and Maths
-----------------------------

```javascript
const total = 9;
const price = 11.99;

Number.isInteger(total) // returns true;
Number.isInteger(price) // returns false;
Math.sqrt(total); //returns 3
Math.ceil(price); //returns 12
Math.floor(price); //returns 11
```

To create a number data type, we declare a container of either an integer or a decimal.

We then have the ability to perform numerical or mathematical functions and methods on the value.  In the example above we use **isInteger()** to determine if value is an integer, **Math.sqrt()** to return the square root of a value, **Math.floor()** to round down to the nearest integer and **Math.ceil()** to round up to the nearest integer.

Javascript allows us to replicate most mathematical computations. 

```javascript
let sum = 0;

const add = (a,b) => {
	return a + b;
}

const subtract = (a,b) => {
	return a - b;
}

const multiply = (a,b) => {
	return a * b;
}

const divide = (a,b) => {
	return a / b;
}

sum = add(1,2) //sum equals 3
sum = multiply(sum,2) // sum equals 6
sum = divide(sum,3) // sum equals 2
sum = minus(sum,1) // sum equals 1

```

Notice how we can pass the value of **sum** as a parameter to our new maths functions as it keeps its state (i.e. **sum** retains its previous value and then changes to reflect its new value).

If we tried to pass a string as an argument:

```javascript
multiply('name',3); // returns NaN
add('name',3) // returns 'name3'
```

Javascript stops behaving predictably. With **multiple**, it returns **NaN** (i.e. Not a Number) and with **add**, it returns a new string of the 'name' with '3' tagged on the end.

We can only do numeric or mathematical work on Number data types. 

Objects
-----------------------------

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
```
To create a object data type, we declare a container with parentheses {}. Inside the object you can define values of any sort of data type. The values are written as name:value pairs (name and value separated by a colon).

In the example above we have defined an object with a string, number, boolean, another object and also a function.

Notice that in the function, we reference the object with the **this** keyword. The **this** keyword is very useful in Javascript. It allows us to be **self-referential** (refer to different parts of the same object).

The defined object is also **stateful**. In the example, we can increment the **count** value by invoking the **addToCount()** function. The defined object remembers what the internal values as long as it exists.

Variables and Constants
-----------------------------

Javascript allows us to define containers to store data, objects or functions in. Defining these containers allow us to structure our code and to manage scope (i.e. ability to access the container). There are 3 ways to define a container:

Use a **variable** declaration.
```javascript
var z;
var x = 1;
var y = 2;
z = x + y; // z equals 3 now
```

You can define a variable with a value or without a value and populate it later. All JavaScript variables must be identified with unique names.

Use a **let** declaration.
```javascript
let sentence;
let name = "Ted";
sentence = "My name is " + y; // sentence equals "My name is Ted"
```

**Let** is similar to a variable declaration. **Let**, unlike **var**, cannot be hoisted and it exhibits block scope. We will discuss scope and hoisting later in the book. 

Use a **const** declaration.
```javascript
const PI = 3.14;
PI = 3.145 //Throws an error
```

**Const** declared with a given value can not be changed. It is used, as it's name suggests, to define constants. **Const**, like **let**, also cannot be hoisted and it exhibits block scope.

It is possible to declare a container without using **var**, **let** or **const**.

```javascript
name = 'Ted'; //same as window.name = 'Ted'
x = 1; //same as window.x = 1
```

Declaring a container this way adds the container on to the window object and it becomes globally available. This is considered bad practice because relying too much on global containers can result in collisions between various scripts on the same page.

Best practise is to use **let** and **const**. Block scoping means your containers will act in a more granular and predictable way.

```javascript
const increment = (num) => {
	let total = 0;
	total = total + num;
	return total;
}
increment(5) //returns 5
increment(10) //returns 15
```

In this example we use **const** to define our increment function (as we don't want it to change) and **let** for our sum total (as it does change).

What is Scope?
------------------

Javascript is loosely typed. That means you can define a variable but not have to describe what it contains.

There are 4 ways to create containers for your 
In this tutorial I’ll introduce you to two new keywords: let and const. They enhance JavaScript even more by filling the gap with other languages and providing us a way to define block-scope variables and constants. If you want to learn more about them, keep reading.

A simple web page
-------------------------

A web page consists of HTML, CSS and Javascript. HTML provides the scaffolding of the page. CSS provides the styling of the page. Javascript provides the behaviour. Javascript is what makes a web page dynamic and responsive to the user. 

To make our web page, we will need a text-editor to write our code with. Any text editor would work (i.e. Notepad or TextEdit) but there are a number of excellent free options that will help you write code more efficiently. The best free options are:

 - Atom - https://atom.io/
 - Sublime - http://www.sublimetext.com/
 - Brackets - http://brackets.io/

Next we need to create a new directory to store our web page files in. Let us name it "example-web-page" and save it to your desktop. Now we are going to create 2 files that we will save in this director.

Create and save **index.html**.
```
<html>
	<head>
		<title>Example Web Page</title>
	</head>
	<body>
		<div id="container"></div>
	</body>
	<script src="script.js"></src>
</html>
```
we've put the <kbd>script</kbd> element near the bottom of the HTML file. This is because we wish to have all the HTML loaded before the Javascript is parsed. This will make scripts that interact with the HTML work consistently.

Create and save **script.js**.
```
const 
```