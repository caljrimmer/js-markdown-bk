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
 
```
window.alert('hello');
```
The **window** object is where all native global JavaScript objects, functions, and variables reside in the browser. The **alert** is a function that Javascript provides to allow you to easily create pop-ups. 

A **function** in javascript is invoked with parentheses and inside the parentheses arguments can be passed. 

we use a semicolon to separate statements. 

Now let's make a simple function to capture a user's response and return the value.
```
const result = (message) => {
	return window.confirm(message);
}
result('Do you confirm this action?');
```

The console should log *true*, if ok is clicked and *false* if cancel is clicked.

So we have create a new function called **result** that returns a value that we get from another native javascript function called **confirm**. We then invoke our result function with parentheses whilst passing a string of 'Do you confirm this action?' as an argument.

We also use the **const** keyword to declare our function. Const  creates a read-only reference to the function. This means the function can not be amended after it has been declared.

We don't need to specify **window** when calling functions. Javascript will assume it for you. Thus these two function do the same thing.
```
window.alert('hello');
alert('hello'); //Same

window.confirm('confirm?');
confirm('confirm?'); //Same
```

> **Recap**

>The **window** object is global and contains all native Javascript functions and variables. 

>A **function** can be passed arguments and is invoked with parentheses.

Variables and Constants
-----------------------------

Javascript allows us to define containers to store data, objects or functions in. Defining these containers allow us to structure our code and to manage scope (i.e. ability to access the container). There are 3 ways to define a container:

Use a **variable** declaration.
```
var z;
var x = 1;
var y = 2;
z = x + y; // z equals 3 now
```

You can define a variable with a value or without a value and populate it later. All JavaScript variables must be identified with unique names.

Use a **let** declaration.
```
let sentence;
let name = 'Ted;
sentence = 'My name is ' + y; // sentence equals 'My name is Ted'
```

**Let** is similar to a variable declaration. **Let**, unlike **var**, cannot be hoisted and it exhibits block scope. We will discuss scope and hoisting later in the book. 

Use a **const** declaration.
```
const PI = 3.14;
PI = 3.145 //Throws an error
```

**Const** declared with a given value can not be changed. It is used, as it's name suggests, to define constants. **Const**, like **let**, also cannot be hoisted and it exhibits block scope.

It is possible to declare a container without using **var**, **let** or **const**.

```
name = 'Ted'; //same as window.name = 'Ted'
x = 1; //same as window.x = 1
```

Declaring a container this way adds the container on to the window object and it becomes globally available. This is considered bad practice because relying too much on global containers can result in collisions between various scripts on the same page.

Best practise is to use **let** and **const**. Block scoping means your containers will act in a more granular and predictable way.

What is Scope
-----------------

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


#### <i class="icon-folder-open"></i> Switch to another document

All your local documents are listed in the document panel. You can switch from one to another by clicking a document in the list or you can toggle documents using <kbd>Ctrl+[</kbd> and <kbd>Ctrl+]</kbd>.

#### <i class="icon-pencil"></i> Rename a document

You can rename the current document by clicking the document title in the navigation bar.

#### <i class="icon-trash"></i> Delete a document

You can delete the current document by clicking <i class="icon-trash"></i> **Delete document** in the document panel.

#### <i class="icon-hdd"></i> Export a document

You can save the current document to a file by clicking <i class="icon-hdd"></i> **Export to disk** from the <i class="icon-provider-stackedit"></i> menu panel.

