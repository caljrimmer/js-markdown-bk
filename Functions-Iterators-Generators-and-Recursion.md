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

Now we define a **barracks()** function and inside this function, we define a **sergeantRole** variable. 

Inside the **barracks()** function, we can access the **giveOrder()** function and **soldierRole** variable because they are **globally scoped**. 

Inside the **barracks()** function, we can give orders to the **soldierRole** and the **sergeantRole**. Outside the **barracks()**, we can only give orders to the **soldierRole**. The **sergeantRole** variable is functionally scoped.

```javascript
let SoldierRole = "Obeys all orders";
function barracks () {
	let SergeantRole = "Gives orders to Soldier";
	function officersMess () {
		let MajorRole = "Gives orders to Sergeant and Soldier";
		giveOrder (MajorRole, "Peel potatoes");		
	};
	giveOrder (sergeantRole, "Peel potatoes");
};
giveOrder (soldierRole, "Peel potatoes");

```

In the example above, we define another function called **officersMess()** which exists inside the **barracks()**.

The **majorRole** variable is defined inside the innermost **officerMess()** function. The **majorRole** variable has functional scope to the **officersMess()** function. It is not possible for function outside the **officersMess()** to read or write to the **majorRole** variable.

A simple rule of thumb is that the innermost defined function, i.e. the **officerMess()** function, can access and amend everything outside it.

If we try and invoke the **giveOrders()** function with a variable whilst in the wrong scope, the browser will throw a **ReferenceError**.

When we define a function inside a function, we create a **closure**.

**Closures**

The definition of a closure is:

> A function with a function, where the inner function has access to the variables and functions defined in the outer function.

Closures allow us to create a new way to contain our web application that is superior to using **object literals**. 

From the previous chapter, we demonstrated we could wrap our applications in an **object literal**.

```javascript
let myApp = {
    text : 'App Started',
    start : function (){
        return this.text;
    }
}
myApp.start(); //returns "App started"
```
The disadvantage to this approach is that all the properties of **myApp** are amendable at any time, anywhere in your code. For example:

```javascript
myApp.text = 'Hacky text';
myApp.start(); //returns "Hacky text"
```

This is acceptable when you're the only developer working on the code but the this approach can become unmanageable in bigger teams. Properties and methods can be amended with no structure or process. This will result in the code becoming brittle.

**Closures** allow us to create structure and enforce process. Take the following code as an example:

```javascript
let myApp = function () {
	const privateText = "App Started";
	function start () {
		return privateText;
	}
	return {
		start : start
	}
}();

myApp.start(); //returns "App Started"
console.log(privateText) // Reference Error
```

We define a function called **myApp** and within that function we define another function called **start()**. We return an object that contains the exposed **start()** function.

We have created a **closure**. We have also defined a variable called **privateText** which is not accessible outside the **myApp()** function.

The trailing parentheses **()** mean the function is immediately invoked. That means the function executes immediately to define **myApp**.

We expand our example to create public and private methods, and public and private properties.

```javascript
const myApp = function () {
	const privateText = "Prefix-";
	let publicText = "Text";
	
	function setPublicText (newText) {
		publicText = newText;
	}
	
	function getAllText () {
		return privateText + this.publicText;
	}
	
	return {
		getAllText : getAllText,
		setPublicText : setPublicText
	}
}();

myApp.getAllText(); //returns "Prefix-Text"
myApp.setPublicText("Overwrite");
myApp.getAllText(); //returns "Prefix-Overwrite"
```

In the above example, we allow the **publicText** to be amended with the **setPublicText()**, and the **publicText** and **privateText** to be returned with **getAllText()**.  We cannot edit the **privateText**.

We have now created a container for our web application that allows us to expose just the methods and properties that are appropriate.

>Tip

>When we immediately invoke a function, i.e. **function(){}()**, it is called an **Immediately-Invoked Function Expression** or **IIFE**. **IIFEs** are useful for creating self contained code blocks.

**Hoisting**

Hoisting is not so much a concept but more of a feature of javascript to beware of. It is important to understand hoisting so that you don't create obscure bugs in your code.

Hoisting is JavaScript's default behavior of moving variable declarations to the top of a functional block. 

```javascript
function notHoisted() {
	var x;
	x = 1;
	return x;
}

function hoisted() {
	x = 1;
	return x;
	var x;
}

notHoisted(); //returns 1
hoisted(); //returns 1
```
In the above example, both functions preform the same task. They return x. 

In **notHoisted()** we declare **x**, then assign **x** a value of 1 and return **x**.

In **hoisted()** we assign **x** a value of 1, then return **x** and finally declare **x**. This looks like it should not work. You would expect an Reference Error, as **x** is not declared. 

Javascript will always move the declaration of a variable to the top of a function at run time. This is called **hoisting**.

To avoid **hoisting**, we simply always declare our variables at the top of our code. This makes you code easy to read and perform as you expect.