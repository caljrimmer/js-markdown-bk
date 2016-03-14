
Working with JS Syntax
====================

In the previous chapter, we looked at the basic building blocks of javascript code. In this chapter, we will start to look at how we can use these building block enrich our functions.

This chapter will address how to define functions and understanding how to use functions properly. We will then look at iterations and recursion over arrays and objects. Finally, we shall look at generator functions, new to javascript, which combine functions and iteration. 

Defining functions
---------------------

Functions are used to contain blocks of code designed to perform a particular task. We created our functions to be small, reusable and testable.

Functions can be defined in a several different ways. In this section, we shall look at what ways we can define functions and what difference that makes to how our functions execute.

**Anonymous function** 

An **anonymous function** is a function defined without a name. It is the easiest way to define a function and you will see **anonymous functions** used often in javascript.

```javascript
function () {
	return "I am an Anonymous Function";
}
```
This, in its current context, is rather useless. We can't refer to the function and we haven't invoked it.

```javascript
function () {
	return "I am an Anonymous Function";
}() //returns "I am an Anonymous Function"
```

If we invoke the **anonymous function** immediately by add trailing **()** parentheses, then it will return a value. This makes it useful for doing a task once.

>Tip

>When we immediately invoke a function, i.e. **function(){}()**, it is called an **Immediately-Invoked Function Expression** or **IIFE**. **IIFEs** are useful for creating self contained code blocks.

**Anonymous function** can also be passed in callbacks or as event handlers. For example:

```javascript
el.addEventListener("click", function () {
	return "I was Clicked";
})
```

In this example,  we pass an **anonymous function** which returns a string when the element is clicked. We do not need to re-use this function outside the click event. If we use an **anonymous function**, it means we have to write less code.

**Function declaration**

A **function declaration** is just a **named anonymous function**. We provide our **function declaration** with a name so it can be referenced at a later point in your code. 

Note that we define the **name** after the **function** keyword and before the **parenthesis** **()**

```javascript
function add (a,b) {
	return a + b;
}

add(2,3) //returns 5
```

A **function declaration**, like an **anonymous function**, can be immediately invoked but can also be re-used:

```javascript
function add (a,b) {
	return a + b;
}(1,2) // returns 3

add(3,5) //returns 8
```

Note that we pass the arguments in the trailing parentheses **()** when we invoke the function immediately. 

We can reuse the **add()** function whenever we like.

We can also access the name of the function declaration, inside our defined function using:

```javascript
function add() {
	return arguments.callee.name;
}
add(); // returns "add";
```

**Function constructor**

We can make a function using the **Function()** constructor function.

```javascript
const add = new Function('a', 'b', 'return a + b');
```
We provide the **Function()** constructor with our arguments (**a,b**) and the function body as a string. Any number of arguments can be passed aslong as the function body is the last argument provided.

**Assign a function to variable**

A function can be assigned to a variable.  This is very similar to our **function declaration** but can assign the function as a value of a variable so we can reuse it later in our code.

```javascript
const add = function (a,b) {
	return a + b;
}

const subtract = function subtract (a,b) {
	return a - b;
}

const multiple = new Function('a', 'b', 'return a * b');

add(1,3); //returns 4
subtract(3,1); //returns 2
multiple(4,2) //returns 8
```

When a function is assigned to a variable, it works the same as a **function declaration**. We can immediately invoke it, or re-use at a later point.

An important difference between **assigning a function to a variable** and a **function declaration** is that when assigning to a variable, you can change the function at run time. This means you can change what the function does at anytime in your code.

```javascript
let add = function (a,b) {
	return a + b;
}

const augmentAdd = function (c) {
	add = function (a,b) {
		return a + b + c;
	}
}

add(1,2) // Returns 3
augmentAdd(2);
add(1,2) // Returns 5
```

**Differentiation between a method and a function**

A method is a function that exists as a property of an object. Functions and methods perform exactly the same but are invoked differently. Take the follwoing example:

```javascript

function add (a, b) {
	return a + b;
}// This is a function

const object = {
	add : function (a, b) {
		return a + b;
	}, // This is a method
	addTwice : function (a,b) {
		return 2 * this.add(a,b);
	}
}

add(1,2) //returns 3
object.add(1,2) //returns 3
object.addTwice(1,2) //returns 6
```