> **Tip:** Check out the [<i class="icon-upload"></i> Publish a document](#publish-a-document) section for a description of the different output formats.


----------


Synchronization
-------------------

StackEdit can be combined with <i class="icon-provider-gdrive"></i> **Google Drive** and <i class="icon-provider-dropbox"></i> **Dropbox** to have your documents saved in the *Cloud*. The synchronization mechanism takes care of uploading your modifications or downloading the latest version of your documents.

> **Note:**

> - Full access to **Google Drive** or **Dropbox** is required to be able to import any document in StackEdit. Permission restrictions can be configured in the settings.
> - Imported documents are downloaded in your browser and are not transmitted to a server.
> - If you experience problems saving your documents on Google Drive, check and optionally disable browser extensions, such as Disconnect.

#### <i class="icon-refresh"></i> Open a document

You can open a document from <i class="icon-provider-gdrive"></i> **Google Drive** or the <i class="icon-provider-dropbox"></i> **Dropbox** by opening the <i class="icon-refresh"></i> **Synchronize** sub-menu and by clicking **Open from...**. Once opened, any modification in your document will be automatically synchronized with the file in your **Google Drive** / **Dropbox** account.

#### <i class="icon-refresh"></i> Save a document

You can save any document by opening the <i class="icon-refresh"></i> **Synchronize** sub-menu and by clicking **Save on...**. Even if your document is already synchronized with **Google Drive** or **Dropbox**, you can export it to a another location. StackEdit can synchronize one document with multiple locations and accounts.

#### <i class="icon-refresh"></i> Synchronize a document

Once your document is linked to a <i class="icon-provider-gdrive"></i> **Google Drive** or a <i class="icon-provider-dropbox"></i> **Dropbox** file, StackEdit will periodically (every 3 minutes) synchronize it by downloading/uploading any modification. A merge will be performed if necessary and conflicts will be detected.

If you just have modified your document and you want to force the synchronization, click the <i class="icon-refresh"></i> button in the navigation bar.

> **Note:** The <i class="icon-refresh"></i> button is disabled when you have no document to synchronize.

#### <i class="icon-refresh"></i> Manage document synchronization

Since one document can be synchronized with multiple locations, you can list and manage synchronized locations by clicking <i class="icon-refresh"></i> **Manage synchronization** in the <i class="icon-refresh"></i> **Synchronize** sub-menu. This will let you remove synchronization locations that are associated to your document.

> **Note:** If you delete the file from **Google Drive** or from **Dropbox**, the document will no longer be synchronized with that location.

----------


Publication
-------------

Once you are happy with your document, you can publish it on different websites directly from StackEdit. As for now, StackEdit can publish on **Blogger**, **Dropbox**, **Gist**, **GitHub**, **Google Drive**, **Tumblr**, **WordPress** and on any SSH server.

#### <i class="icon-upload"></i> Publish a document

You can publish your document by opening the <i class="icon-upload"></i> **Publish** sub-menu and by choosing a website. In the dialog box, you can choose the publication format:

- Markdown, to publish the Markdown text on a website that can interpret it (**GitHub** for instance),
- HTML, to publish the document converted into HTML (on a blog for example),
- Template, to have a full control of the output.

> **Note:** The default template is a simple webpage wrapping your document in HTML format. You can customize it in the **Advanced** tab of the <i class="icon-cog"></i> **Settings** dialog.

#### <i class="icon-upload"></i> Update a publication

After publishing, StackEdit will keep your document linked to that publication which makes it easy for you to update it. Once you have modified your document and you want to update your publication, click on the <i class="icon-upload"></i> button in the navigation bar.

> **Note:** The <i class="icon-upload"></i> button is disabled when your document has not been published yet.

#### <i class="icon-upload"></i> Manage document publication

Since one document can be published on multiple locations, you can list and manage publish locations by clicking <i class="icon-upload"></i> **Manage publication** in the <i class="icon-provider-stackedit"></i> menu panel. This will let you remove publication locations that are associated to your document.

> **Note:** If the file has been removed from the website or the blog, the document will no longer be published on that location.

----------


Markdown Extra
--------------------

StackEdit supports **Markdown Extra**, which extends **Markdown** syntax with some nice features.

> **Tip:** You can disable any **Markdown Extra** feature in the **Extensions** tab of the <i class="icon-cog"></i> **Settings** dialog.

> **Note:** You can find more information about **Markdown** syntax [here][2] and **Markdown Extra** extension [here][3].


### Tables

**Markdown Extra** has a special syntax for tables:

Item     | Value
-------- | ---
Computer | $1600
Phone    | $12
Pipe     | $1

You can specify column alignment with one or two colons:

| Item     | Value | Qty   |
| :------- | ----: | :---: |
| Computer | $1600 |  5    |
| Phone    | $12   |  12   |
| Pipe     | $1    |  234  |


### Definition Lists

**Markdown Extra** has a special syntax for definition lists too:

Term 1
Term 2
:   Definition A
:   Definition B

Term 3

:   Definition C

:   Definition D

	> part of definition D


### Fenced code blocks

GitHub's fenced code blocks are also supported with **Highlight.js** syntax highlighting:

```
// Foo
var bar = 0;
```

> **Tip:** To use **Prettify** instead of **Highlight.js**, just configure the **Markdown Extra** extension in the <i class="icon-cog"></i> **Settings** dialog.

> **Note:** You can find more information:

> - about **Prettify** syntax highlighting [here][5],
> - about **Highlight.js** syntax highlighting [here][6].


### Footnotes

You can create footnotes like this[^footnote].

  [^footnote]: Here is the *text* of the **footnote**.


### SmartyPants**strong text**


SmartyPants converts ASCII punctuation characters into "smart" typographic punctuation HTML entities. For example:

|                  | ASCII                        | HTML              |
 ----------------- | ---------------------------- | ------------------
| Single backticks | `'Isn't this fun?'`            | 'Isn't this fun?' |
| Quotes           | `"Isn't this fun?"`            | "Isn't this fun?" |
| Dashes           | `-- is en-dash, --- is em-dash` | -- is en-dash, --- is em-dash |


### Table of contents

You can insert a table of contents using the marker `[TOC]`:

[TOC]


### MathJax

You can render *LaTeX* mathematical expressions using **MathJax**, as on [math.stackexchange.com][1]:

The *Gamma function* satisfying $\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$ is via the Euler integral

$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$

> **Tip:** To make sure mathematical expressions are rendered properly on your website, include **MathJax** into your template:

```
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
```

> **Note:** You can find more information about **LaTeX** mathematical expressions [here][4].


### UML diagrams

You can also render sequence diagrams like this:

```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

And flow charts like this:

```flow
st=>start: Start
e=>end
op=>operation: My Operation
cond=>condition: Yes or No?

st->op->cond
cond(yes)->e
cond(no)->op
```

> **Note:** You can find more information:

> - about **Sequence diagrams** syntax [here][7],
> - about **Flow charts** syntax [here][8].

### Support StackEdit

[![](https://cdn.monetizejs.com/resources/button-32.png)](https://monetizejs.com/authorize?client_id=ESTHdCYOi18iLhhO&summary=true)

  [^stackedit]: [StackEdit](https://stackedit.io/) is a full-featured, open-source Markdown editor based on PageDown, the Markdown library used by Stack Overflow and the other Stack Exchange sites.


  [1]: http://math.stackexchange.com/
  [2]: http://daringfireball.net/projects/markdown/syntax "Markdown"
  [3]: https://github.com/jmcmanus/pagedown-extra "Pagedown Extra"
  [4]: http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference
  [5]: https://code.google.com/p/google-code-prettify/
  [6]: http://highlightjs.org/
  [7]: http://bramp.github.io/js-sequence-diagrams/
  [8]: http://adrai.github.io/flowchart.js/
