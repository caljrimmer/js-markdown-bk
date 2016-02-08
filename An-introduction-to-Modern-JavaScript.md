Introduction to Modern Javascript
===========================

You can code any sort of application, to run on nearly any device when you build it with Javascript.  This book is to show you how to create, build, test and deploy your own application using just javascript.

A modern Javascript developer can create any application, on any device. From the first line of code to deployment to live environment, javascript developer never has to utilise any other language.  Modern javascript isn't just about the latest revisions of the language but a fundamental shift in simplifying how a developer can create, test and deploy applications.

Javascript, released in 1995, was developed as a way to run scripts within a website. In its early days some derided the language as being simple and lacking the power and sophistication to be taken seriously. Javascript has evolved with the internet and the language has be improved over the years. 

Javascript, once just used for simple client-side scripting on web sites can now be used to develop games, create mobile applications, web applications, desktop applications, sophisticated data visualisation, complex animations and run intensive computations.


> **ES6**

>The latest version of Javascript,  ECMAScript 2015, also known as ES6, is a significant update to the language. It was the first update to the language since ES5 was standardised in 2009. All code examples in this book will utilise ES6 where appropriate. 
 
 

Writing some Javascript
-----------------------

JavaScript is designed to run as a scripting language in a host environment. The most common host environment is a **browser**.

 Javascript can be run on any **browser**. We will be using **Chrome** as our browser of choice. Chrome has a number of developer tools that will help you develop your code. One of those tools is called **Console** and it that allows you to run Javascript directly.

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

Time to look at data types, variables and constants, and operators. There will be code example for each which you can use **Console** in **Chrome** to verify and experiment with.

Data Types 
-----------------------------

In JavaScript there are 5 different data types that can contain values. String, Boolean, Number, Object and Function:

```javascript
const age = 16; //Number
const name = "Ted"; // String
const isChecked = true; //Boolean
const obj = {count: 1, name: "MyApp"}; // Object
function add (a,b) { 
	return a + b; 
} // Function
```

There also two other data types that are subsets of Object. Date and Array:

```javascript
const dateOfBirth = new Date('28/12/1980'); //Date
const teams = ["reds","blues","greens"]; // Array
```

Finally there are 2 data types that cannot contain values. Null and Undefined:

```javascript
const noValue; //Undefined as we have no value
const nullValue = null; //Value is defined as null
```

Javascript, once a data type object is defined, Javascript makes available a number of different prototypal methods for that data type. 

A method is very similar to a function but it exists on the data type object rather than independent of it. These methods help you do work on that particular data type.

**Strings** 

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
function StringLength (str) {
	return str.length;
}
StringLength("marvellous") // returns 10

//This is a method
const string = "marvellous";
string.length; //returns 10
```

**Booleans**

```javascript
let value = false;
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

To create a **boolean** (i.e. true or false) data type, we declare a container of either true or false. Note that we do not wrap true or false in quotations as this would turn the boolean into a string.

**Booleans** are often used in Javascript. In the example, we are using them to toggle a value (i.e. hide or show, done or not done, etc.).

**Dates**

```javascript
const today = new Date();
const christmas = new Date('12/25/2015');

today.getDate() // returns date of today (i.e. 1-31);
today.getMonth() // returns month of today (i.e. 1-12);
today.getHours() // returns hour of today (i.e. 0-23);
```

To create a **date** data type, we declare a container with the function **Date()**. 

We then have the ability to perform date operations on the data type.  In the example above we use **getDate()** to return the date of today, **getMonth()** to return the month of today, **getHours()** to return the hour of today.

We also can define a date in the future or past by passing a date to the **Date()** function. We must pass the date in the US format (i.e. month before day).

**Numbers**

```javascript
const total = 9;
const price = 11.99;

Number.isInteger(total) // returns true;
Number.isInteger(price) // returns false;
Math.sqrt(total); //returns 3
Math.ceil(price); //returns 12
Math.floor(price); //returns 11
```

To create a **number** data type, we declare a container of either an integer or a decimal.

We then have the ability to perform numerical or mathematical functions and methods on the value.  In the example above we use **isInteger()** to determine if value is an integer, **Math.sqrt()** to return the square root of a value, **Math.floor()** to round down to the nearest integer and **Math.ceil()** to round up to the nearest integer.

Javascript allows us to replicate most mathematical computations. 

```javascript
let sum = 0;

function add (a,b) {
	return a + b;
}

function subtract (a,b) {
	return a - b;
}

function multiply (a,b) {
	return a * b;
}

function divide (a,b) {
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

**Array**

```javascript
const strings = ['blue','red','yellow'];
const numbers = [20,30,40];
const mixedList = [1,'blue',false];

strings.length; //returns 3

numbers.map((num) => {
	return num / 10; 
}); //returns [2,3,4]

