5. Scope
------------------

Scope is what sets of variables, constants or functions that functions have access too.

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
printName('Pete') //  ReferenceError: surname is not defined

console.log(name) // returns Ted
console.log(newName) // ReferenceError: newName is not defined
console.log(surname) // ReferenceError: surname is not defined
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