# Controlled Components

This statement is explaining the difference in how form elements are handled in HTML versus React. In HTML, form elements like text `input boxes`, `text areas`, and `dropdown menus` can store and update their own data based on user input.

However, in React, the practice is to keep track of any mutable state data for these form elements within the component's state property. Rather than directly updating the state, React uses the `setState()` method to modify and update the component's state.

This helps to keep the state and the UI in sync, allowing for more efficient and controlled updates to the user interface.

## What is a Controlled Component?

In React, a controlled component is a form element that has its value and state controlled by React instead of the DOM. This means that the value of the form element is not determined by the browser's DOM, but rather is set and managed by the component's state within the React component hierarchy.

To create a controlled component, you need to define a state variable within your component and set the value of the form element to the value of the state variable. Then, you need to define an event handler function that updates the state variable whenever the form element is modified. This way, the state of the component is always in sync with the value of the form element.

Controlled components are useful for several reasons. Firstly, they provide a single source of truth for the value of the form element, which can help prevent bugs and inconsistencies in your application. Secondly, they make it easier to validate and manipulate user input before submitting it to a server or storing it in your application's state. Finally, they provide a straightforward way to implement features like input masking, auto-completion, and other custom behavior that is difficult to achieve with uncontrolled form elements.

## Should we wait to store the users responses from the form into state when they submit the form OR should we update the state with their responses as soon as they enter them? Why

It's generally better to update the state with the user's responses as soon as they enter them, rather than waiting until they submit the form. This is because it provides a better user experience and makes it easier to handle form validation and error messages.

When you update the state with the user's responses as they enter them, you can immediately start validating the data and providing feedback to the user if there are any errors or issues with their input. This can help prevent the user from submitting invalid or incomplete data, which can save time and reduce frustration.

Additionally, updating the state as the user enters data allows you to implement features like auto-save and auto-complete, which can provide a smoother and more seamless user experience. For example, if the user enters their email address and then navigates away from the page, you can automatically save their progress and pre-fill their email address when they return.

Overall, updating the state with the user's responses as soon as they enter them is a better approach because it provides immediate feedback to the user, allows for more efficient form validation, and can improve the user experience by providing features like auto-save and auto-complete.

Example:

Suppose you have a simple form with two input fields, one for the user's name and another for their email address. You want to update the state with the user's responses as they enter them.

First, you would define a state variable in your component to store the user's responses:

```

import React, { useState } from 'react';

function MyForm() {
  const [formData, setFormData] = useState({
    name: '',
    email: ''
  });

  const handleInputChange = (event) => {
    const { name, value } = event.target;
    setFormData({
      ...formData,
      [name]: value
    });
  }

  const handleSubmit = (event) => {
    event.preventDefault();
    // Handle form submission
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="name">Name:</label>
      <input type="text" id="name" name="name" value={formData.name} onChange={handleInputChange} />

      <label htmlFor="email">Email:</label>
      <input type="email" id="email" name="email" value={formData.email} onChange={handleInputChange} />

      <button type="submit">Submit</button>
    </form>
  );
}

```
Here, we define a formData state variable using the useState hook, with name and email properties initially set to empty strings. We also define an handleInputChange function that updates the formData state as the user enters data into the input fields. We pass this function to the onChange event of each input field.

Finally, we define an handleSubmit function that is called when the form is submitted. In this example, we're just preventing the default form submission behavior, but you would typically handle the form data submission to your server or API.

By updating the state with the user's responses as they enter them, we can perform form validation and error handling in real-time. For example, we could display an error message if the user enters an invalid email address or if the name field is left blank. Additionally, we could use the formData state to pre-fill the input fields if the user navigates away from the page and returns later.

## How do we target what the user is entering if we have an event handler on an input field?

To target what the user is entering in an input field with an event handler, you can use the event object that is passed to the event handler function.

For example, if you want to target the text that the user types into an input field with an oninput event handler, you can access the value of the input field using the value property of the input element, which is stored in the target property of the event object. Here's an example:

```

<input type="text" oninput="handleInput(event)"> 

function handleInput(event) {
  const userInput = event.target.value;
  // do something with the userInput
}

```

In this example, the handleInput function is called whenever the user types into the input field. The event object is passed to the function as a parameter, and the userInput variable is set to the current value of the input field.

You can then use the userInput variable to manipulate the input data or perform some action based on the user input.

## Ternary Operator

A ternary operator is a shorthand way of writing an if...else statement in JavaScript. It allows you to write a single line of code that evaluates a condition and returns one of two values, depending on whether the condition is true or false. The syntax of a ternary operator is as follows:

```

condition ? valueIfTrue : valueIfFalse;

```

Here, condition is the condition that you want to evaluate, valueIfTrue is the value that is returned if the condition is true, and valueIfFalse is the value that is returned if the condition is false.

Here are some reasons why you might want to use a ternary operator:

Conciseness: Ternary operators are more concise than if...else statements, especially for simple conditions. This can make your code more readable and easier to understand.

Clarity: Ternary operators can make your code more clear and concise, especially when you're working with boolean values. They can help you avoid unnecessary if...else statements and reduce the overall complexity of your code.

Code Optimization: Ternary operators can be optimized more easily by the JavaScript engine than if...else statements. This means that using ternary operators can improve the performance of your code.

Functional programming: Ternary operators are often used in functional programming to create more concise and expressive code. They can be used in combination with other functional programming techniques, such as mapping and filtering arrays, to write more elegant and powerful code.

Overall, the ternary operator is a useful tool for writing concise, readable, and optimized code. However, it's important to use it judiciously and not to sacrifice clarity or readability for the sake of brevity.

## Ternary Vs If...Else

```

if(x===y){
  console.log(true);
} else {
  console.log(false);
}

```

```

x === y ? true : false

```

### Here’s what you need to know:

The condition is what you’re actually testing. The result of your condition should be true or false or at least coerce to either boolean value.
A ? separates our conditional from our true value. Anything between the ? and the : is what is executed if the condition evaluates to true.
Finally a : colon. If your condition evaluates to false, any code after the colon is executed.

In this case, the ternary operator evaluates the condition x === y. If this condition is true, the value true is returned. Otherwise, the value false is returned. This value is then passed to the console.log() function to output the result.