mixedList.forEach((item) => {
	console.log(typeof(item)) 
}); //returns number, string, boolean
```

To create an **array** (i.e. a list) data type, we declare a container with square brackets []. Inside the **array** you can define values of any sort of data type. The values are separated by commas.

In the example above we have defined an 3 different **arrays**. One with string data types, then number data types and finally a mix of different data types.

Arrays have many prototype methods to help you work with them. They have the most prototype methods of all the data types. You are able to loop through **arrays** with **forEach()** or even transform the values of an array with **map()**.

Arrays can be used to create lists of objects:

```javascript
const collection = [
	{id:1, name:'Ted'},
	{id:2, name:'Fred'},
	{id:3, name:'Ned'}
]
```
When an we have **array** of objects, particularly if they have been return from a database, then we call the array a **collection** and the objects **models**.

**Functions**

Functions are building blocks in JavaScript. A function is a JavaScript procedure, a set of statements that performs a task or calculates a value.

```javascript
function subtract (a,b) {
	return a - b;
}

const multiple = function (a,b) {
	return a * b;
}

//Fat Arrow
const add = (a,b) => {
	return a + b;
}

add(2,4); //returns 6
subtract(6,2); //returns 4
multiple(2,2); //returns 4
```

We can create a **function** in a few different ways. In each case we must define what arguments the **function** expects with parentheses ().  The **function** statements are enclosed in curly brackets {}

In the example, we define 3 functions for adding, subtracting and multiplying. In each can we define the arguments a and b, do an operation on them, and then return result.

It is possible to define a function but not pass it arguments.

```javascript
function staticAdd () {
	return 10 + 6;
}

staticAdd(); //returns 16
```

It is possible to define a function within a function

```javascript
function internalAdd (a,b) {
	function add (a,b) {
		return a + b;
	}
	return add(a,b) * 2;
}

internalAdd(2,4); //returns 12
```

A function can also return a function

```javascript
function dynamic (a) {
	return function (b) {
		return a * b;
	};
}

const multiplyBy2 = dynamic(2);
multiplyBy2(4); //returns 8

const multiplyBy4 = dynamic(4);
multiplyBy4(4); //returns 16
```


**Objects**

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

amendable.name = 'Edward'; //name is now Edward
amendable.job = 'Accountant'; //adds job value

delete amendable.age; //removes age value
```

**Javascript is Loosely Typed**

Javascript is loosely typed. This means you can change the data type of a defined container at anytime. Most programming languages do not allow you to do this. 

```javascript
var changeable = 1; //Data type is a number
changeable = 'Ted'; //Data type is now a string
```
In the example, we change the variable **changeable** to not just have a different value but also to have a different data type. It is advisable, even though you can, not to change your data type whilst drafting your code. It can be confusing to maintain and extend your code.

Variables and Constants
-----------------------------

Javascript allows us to define containers to store data, objects or functions. Defining these containers allow us to structure our code and to manage scope (i.e. ability to access the container and the data within). There are 3 ways to define a container:

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

Operators
------------------

**Comparison Operators**

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

**Logical Operators**

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


What is Scope?
------------------

Scope is basically sets of variables, constants or functions that you have access to as you draft your code.

There are 3 types of scope in Javascript:

 - **Global scope** - i.e. this is accessible from everywhere
 - **Local or Function scope** - i.e. this is accessible from within the same function
 - **Block scope** - i.e. this is accessible from inside the expression e.g. inside an **if()** statement 

```javascript
let name = 'Ted'; //Global scoped 
function printName (middle) {
	let newName = 'Edward'; //Function scoped
	if (middle === 'John') {
		let surname = 'Smith'; //Block scoped
		return name + ' ' + middle + ' ' + surname;
	}
	return newName + ' ' + middle + ' ' + surname; 
}

printName('John') // returns Ted John Smith
printName('Pete') // returns Edward Pete undefined

console.log(name) // returns Ted
console.log(newName) // returns undefined
console.log(surname) // returns undefined
```

In the example above, we have defined three variables **name**, **surname** and **newName**. Where we have defined these variables, determines the scope of the variable.  

If we define a variable outside all functions, then it will be **global scoped**, i.e. **name**.

If we define a variable inside a function, then it will be **function scoped**, i.e. **newName**. This is only accessible inside the function and not outside it. 

if we define a variable inside a statement, then it will be **block scoped**, i.e. **surname**. This is only accessible inside the statement and not outside it (either in the parent function or any other function).

We use scoping to allow us to control what each function can do. We make our function discrete and the variables defined in them private from other functions. 

Another example:

```javascript
function giveOrder (who, what) {
	who.role = what;
	return who;
}

let Soldier = {
	name: 'Jones',
	role: 'Obeys orders'
}

giveOrder (Sergeant, 'Peel potatoes'); //Error
giveOrder (Major, 'Peel potatoes'); //Error

function barracks () {
	
	let Sergeant = {
		name: 'Smith',
		role: 'Gives orders to Soldier'
	}
  
	giveOrder (Soldier, 'Peel potatoes'); // returns {name: 'Jones', role: 'Peel potatoes'}
	giveOrder (Major, 'Peel potatoes'); //Error
	
	function officerMess () {
	
		let Major = {
			name: 'Lee',
			role: 'Gives orders to Sergeant and Soldier'
		}
		
		giveOrder (Soldier, 'Peel potatoes'); //returns {name: 'Jones', role: 'Peel potatoes'}
		giveOrder (Sergeant, 'Peel potatoes'); //returns {name: 'Peel', role: 'Peel potatoes'}
		
	}();
}();

```

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