# Class 6

What Is JavaScrtipt?

JavaScript is a coding language that uses functions to tell the computer to do cetain thing that help people actually interact with the website/game/software. This is refered to as `dynamics`.

`API (application programming interface)` - which is a set of definitions and protocols for building and integrating application software

APIs let your product or service communicate with other products and services without having to know how they’re implemented. This can simplify app development, saving time and money.

The `Document Object Model (DOM)` connects web pages to scripts or programming languages by representing the structure of a document—such as the HTML representing a web page—in memory. Usually it refers to JavaScript, even though modeling HTML, SVG, or XML documents as objects are not part of the core JavaScript language.

The `DOM` represents a document with a logical tree. Each branch of the tree ends in a node, and each node contains objects. DOM methods allow programmatic access to the tree. With them, you can change the document's structure, style, or content.

We can distinguish 3 major parts of what we usually refer to as "JavaScript".

- The language itself. This is fairly standard among the various environments, both in the various browsers and in the various server-side environments.

- The DOM API - how the language can interact with the various parts of a web page while in the browser. While in this respect the various browsers are getting closer to each other they still differ. Several libraries, most prominently JQuery, is trying to provide a unified API.

- The server API (or just API) provided by Node.js or one of the other server-side systems.

## How to implement JavaScript

You can either embed the JavaScript code directly inside the HTML file, or you can put a line in the HTML file that will include the external JavaScript file.

### Non-Embeding

Simply add a file and label it `script.js`
Then, anywhere you want, in the HTML file type:

`<script src="script.js"></script>`

### Embeding

In order to do that we add the `<script>` opening and `</script>` closing tags. Between the two we write our JavaScript code.

Example:

`<script language="javascript">`

`alert("Hello World");`

`</script>`

## Coding in JS

## Alert

This will show a pop-up in the browser with the text. (You can click on Try! that will open the specific script in a separate window.) The alert() function is actually rarely used, but it is an easy way to show the use of JavaScript.

### Example

`<script language="javascript">`

#### ***`alert("Hello World");`***

`</script>`

## Document.write

In this example we have some text (First line), then the JavaScript code, and then some more text (Last line). The JavaScript code uses the `document.write` function to change the content of the page. It will embed the html snippet`<h1>Hello World</h1>` after the "First line", but before the "Last line".

### Example

`<script>`

***`document.write("<h1>Hello World</h1>");`***

`</script>`

## Prompt()

This one is called prompt. It will show a pop-up window with the text provided as the first parameter and with a textbox the user can fill in. When the user presses OK, the value in the text box will be returned by the `prompt()` function. Then, in this example we use the `document.write` method to update the html with the text.

### Example

`<script>`

`var name = prompt("Your name:", "");`

`document.write("Hello ", name);`

`</script>`

## Confirm()

The other pop-up is not really an input method. It allows the developer to ask a Yes/No question. Calling the `confirm()` function will show a pop-up window with the provided texts and with two buttons. If the user presses OK the `confirm()`
function will return true, if the user presses cancel or hits the ESC key, the function will return false.

In order for this to make more sense you'll have to understand what true and false really mean and what this `if - else` construct does.

- That code can basically be translated to the following
English sentence:

- `If confirm returned true, print "Hello World", otherwise`
`print "OK, I won't print it."`

- Or even better:

- `If the user presses OK when we asked "Shall I print Hello`
`World?", then print "Hello World", otherwise print "OK, I`
`won't print it."`

### Example

`<script>`

`if (confirm("Shall I print Hello World?")) {`

   `document.write("Hello World");`

`} else {`

 ``document.write("OK, I won't print it.");``

`}`

`</script>`

## Varibles

All JavaScript variables must be identified with unique names.

These unique names are called identifiers.

Identifiers can be short names (like x and y) or more descriptive names (age, sum, totalVolume).

The general rules for constructing names for variables (unique identifiers) are:

- Names can contain letters, digits, underscores, and dollar signs.

- Names must begin with a letter.

- Names can also begin with $ and _ (but we will not use it in this tutorial).