We invoke a **function** with it's name **add()** and with a **method**, we invoke it based on it's parent object and then dot followed by name **object.add()**. **Methods** use dot notation to be accessed and invoked.

A method allows us use the **this** keyword to be self-referential to its containing object. 

**Arrow function**

The latest javascript version, **ES6**, we have a new way to create a function.  The **arrow function** means you can express more whilst writing less code.

```javascript
(a,b) => {
	return a + b;
} //example of anonymous function

const add = (a,b) => {
	return a + b;
} //example of variable defined function
```

**Arrow functions** don't need the function keyword, which is replaced with an arrow (**=>**).

```javascript
const multiplyBy2 = (num) => {
	return num * 2;
}

//is equivalent to
const multiplyBy4 = num => num * 4;

multiplyBy2(2); //returns 4
multiplBy4(2); //returns 8 
```
In the above example, we can remove the **return** keyword and parentheses **()** but still perform the same task. **Arrow functions** allow us to do more, with less code. 

The **arrow function** deals with **scope** and the **this** keyword differently than any other function definition. We shall address this later in the book.

>Tip

>The **Arrow function** can also be called a **Fat Arrow function**.

**What is the best way to define a function?**

There is no wrong way to define a function. You can choose whichever you feel best suits what you are trying to achieve. 

A function will always take arguments, execute the defined statements and then return the result. 

 - **Methods** are used most when taking an object oriented approach to structuring your code
 - **Function declarations** are useful if you are taking a functional programming approach to structuring your code
 - **Arrow functions** are useful when you wish to limit the amount of code you write
 - **Anonymous function** are useful for wrapping your web applications (for functional scoping reasons) and when you don't wish to re-use the function

In most web applications, you will see a mix of different ways to define functions. You should try to be consistent in how you structure your code but not over concerned which approach you take.


Understanding Functions
------------------------------

Functions are objects that are invokable with **()** parentheses. A function is a set of statements that perform a task. 

In order to be able to write functions that work as expected, it is important to understand some of the fundamental expectations of javascript with respect to functions.

We shall look at **parameters**, **scope**, **closures**, **arguments**, **hoisting** and **methods**.

**Parameters**

Functions are passed parameters via the parentheses **()**. Parameters can be any sort of data type including other functions.

**Default parameters**

A default parameter allows us to set the initial value of a parameter. We can over write the parameter value or accept the default value when evaluating our function. 

We can define the default value of parameters by using the **=** operator.

```javascript
function add (a,b=10) {
	return a + b;
}

add(5); //Returns 15;
add(5,2); //Returns 7;
```

In the example above, we assign the **b** parameter a default value of 10 (**b=10**).  This default value can be overridden by passing a parameter when invoked.

**Arguments**

Functions have a property called **arguments** that allow us to get all the parameters passed as an array. 

**Arguments** allow us to access **parameters** without having to explicitly define them. This is useful if we have more than the defined number of parameters passed to a function.

```javascript
function recipe (ing1,ing2,ing3) {
	return ing1 + " " + ing2 + " " + ing3;
}

//is same as
function recipe () {
	const args = arguments;
	return args[0] + " " + args[1] + " " + args[2];
}

recipe ("onion", "carrot", "salt"); //Returns "onion carrots salt"
```

We can use the **arguments** array to get the supplied parameters as an array. We can then pick our parameters from the arguments array. 

We access items in an array by using the index (position) in any array in square brackets e.g. **array[1]**.

**Spread parameters**

**Spread parameters**, available in **ES6**, are an improvement on arguments. Spread parameters allow us to represent an array without having to be explicit what is in the array.

```javascript
function recipe (...ings) {
	let str = "";
	ings.forEach((ing) => {
		str += " " + ing;
	});
	return str;
}

recipe ("onion", "carrot", "salt"); //Returns "onion carrots salt"

recipe ("onion", "carrot", "salt", "pepper"); //Returns "onion carrots salt pepper"
```

