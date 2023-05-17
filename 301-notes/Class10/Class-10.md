# Memory Storage

Here are the answers to your questions using the information from the link "Understanding the JavaScript Call Stack":

1. What is a 'call'?

    In JavaScript, a 'call' refers to the execution of a function. When a function is called, it is added to the call stack, and its code is executed.

2. How many 'calls' can happen at once?

    In JavaScript, only one call can happen at a time. JavaScript is single-threaded, meaning it can only execute one piece of code at a time. Each function call is added to the call stack, and the JavaScript engine executes them one after another.

3. What does LIFO mean?

    LIFO stands for "Last-In, First-Out." It is a principle that describes the order in which function calls are processed in the call stack. The last function that is pushed into the call stack is the first one to be popped out and executed.

4. Draw an example of a call stack and the functions that would need to be invoked to generate that call stack.

    Here's an example of a call stack with three functions: `main`, `firstFunction`, and `secondFunction`.

    ```
       |                     |
       |    secondFunction   |
       |                     |
       |---------------------|
       |    firstFunction    |
       |---------------------|
       |        main         |
       -----------------------
    ```

    In this example, the `main` function is the first function to be called. Inside the `main` function, the `firstFunction` is called, and inside `firstFunction`, the `secondFunction` is called. As each function is called, it is added to the top of the call stack. When a function completes its execution, it is removed from the top of the call stack, and the control goes back to the previous function.

5. What causes a Stack Overflow?

    A Stack Overflow occurs when the call stack exceeds its maximum limit. This usually happens when there is excessive recursion or an infinite loop in the code. When a function calls itself recursively without a proper exit condition, it leads to an ever-growing call stack until it exceeds the available stack size. This results in a Stack Overflow error, indicating that the call stack has reached its maximum capacity.

- Here's an example code snippet that corresponds to the call stack example I provided earlier:

```
function secondFunction() {
  // Code for secondFunction
}

function firstFunction() {
  secondFunction(); // Call to secondFunction
}

function main() {
  firstFunction(); // Call to firstFunction
}

main(); // Call to main function
```

Explanation:

In this code snippet, we have three functions: `main`, `firstFunction`, and `secondFunction`. The `main` function is the entry point of our program.

1. The `main` function calls the `firstFunction` by invoking `firstFunction()`.

2. Inside `firstFunction`, there is a call to `secondFunction` by invoking `secondFunction()`.

3. Finally, `secondFunction` does its own operations.

The function calls occur sequentially, and each function call adds a new stack frame to the call stack. The call stack keeps track of the functions that are currently being executed.

The call stack would look like this:

    ```
       |                     |
       |    secondFunction   |
       |                     |
       |---------------------|
       |    firstFunction    |
       |---------------------|
       |        main         |
       -----------------------
    ```

When `secondFunction` completes its execution, it is popped off from the call stack, and the control goes back to `firstFunction`. Similarly, when `firstFunction` completes, it is popped off from the call stack, and the control goes back to `main`. Finally, when `main` finishes executing, it is also popped off from the call stack, and the program ends.

This example demonstrates how function calls are added to the call stack and executed in a Last-In, First-Out (LIFO) order.

## JavaScript error messages

Sure! Here are the answers to your questions along with code snippets:

1. What is a 'reference error'?

    A 'ReferenceError' occurs when you try to use a variable that is not declared or is not within the scope. It indicates that the interpreter cannot find a reference to the variable.

    ```
    console.log(nonExistentVariable); // ReferenceError: nonExistentVariable is not defined
    ```

2. What is a 'syntax error'?

    A 'SyntaxError' occurs when you have a mistake in the syntax of your code. It means that the code is not valid according to the language grammar rules.


    ```
    console.log('Hello, World!; // SyntaxError: Unexpected token ';'
    ```

3. What is a 'range error'?

    A 'RangeError' occurs when you try to manipulate a numeric value that is outside the valid range. It usually happens with functions like `Number.toFixed()` or `Array.length`.

    ```
    const array = [1, 2, 3];
    array.length = -1; // RangeError: Invalid array length
    ```

4. What is a 'type error'?

    A 'TypeError' occurs when you perform an operation on a value of the wrong type. It indicates that the value's type is incompatible with the operation being performed.

    ```
    const number = 42;
    number.toUpperCase(); // TypeError: number.toUpperCase is not a function
    ```

5. What is a 'breakpoint'?

    A 'breakpoint' is a debugging feature that allows you to pause the execution of your code at a specific line or condition. It helps you inspect the program's state and variables at that point in order to understand and debug issues.

6. What does the word 'debugger' do in your code?

    The 'debugger' keyword is a built-in JavaScript statement that triggers a breakpoint in your code. When the debugger encounters the 'debugger' statement, it will pause the execution at that line, allowing you to step through the code and inspect variables and values.

    ```
    function calculateSum(a, b) {
      debugger; // Pause execution here
      return a + b;
    }

    const result = calculateSum(2, 3);
    console.log(result);
    ```

#### Debugger

When you run the code with the 'debugger' statement, it will pause at that line, and you can use your browser's developer tools or a dedicated IDE to step through the code and analyze the program's state.