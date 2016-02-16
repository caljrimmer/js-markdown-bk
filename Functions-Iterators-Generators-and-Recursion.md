1. Scope
------------------

The scope of a variable or function communicates where it is accessible in different areas of your code. You create scope by where you define a variable or function.

There are 3 types of scope in Javascript:

 - **Global scope** - i.e. this is accessible from everywhere
 - **Local or Function scope** - i.e. this is accessible from within the same function
 - **Block scope** - i.e. this is accessible from inside the expression e.g. inside curly brackets **{}**. 

**Global Scope**

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

>Whilst it might seem useful to have **variables** accessible from everywhere, you should try and structure your code so you have as few **global scoped variables** as possible. This will make your code will be easy to maintain and test your code.

**Function Scope**

```javascript
function printName (surname) {
	let firstname = 'Edward'; //Function scoped
	return firstname + ' ' + surname; 
}

printName("Smith") // returns "Edward Smith"
console.log(firstname) // ReferenceError
```

In the example, we have define a **firstname** inside a **function**, then it will be in **function scoped**. This is only accessible inside the function and not outside it.  If we try to access **firstname** outside the function, we will get a reference error.

**Block Scope**

```javascript
function printName (surname) {
	if (surname === "Smith") {
		let firstname = "Edward"; //Block scoped
		return firstname + ' ' + surname;
	}
	console.log(firstname); // ReferenceError
	return surname; 
}

console.log(firstname); // ReferenceError
printName("Smith") // returns "Edward Smith"
```

When we define a variable inside curly brackets **{}**, an **if()** statement in our example, this will now exhibit **block scope**. This is only accessible inside the curly brackets **{}** and not outside it (not in the parent function or any other function).

Before **ES6**, the latest released javascript version, javascript didn't have the concept of **block scope**. We can still be backwards compatible by still using the **var** which doesn't exhibit block scope. **Let** and **const** both exhibit **block scope**. 

```javascript
if (isChecked) {
	var firstname = "Edward";
	const middle = "Alan";
	let surname = "Smith";
}
console.log(firstname) // returns Edward
console.log(middle) // ReferenceError
console.log(surname) // ReferenceError
```

>Tip

>**Function scope** is just a javascript concept. In other coding languages **block scope** would include **functional scope** (as they both are defined inside curly brackets **{}**).

**Using scope in a web application**

When we are coding our web applications, we use scoping to allow us to control what each function can do and what variables are readable and writable.

```javascript
let soldierRole = "Obeys all orders";

function giveOrder (who, newRole) {
	who = newRole;
}

giveOrder(soldierRole, "Peel potatoes");
```

We have create a function called **giveOrder()** that amends the  **soldierRole**. The **soldierRole** variable and **giveOrder()** function are both defined in the **global scope**. The **giveOrder()** function can read and write to the **soldierRole**.

```javascript

let soldierRole = "Obeys all orders";

function giveOrder (who, newRole) {
	who = newRole;
}

function barracks () {
	let sergeantRole = "Gives orders to Soldier";
	giveOrder(soldierRole, "Peel potatoes");
	giveOrder(sergeantRole, "Peel potatoes");
}

giveOrder(sergeantRole, "Peel potatoes"); //Reference Error
```

Now we define a **barracks()** function and inside this function, we define a **sergeantRole** variable. Inside the **barracks()** function, we can access the **giveOrder()** function and **soldierRole** variable because they are **globally scoped**. 

Inside the **barracks()** function, we can give orders to the **soldierRole** and the **sergeantRole**. Outside the **barracks()**, we can only give orders to the **soldierRole**. The **sergeantRole** variable is functionally scoped.

```javascript
let SoldierRole = "Obeys all orders";
function barracks () {
	let SergeantRole = "Gives orders to Soldier";
	function officersMess () {
		let MajorRole = "Gives orders to Sergeant and Soldier";
		giveOrder (SoldierRole, "Peel potatoes");
		giveOrder (SergeantRole, "Peel potatoes");
		giveOrder (MajorRole, "Peel potatoes");		
	};
	giveOrder (majorRole, "Peel potatoes"); //Reference Error
};
giveOrder (sergeantRole, "Peel potatoes"); //Reference Error

```

In the example above, we define another function called **officersMess()** which exists inside the **barracks()**.

The **majorRole** variable is defined inside the innermost **officerMess()** function. The **majorRole** variable has functional scope to the **officersMess()** function. It is not possible for function outside the **officersMess()** to read or write to the **majorRole** variable.

A simple rule of thumb is that the innermost defined function, i.e. the **officerMess()** function, can access and amend everything outside it.

If we try and invoke the **giveOrders()** function with a variable whilst in the wrong scope, the browser will throw a **ReferenceError**.

When we define a function inside a function, we create a **closure**. An inner function has access to read and write to all outer functions and variables.

**Closures**



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