Spread parameters have two advantages over using arguments.

 - You can iterate through the values with forEach.
 - We write less code to do more.

We can also use the **spread parameter** to combine arrays.

```javascript
var eFruits = ["pineapple","kiwi"];
var fruits = ["apple",...eFruits,"orange"]

console.log(fruits) //Returns ["apple","pineapple","kiwi","orange"]

```

**Scope**

**Scope** defines what a function has access to for reading, writing or invoking. You create **scope** by where you initially define a variable or function.

There are 3 types of scope in Javascript:

 - **Global scope** - i.e. this is accessible from everywhere
 - **Local or Function scope** - i.e. this is accessible from within the same function
 - **Block scope** - i.e. this is accessible from inside the expression e.g. inside curly brackets **{}**. 

**Global Scope**

**Global scope** is available everywhere in your code. It exists outside functional blocks and code encapsulation. **Global scope** also means that the defined functions or variables exist on the **window object**. 

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

>Whilst it might seem useful to have **variables** accessible from everywhere, you should try and structure your code so you have as few **global scoped variables** as possible. This will make your code easier to maintain and to test.

**Function Scope**

**Function scope** does encapsulate you variables and functions within your application. 

You use **function scope** to make code and information only accessible to your application and not any other applications that might be also be running.

```javascript
function printName (surname) {
	const firstname = 'Edward'; //Function scoped
	return firstname + ' ' + surname; 
}

printName("Smith") // returns "Edward Smith"
console.log(firstname) // ReferenceError
```

In the above example, we have defined a **firstname** inside a **function**, and then it will be in **functional scope**. This is only accessible inside the function and not outside it. 
 
If we try to access **firstname** outside the function, we will get a **reference error**.

**Block Scope**

**Block scope** is even more granular than **function scope**. **Block scope** can be used to make even smaller areas of an application can access only specific code and information.

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

When we define a variable inside curly brackets **{}**, an **if()** statement in our example, this will now exhibit **block scope**. T

his is only accessible inside the curly brackets **{}** and not outside it (not in the parent function or any other function).

Before **ES6**, the latest released javascript version, javascript didn't have the concept of **block scope**. 

We can still be backwards compatible by still using the **var** which doesn't exhibit block scope. **Let** and **const** both exhibit **block scope**. 

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

>**Functional scope** is just a javascript concept. In other coding languages **block scope** would include **functional scope** (as they both are defined inside curly brackets **{}**).

**Using scope in a web application**

When we are coding our web applications, we use scoping to allow us to control what each function can do and what variables are readable and writable.

```javascript
let soldierRole = "Obeys all orders";

function giveOrder (currentRole, newRole) {
	currentRole = newRole;
}

giveOrder(soldierRole, "Peel potatoes"); //soldierRole is now "Peel potatoes"
```

We have create a function called **giveOrder()** that amends the  **soldierRole**. The **soldierRole** variable and **giveOrder()** function are both defined in the **global scope**. 

The **giveOrder()** function can read and write to the **soldierRole**.

```javascript

let soldierRole = "Obeys all orders";

function giveOrder (currentRole, newRole) {
	currentRole = newRole;
}

function barracks () {
	let sergeantRole = "Gives orders to Soldier";
	giveOrder(soldierRole, "Peel potatoes"); //soldierRole is now "Peel potatoes"
	giveOrder(sergeantRole, "Peel potatoes"); //sergeantRole is now "Peel potatoes"
}

giveOrder(sergeantRole, "Peel potatoes"); //Reference Error
```

Now we define a **barracks()** function and inside this function, we define a **sergeantRole** variable. 

Inside the **barracks()** function, we can access the **giveOrder()** function and **soldierRole** variable because they are **globally scoped**. 

Inside the **barracks()** function, we can give orders to the **soldierRole** and the **sergeantRole**. Outside the **barracks()**, we can only give orders to the **soldierRole**. 

The **sergeantRole** variable is functionally scoped.

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

> a function with a function, where the inner function has access to the variables and functions defined in the outer function.

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

This is acceptable when you're the only developer working on the code but the this approach can become unmanageable in bigger teams. 

Properties and methods can be amended with no structure or process. This will result in the code becoming brittle.

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