- Names are case sensitive (y and Y are different variables).
Reserved words (like JavaScript keywords) cannot be used as names.

## The Assignment Operator

In JavaScript, the equal sign `(=)` is an "assignment" operator, not an "equal to" operator.

JavaScript variables can hold numbers like 100 and text values like "John Doe".

In programming, text values are called text strings.

JavaScript can handle many types of data, but for now, just think of numbers and strings.

Strings are written inside double or single quotes. Numbers are written without quotes.

If you put a number in quotes, it will be treated as a text string.

`const pi = 3.14;` (integer)

`let person = "John Doe";` (string)

`let answer = 'Yes I am!';` (string)

## Declaring a Variable

Creating a variable in JavaScript is called "declaring" a variable.

You declare a JavaScript variable with the var or the let keyword:

`var carName;`

`let carName;`

After the declaration, the variable has no value (technically it is undefined).

To assign a value to the variable, use the equal sign:

`carName = "Volvo";`

You can also assign a value to the variable when you declare it:

`let carName = "Volvo";`

### One Statement, Many Variables

You can declare many variables in one statement.

Start the statement with let and separate the variables by comma:

Example:

`let person = "John Doe", carName = "Volvo", price = 200;`

But, a declaration can span multiple lines:

Example:

`let person = "John Doe",`

`carName = "Volvo",`

`price = 200;`

## JavaScript Arithmetic

As with algebra, you can do arithmetic with JavaScript variables, using operators like = and +:

Example:

`let x = 5 + 2 + 3;`

You can also add strings, but strings will be concatenated:

Example:

`let x = "John" + " " + "Doe";`

Also try this:

Example:

`let x = "5" + 2 + 3;`

## How Computers Work

A computer's job is to take in info, store recieved info, process info, and then output the result of the process.

1. Input

2. Storage

3. Process

4. Output

### What makes a Computer a Computer?

As humans, we've always built tools to help us solve problems.

Tools like a wheelbarrow, a hammer, or a printing press, or a tractor-trailer.

All of these inventions helped us with manual work.

Over time, people began to wonder if a machine could be designed and built to help us with the thinking work we do, like solving equations or tracking the stars in the sky.

All these different inputs give a computer information, which is then stored in memory.
A computer's processor takes information from memory.
It manipulates it or changes it using an algorithm,
which is just a series of commands.

How a computer outputs information depends on what the computer is designed to do.
A computer display can show text, photos, videos, or interactive games -- even virtual reality!
The output of a computer may even include signals to control a robot.
And, when computers connect over the Internet,
the output from one computer becomes the input to another, and vice versa.

### Binaryand Data

Inside a computer are electric wires and circuits that carry all the information in a computer.

If you have a single wire with electricity flowing through it,
the signal could either be on or off.
With one wire, we can represent a yes or no,
true or false,

This on/off state of a single wire is called a `bit`,
and it's the smallest piece of information a computer can store.

If you use more wires you get more bits: more ones and zeros.
With more bits you can represent more complex information.

Anything can be expressed in the form of number such as:

- Sound - Vibrations can be represented graphically as a waveform.

- Pictures/Video - All of these images are made out of teeny dots called pixels,and each pixel has a color. Each of the colors can be represented with numbers.

- Text - Every word you see on every webpage or your phone is represented using a system like binara.

- Ect...

## Circuits and Logic

In order to process the information that comes in as input, and to make the information that is output, a computer needs to modify and combine the input signals.

To do this, a computer uses millions of teeny electronic components, which come together to form `circuits`.

By connecting these `circuits` together, we can make more complex circuits that perform more complex calculations.

In fact, all the information processing your computer does is just lots and lots of small simple operations put together.

Each individual operation done by a computer is so, so simple it could be done by a human,
but these circuits inside computers are way way faster.

### Why are smaller computers faster?

Well, because the smaller the circuit is, the less distance the electrical signal has to go.

Electricity moves at just about the speed of light, which is why modern circuits can perform billions of calculations per second.

## Things I want to learn more about are:

- How to make circuits

- Different types of circuits

- Relearn binary

[Back to home page](../../README.md)
