1. Scope
------------------

The scope of a variable or function communicates where they are accessible in different areas of your code. You create scope by where you define a variable or function.

There are 3 types of scope in Javascript:

 - **Global scope** - i.e. this is accessible from everywhere
 - **Local or Function scope** - i.e. this is accessible from within the same function
 - **Block scope** - i.e. this is accessible from inside the expression e.g. inside an **if()** statement 

**1.1 Global Scope**

```javascript
name = "Ted";
window.name = "Ted";

//or variables defined outside functions
var name = "Ted";
let name = "Ted";
const name = "Ted";

//or functions defined outside other functions
function sayName (name) {
	return name;
}
```

When a variable or function is defined outside a bounding function, then it will always be in **global scope**. These functions and variables can be invoked, read and written from anywhere in your code.

>**Tip**

>Whilst it might seem useful to have **variables** accessible from everywhere, you should try and structure your code so you have as few **global scoped variables** as possible. your code will be easy to maintain and test your code, if you limit **global scoping**.

**1.2 Function Scope**

```javascript
function printName (surname) {
	let firstname = 'Edward'; //Function scoped
	return firstname + ' ' + surname; 
}

printName("Smith") // returns "Edward Smith"
console.log(newName) // ReferenceError
```

In the example, we have define a **firstname** inside a **function**, then it will be in **function scoped**. This is only accessible inside the function and not outside it.  If we try to access **firstname** outside the function, we will get a reference error.

**1.3 Block Scope**

```javascript
function printName (surname) {
	let firstname = "Edward"; //Function scoped
	if (surname === "Smith") {
		let middle = "Alan";
		return firstname + ' ' middle + ' ' + surname;
	}
	console.log(middle); // ReferenceError
	return firstname + ' ' + surname; 
}

printName("Smith") // returns "Edward Alan Smith"
console.log(middle); // ReferenceError
```

if we define a variable inside an **if()** statement, then it will be **block scoped**. This is only accessible inside the statement and not outside it (either in the parent function or any other function).

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

giveOrder (Sergeant, 'Peel potatoes'); //ReferenceError: Sergeant is not defined
giveOrder (Major, 'Peel potatoes'); //ReferenceError: Major is not defined

function barracks () {
	
	let Sergeant = {
		name: 'Smith',
		role: 'Gives orders to Soldier'
	}
  
	giveOrder (Soldier, 'Peel potatoes'); //returns {name: 'Jones', role: 'Peel potatoes'}
	giveOrder (Major, 'Peel potatoes'); //ReferenceError: Major is not defined
	
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

In the example above, we define three variables **Soldier**, **Sergeant** and **Major**. We have a global scoped function called **giveOrders()**.

**Soldier** is defined outside all functions and is accessible and amendable everywhere.

**Sergeant** is defined inside the first **barracks()** function and is accessible to everything inside this function but inaccessible outside it.

**Major** is defined inside the innermost **officerMess()** function and is accessible to everything inside this function but inaccessible outside it.

A simple rule of thumb is that the innermost defined function, i.e. anything inside the **officerMess()**, can access and amend everything outside it.

In our example,  any function in the **officerMess()** has the greatest ability to inform variables, then function in the **barracks()** and finally anything outside that.

If we try and invoke the **giveOrders()** function with a variable whilst in the wrong scope, the browser will throw a **ReferenceError**.

We can use scope to organise our applications and provide protection to our variables being accidentally overwritten. 

**2.6 Functions**

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