We expand our example to create **public** and **private methods**, and **public** and **private properties**.

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

We have used **closures** to create a container for our web application. The **closure** that allows us to expose just the methods and properties that are appropriate.

**Hoisting**

Hoisting is not so much a concept but more of a feature of javascript to beware of. It is important to understand hoisting so that you don't create bugs in your code.

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
In the above example, both functions perform the same task. They return **x**. 

In **notHoisted()** we declare **x**, then assign **x** a value of 1 and return **x**.

In **hoisted()** we assign **x** a value of 1, then return **x** and finally declare **x**. This looks like it should not work. You would expect an error, as **x** is not declared when we return it.

Javascript will always move the declaration of a variable to the top of a function at run time. This is called **hoisting**.

**Hoisting** is a little different with **var**, than it is with **let** or **const**. If we initialize (assign a value) and declare a variable at the same time, then we get slightly different errors.

```javascript
function() {
    x; // undefined
    y; // Reference error: y is not defined
    z; // Reference error: z is not defined

    var x = "local";
    let y = "local";
    const z = "local";
}
```

To avoid having to worry about **hoisting**, we simply always declare our variables at the top of our code.

>Tip

>Always declare your variables (**var**, **let** or **const**) at the top of your functions. this makes your code easier to read and perform as expected. 

```javascript
function() {
    var x = "local";
    let y = "local";
    const z = "local";

	//Define the rest of your statements below the variable definitions
}

```

**What is the difference between a method and a function?**

A method is just a function that exists as a property of an object. 

```javascript

function add (a, b) {
	return a + b;
}

const object = {
	add : function (a, b) {
		return a + b;
	}
}

add(1,2) //returns 3
object.add(1,2) //returns 3
```

The **add(**) function does the same task as the **object.add()** method. The only difference is that the method defined as the property of an object.


Iteration
----------

Iteration is when a process or sequence repeated. In javascript, we commonly iterate through items in an array, iterate over properties in an object or just perform a task a number of times.

**Iterating a set number of times**

Sometimes we may want to perform a task a set number of times. For example, we might want to just select 3 items from a larger list of items or keep iterating until some condition is met.

**while and do while loops**

A **while** loop checks a condition and then runs through the loop if met.

```javascript
let check = true;
let string = "The count is:";
let x = 0;

while (check) {
	x++;
	string += x;
	if(x > 3) {
		check = false;	
	}
} //string is "The count is:123"
```
In this example, we have a condition test on the boolean **check**. If it is *true*, then we loop, if *false* then we stop. In the body of the **while** loop, we increment **x** and append the number to a **string**.

**Do while** loops are similar to **while** loops but the condition is checked after the loop.

```javascript
let i = 0;
let string = "The count is:";

do {
	string += i; 
	i++;
} while (i < 5); //string is "The count is:12345"

```
Our condition (**i <5**) happens after we run our loop rather than before. A **do while** loop is guaranteed to run at least once.

**Iterating over items in an array**

Javascript gives us both native functions and Array prototypal methods (i.e. methods that exist on the array data type) to iterate over arrays.

**For statement**

```javascript
const fruits = ["banana","apple","orange"];

for(let i = 0; i < fruits.length; i++) {
	if(fruits[i] === "orange") {
		window.alert("Array contains an Orange");
	}
}
```

This may look complicate initially. Let us break it down into all its elements and it will become easier to understand. 

We define our **for** statement with an initial expression (**let i = 0**) - start with **i** to equal **0**. 

The condition (**i < fruits.length**) - keep looping over the array until we have no items left to loop over. Remember that the **length** attribute returns the number of items in an array. 

Finally, the increment expression (**i++**), increment **i** by one on each loop through.

We have an **If()** statement that checks the value of the item (**fruits[i]**), and if it is **orange**, then we create a popup with the content of "Array contains an Orange".

```javascript
const fruits = ["banana","apple","orange"];

fruits[0] //equals "banana"
fruits[1] //equals "apple"
fruits[2] //equals "orange"
```

We can pick any item of an array by adding the index (the numeric position in an array) to proceeding square brackets **[]**.

>**Tip**

