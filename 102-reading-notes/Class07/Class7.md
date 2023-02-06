# MDN Control Flow 

The control flow is the order in which the computer executes statements in a script.

Code is run in order from the first line in the file to the last line, unless the computer runs across the (extremely frequent) structures that change the control flow, such as conditionals and loops.

To do this, the script uses a conditional structure or if...else, so that different code executes depending on whether the form is complete or not:

`if (isEmpty(field)) {`

 ` promptUser();`

`} else {`

  `submitForm();`

`}`

A typical script in JavaScript or PHP (and the like) includes many control structures, including conditionals, loops and functions.

For example, the above excerpt might be inside a function that runs when the user clicks the Submit button for the form. The function could also include `a loop, which iterates through all of the fields in the form`, checking each one in turn.

Control flow means that when you read a script, you must not only read from start to finish but also look at program structure and how it affects order of execution.

## Functions

A JavaScript function is a block of code designed to perform a particular task.

A JavaScript function is executed when "something" invokes it (calls it).

### JavaScript Function Syntax

A JavaScript function is defined with the function keyword, followed by a name, followed by parentheses ().

`function name(parameter1, parameter2, parameter3) {`

`}`

Function parameters are listed inside the parentheses () in the function definition.

Function arguments are the values received by the function when it is invoked.

Js is defined with the function keyword, follow by name, followed by paraentheses().

`function nameFunction()`

Functions names can be anything and the same thing applies to variables.

#### Function Invocation


The code inside the function will execute when "something" invokes (calls) the function:

- When an event occurs (when a user clicks a button)

- When it is invoked (called) from JavaScript code

- Automatically (self invoked)

### Local Variables

Variables declared within a JavaScript function, become LOCAL to the function.

Local variables can only be accessed from within the function.

Inside the function, the parameters behave as variables that are declared inside of a function or loop. Since they are declared inside of the function, they belong only to that one function and no other functions.

`function myFunction() {`

  `let carName = "Volvo";`

  `// code here CAN use carName`
`}`

Since local variables are only recognized inside their functions, variables with the same name can be used in different functions.

Local variables are created when a function starts, and deleted when the function is completed.

### The () Operator Invokes the Function

Using the example above, toCelsius refers to the function object, and toCelsius() refers to the function result.

Accessing a function without () will return the function object instead of the function result.

`function toCelsius(fahrenheit) {`

  `return (5/9) * (fahrenheit-32);`

`}`

`document.getElementById("demo").innerHTML = toCelsius;`

### Function Return

When JavaScript reaches a `return` statement, the function will stop executing.

If the function was invoked from a statement, JavaScript will "return" to execute the code after the invoking statement.

Functions often compute a return value. The return value is "returned" back to the "caller":

`let x = myFunction(4, 3);`   // Function is called, return value will end up in x

`function myFunction(a, b) {`

  `return a * b;`             // Function returns the product of a and b

`}`

The result in x will be:

12



### Functions Used as Variable Values

Functions can be used the same way as you use variables, in all types of formulas, assignments, and calculations.

Example

Instead of using a variable to store the return value of a function:

`let x = toCelsius(77);`

`let text = "The temperature is " + x + " Celsius";`

You can use the function directly, as a variable value:

`let text = "The temperature is " + toCelsius(77) + " Celsius";`

`function toCelsius(fahrenheit) {`

  `return (5/9) * (fahrenheit-32);`

`}`

In the code above the parameter, 'fahrenheit', became equal to the parameter in the function `to Celsius`
## For loop

Syntax:

`for (statement 1; statement 2; statement 3) {`

  `execute code block`

`}`

- Statement 1 is executed once before the code block is run.

- Statement 2 defines the condition needed to execute the code block.

- Statement 3 is executed every time the code block is run.

Example of real code

`for (let i = 0; i < 10; i++) {`

 `console.log(i);`

`}`

- This loop will print numbers 0-9, will stop when condition is met (i = 10)

- Statement 1 sets the variable for the loop (let i = 0).

- Statement 2 sets the loop condition (i < 10).

- Statement 3 increases the value of i (i++) each time the code block is run.

- This loop will print numbers 0-9, will stop when condition is met (i = 10)

### While loop

Syntax

`while (condition) {`

  `execute code block`

`}`

- The code block will continue to loop as long as the condition is true.

Example of real code:

`let i = 0;`

`while (i < 5) {`

  `console.log(i);`

  `i++;`

