
Understanding Functions
------------------------------

Functions are objects that are invokable with **()** parentheses. A function is a set of statements that perform a task. 

In order to be able to write functions that work as expected, it is important to understand some of the fundamental expectations of javascript with respect to functions.

We shall look at **scope**, **closures**, **hoisting** and **methods**

**Scope**

Scope defines what a function has access to for reading, writing or invoking. You create scope by where you initially define a variable or function.

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

>Whilst it might seem useful to have **variables** accessible from everywhere, you should try and structure your code so you have as few **global scoped variables** as possible. This will make your code easier to maintain and to test.

**Function Scope**

```javascript
function printName (surname) {
	const firstname = 'Edward'; //Function scoped
	return firstname + ' ' + surname; 
}

printName("Smith") // returns "Edward Smith"
console.log(firstname) // ReferenceError
```

In the above example, we have define a **firstname** inside a **function**, then it will be in **functional scope**. This is only accessible inside the function and not outside it.  If we try to access **firstname** outside the function, we will get a reference error.

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

>**Functional scope** is just a javascript concept. In other coding languages **block scope** would include **functional scope** (as they both are defined inside curly brackets **{}**).

**Using scope in a web application**

When we are coding our web applications, we use scoping to allow us to control what each function can do and what variables are readable and writable.

```javascript
let soldierRole = "Obeys all orders";

function giveOrder (currentRole, newRole) {
	currentRole = newRole;
}

giveOrder(soldierRole, "Peel potatoes");
```

We have create a function called **giveOrder()** that amends the  **soldierRole**. The **soldierRole** variable and **giveOrder()** function are both defined in the **global scope**. The **giveOrder()** function can read and write to the **soldierRole**.

```javascript

let soldierRole = "Obeys all orders";

function giveOrder (currentRole, newRole) {
	currentRole = newRole;
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
In the above example, both functions preform the same task. They return **x**. 

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

Defining functions
---------------------

Functions can be define in a several different ways. In this section, we shall look at what ways we can define functions and what difference that can make to how our functions work.

**Anonymous function** 

An **anonymous function** is a function defined without a name.

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

**Anonymous function** can also be passed in callbacks or as event handlers. For example:

```javascript
el.addEventListener("click", function () {
	return "I was Clicked";
})
```

In this example,  we pass an **anonymous function** which returns a string when the element is clicked. We do not need to re-use this function outside the click event. If we use an **anonymous function**, it mean we have to write less code.

**Function declaration**

A **function declaration** is a named **anonymous function**.

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

**Function constructor**

We can make a function using the **Function()** constructor function.

```javascript
const add = new Function('a', 'b', 'return a + b');
```
We provide the **Function()** constructor with our arguments (**a,b**) and the function body as a string. Any number of arguments can be passed aslong as the function body is the last argument in

**Assign a function to variable**

A function can be assigned to a variable. 

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
multiple(2,2) //returns 4
```

When a function is assigned to a variable, it works the same as a **function declaration**. We can immediately invoke it, or re-use at a later point.

**What is the difference between a method and a function?**

A method is just a function that exists as a property of an object. 

```javascript

function add (a, b) {
	return a + b;
}

const object = {
	add : function (a, b) {
		return a + b;
	},
	addTwice : function (a,b) {
		return 2 * this.add(a,b);
	}
}

add(1,2) //returns 3
object.add(1,2) //returns 3
object.addTwice(1,2) //returns 6
```

A method performs the same role as a function but is defined as a property on an object. A method allows us use the **this** keyword to be self-referential to its containing object. 

**Arrow function**

The latest javascript version, ES6, we have a new way to create a function.  The **arrow function** means you can express more whilst writing less code.

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

const multiplyBy4 = num => num * 4;

multiplyBy2(2); //returns 4
multiplBy4(2); //returns 8 
```
In the above example, we can remove the **return** keyword and parentheses **()** but still perform the same task. **Arrow functions** allow us to do more, with less code. 

The **arrow function** deals with **scope** and the **this** keyword differently than any other function definition. We shall address this later in the book.

>Tip

>The **Arrow function** can also be called **Fat Arrow**.

**What is the best way to define a function?**

There is no right way to define a function. You can choose whichever you feel best suits what you are trying to achieve. A function will always take arguments, run through the defined statements and then return the result. 

 - **Methods** are used most when taking an object oriented approach to structuring your code
 - **Function declarations** are useful if you are taking a functional programming approach to structuring your code
 - **Arrow functions** are useful when you wish to limit the amount of code you write
 - **Anonymous function** are useful for wrapping your web applications (for functional scoping reasons) and when you don't wish to re-use the function

In most web applications, you will see a mix of different ways to define functions. Your main concern is that you should be consistent in how you structure your code.

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

We define our **for** statement with an initial expression (**let i = 0**) - start with **i** to equal **0**. The condition (**i < fruits.length**) - keep looping over the array until we have no items left to loop over. Remember that the **length** attribute returns the number of items in an array. Finally, the increment expression (**i++**), increment **i** by one on each loop through.

We have an **If()** statement that checks the value of the item (**fruits[i]**), and if it is **orange**, then we create a popup with the content of "Array contains an Orange".

```javascript
const fruits = ["banana","apple","orange"];

fruits[0] //equals "banana"
fruits[1] //equals "apple"
fruits[2] //equals "orange"
```

We can pick any item of an array by adding the index (the numeric position in an array) to proceeding square brackets **[]**.

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

**Foreach ()** is useful for dealing with collections (an array of objects).

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

**Map()** allows you can transform an array into another array. In the example above, we pick the ages from the **people** collection and return a simple **ages** array.