>Array indexes always start with 0 (and not 1). The length of an array will bring back the number of items. We can get the last item in an array with **array[array.length -1]**.

**ForEach method**

**Foreach()** is a method you have available when you define a data type of **array**.

```javascript
const fruits = ["banana","apple","orange"];

fruits.forEach(function(fruit) {
	if (fruit === "banana") {
		window.alert("Array contains an Banana");
	}
}); //Using Anonymous Function

fruits.forEach((fruit) => {
	if (fruit === "banana") {
		window.alert("Array contains an Banana");
	}
}); //Using Arrow Function
```

In the above example, we use the **forEach()** method to pick out each item in the array, and then pass the item to a function. We then check for the **banana** item and trigger a popup.

We pass a function to **ForEach()** to do work in the items of the array. This passed function is called a **callback**. The **callback** function is usually an **anonymous** function.

**Foreach ()** is useful for dealing with collections (an **array** of **objects**).

```javascript
const people = [
	{name:'Ted', age: 32 },
	{name:'Fred', age: 18 }
];

people.forEach((person) => {
	console.log(person.name); //returns "Ted" and then "Fred"
});
```

We can access the properties of the people with dot notation (i.e. **person.name**).

**Map method**

The **map()** method, like the **foreach()** method, is a available to all array data types. **Map()** will iterate over an array, but unlike **foreach()**, will return an array back.

```javascript
const people = [
	{name:'Ted', age: 32 },
	{name:'Fred', age: 18 }
];

const ages = people.map((person) => {
	return person.age;
}); //returns [32,18]
```

**Map()** allows you can transform an array into another array. In the example above, we pick the ages from the **people** collection and return an **ages** array.

**Iterating through properties of an object**

Often **objects literals** are structured in such a way to help retrieval of data. Object that have a objects as properties can be referred to as **nested objects**.

**For in statement**

The **for in** statements, unlike the **for** statement, is used with objects rather than arrays.

```javascript
const family = {
	ted : {
		age : 14,
		gender : "male"
	},
	sally : {
		age : 16,
		gender : "female"
	},
	peter : {
		age : 46,
		gender : "male"
	}
};

console.log(family.ted.age); //returns 14
console.log(family.peter.gender); //returns male

for (let person in family) {
	console.log(person); //Returns ted,sally,peter
	console.log(family[person].age) //Returns 14,16,46
}

```

In the above example, we have defined an **object literal** called family. We use the **for in** loop to iterate over each of the top level  properties of the object (ted, sally and peter) and exposes them as **person** in the **for** loop. 

We can then use the **person** response to inspect the **family** object. Note how we can traverse the **family** object with **dot notation**

>Tip

>**Dot notation** (for example, **family.ted.age**) is used to navigate to data within the **nested object**. The dot is used to signify a property that exists on an object.

**Getting keys from an object**

We can turn the **keys** (properties) of an object in to an array and iterate through the new array to traverse an **object**.

```javascript
const family = {
	ted : {
		age : 14,
		gender : "male"
	},
	sally : {
		age : 16,
		gender : "female"
	},
	peter : {
		age : 46,
		gender : "male"
	}
};

const keys = Object.keys(family); //returns ["ted","sally","peter"] 

keys.forEach((key) => {
	console.log(family[key].age) //returns 14,16,46
});
```

We have used the **Object.keys()** method to pick the top level property names from the **family** object and put them in an array called **keys**. 

We can then use the **forEach()** method to loop through the **keys** array and traverse the **family** object.

Recursion
------------

**Recursion** is a form of iteration where a **recursive** function repeatedly calls itself until it arrives at a result.

```javascript
const countdown = function(value) {
    if (value > 0) {
        return countdown(value - 1);
    } else {
        return value;
    }
};

countdown(5); //Returns 5,4,3,2,1
```

In the example above, we define a function called **countdown()**. **Countdown()** can re-invoke itself if a condition is met (**value > 0**) otherwise it just returns the result. 

**Countdown()** is a **recursive function**.

**When to use recursion**

Most **for** statements and **while** loops can be rewritten in a **recursive** style. **Recursive** functions are most effective for:

 - solving iterative mathematical problems (fibonacci, factorials)
 - traversing the nodes of complex **objects**.
 - sorting large data sets