`}`

This loop will print number 0-4, will stop when condition becomes false (i >=5)

For the above example, the syntax is as follows:

The code block will continue to run as long as the variable (i) is less than 5.

# Operators

All other operators can be found on in the links below:

[Operator Link Number 1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#basic_expressions)

[Operator Link Number 2](https://www.w3schools.com/js/js_operators.asp)


Types of JavaScript Operators
There are different types of JavaScript operators:

## Arithmetic Operators

used to perform arithmetic on numbers

`let a = 3;`

`let x = (100 + 50) * a;`

![Chart](ArthmeticOperators.png)

## Assignment Operators

assign values to JavaScript variables.


![Chart](AssignmentChart.png)


## Comparison Operators

![Chart](ComparisonOperator.png)

## Logical Operators

![Logical Chart](LogicalOperator.png)

## Type Operators

![Type Operators](TypeOperators.png)


## Conditional Operators

The conditional (ternary) operator is the only JavaScript operator that takes three operands: a condition followed by a question mark (?), then an expression to execute if the condition is truthy followed by a colon (:), and finally the expression to execute if the condition is falsy. This operator is frequently used as an alternative to an if...else statement.

`function getFee(isMember) {`

- `return (isMember ? '$2.00' : '$10.00');`

`}`

`console.log(getFee(true));`

- Expected output: "$2.00"

`console.log(getFee(false));`

- Expected output: "$10.00"

`console.log(getFee(null));`

- Expected output: "$10.00"

## BigInt

values represent numeric values which are too large to be represented by the number primitive

[BigInt Link](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#bigint_operators)

Bitwise - 

A bitwise operator treats their operands as a set of 32 bits (zeros and ones), rather than as decimal, hexadecimal, or octal numbers. For example, the decimal number nine has a binary representation of 1001. Bitwise operators perform their operations on such binary representations, but they return standard JavaScript numerical values.

![Bitwise Chart](BitWise.png)


## String Operator

In addition to the comparison operators, which can be used on string values, the concatenation operator `+` concatenates two string values together, returning another string that is the union of the two operand strings.

`console.log("my " + "string");`

- console logs the string "my string".

Another Example:

`let mystring = "alpha";`

`mystring += "bet";`

- evaluates to "alphabet" and assigns this value to `mystring`.

## Comma Operator 

The comma operator `(,)` evaluates both of its operands and returns the value of the last operand. This operator is primarily used inside a for loop, to allow multiple variables to be updated each time through the loop. It is regarded bad style to use it elsewhere, when it is not necessary. `Often two separate statements can and should be used instead.`

`const x = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];`

`const a = [x, x, x, x, x];``

`for (let i = 0, j = 9; i <= j; i++, j--) {`

  `console.log(`a[${i}][${j}]= ${a[i][j]}`);`

`}`

## Urany operator 

A unary operation is an operation with only one operand.

### delete

The delete operator deletes an object's property. The syntax is:

`delete object.property;`

`delete object[propertyKey];`

`delete objectName[index];`

Object is the name of an object, property is an existing property, and propertyKey is a string or symbol referring to an existing property.

If the delete operator succeeds, it removes the property from the object. Trying to access it afterwards will yield undefined. The delete operator returns true if the operation is possible; it returns false if the operation is not possible.

`delete Math.PI;`

  - returns false (cannot delete non-configurable properties)

`const myObj = { h: 4 };`

`delete myObj.h;`

- returns true (can delete user-defined properties)

## Relational Operator

A relational operator compares its operands and returns a Boolean value based on whether the comparison is true.

### `in operator`

The `in` operator returns true if the specified property is in the specified object. The syntax is:

propNameOrNumber in objectName

where `propNameOrNumber` is a string, numeric, or symbol expression representing a property name or array index, and `objectName` is the name of an object.

- Arrays

`const trees = ["redwood", "bay", "cedar", "oak", "maple"];`

`0 in trees;` 

- returns true

`3 in trees;` 

- returns true

`6 in trees;` 

- returns false

`"bay" in trees;` 

- returns false

- you must specify the index number, not the value at that index

`"length" in trees;`

- returns true (length is an Array property)


- Custom objects

`const mycar = { make: "Honda", model: "Accord", year: 1998 };`

`"make" in mycar;`

- returns true

`"model" in mycar;`

- returns true



### [Relational Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#relational_operators)


[Back to home page](../../README.md)