**When to not use recursion**

It is possible to crash the browser with incorrectly written recursive functions. 

```javascript
const countdown = function(value) {
    return countdown(value - 1);
};

countdown(5); //Error Maximum call stack size exceeded
```
In this example, we aren't providing a condition that stops recursion. The function will keep running until the browser throws a **Maximum call stack size exceeded** error.

>**Tip**

>You must always provide a condition that will be met when writing recursive functions. If not, you can crash the browser.

**Recursion to calculate a factorial**

A factorial is a product of an integer and all the integers below it.

```javascript
function factorial (n) {
    if (n === 0) {
        return 1
    } else {
        return n * factorial(n - 1);
    }
};

factorial(3) //Returns 6 (e.g 3 * 2 * 1)
factorial(4) //Returns 24 (e.g 4 * 3 * 2 * 1)
factorial(5) //Returns 120 (e.g 5 * 4 * 3 * 2 * 1)
```

In the above example, we recursively call **factorial()** until the condition is met (**n ===0**) and then we return the result.

**Recursion to calculate the Fibonacci sequence**

The Fibonacci sequence was developed as an idealized representation of a rabbit population. 

The assumption is a newly born pair of rabbits, one male, one female, are put in a field. The rabbits are able to mate at the age of one month so that at the end of its second month a female can produce another pair of rabbits;. The rabbits never die and a mating pair always produces one new pair. 

The sequence, after twelve months, looks like:

1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144

```javascript
function fibonacci(n) {
	if (n <= 1){
	    return n;
	} else {
	    return fib(n-1) + fib(n - 2);
	}
}

console.log(fib(9)); //Returns 34
console.log(fib(11)); //Returns 89
console.log(fib(12)); //Returns 144
```

The above **fibonacci()** takes an argument of the number of months and returns the number of rabbits.

>**Tip**

>We can improve this function by taking in to account **Tail Call Optimization** which improves the memory footprint of our recursive functions. We shall address this latter in the book.

Generator Functions
------------------------------

**Generator functions** are new to javascript in ES6. A **generator function** is used for defining an iterator that can maintain its own state. The generated iterator can also be paused and resumed.

```javascript
function *countToThree() {
	yield 1;
	yield 2;
	yield 3;
}

const count = countToThree();

count.next(); //Returns {value: 1, done: false}
count.next(); //Returns {value: 2, done: false}
count.next(); //Returns {value: 3, done: false}
count.next(); //Returns {value: undefined, done: true}
```  

The **generator function** is defined with an asterisk (\*) and has one or more **yield** expressions.

We invoke the **countToThree()** generator function to the **count** constant. **Count** is now iterable. We can step through each iteration when we call **next()**. 

The returned object has a **value**, which is  yielded by the **generator** function, and a **done** boolean, which indicates if we have complete all yields.

**Why use generator functions?**

Generator functions initially can look cumbersome compared to simple **for** statements or **while** loops. Generators can be powerful when considering iterables are not finite.

```javascript
function *stateful(x) {
    while(true) {
        x = x * 2;
        yield x;
    }
}

const state = stateful(1);
state.next(); // {value: 2, done: false}
state.next(); // {value: 4, done: false}
state.next(); // {value: 8, done: false}
```

In the above example, notice how the value of **x** is maintained on every **next()**.  We do not need to manage the value of **x** outside the generator function like we do with **for** statements and **while** loops.

Our generator function has also created a potentially infinite iterable value, we will never reach **{ done : true }**. We have not had to define a huge array to iterate through, it has been created programmatically.


Summary
-----------

In this chapter, we have introduced a number of core concepts and behavior that inform how you code Javascript applications.

We have introduced:

 - How we can define our functions.
 - How scope determines what our functions can access
 - How closures can be used to structure our applications
 - How to iterate over arrays and objects
 - How we can use recursion to enhance our iteration
 - How generator functions work, and their advantages used to iterate
 
In the next chapter, we will at how to create classes. Classes, introduced in ES6, are a new canonical (preferred) way to structure your web applications. 



