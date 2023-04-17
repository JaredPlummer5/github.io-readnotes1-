# Introduction to React and Components

## What is a “component”?

A component is a modular and self-contained unit of software that encapsulates its own functionality and can be deployed and managed independently. A component has well-defined interfaces that specify its inputs and outputs, allowing it to be integrated with other components to create a complete system.

### Characteristics

- Encapsulation: Components encapsulate their functionality and do not expose their internal workings to other components.

- Modularity: Components are designed to be independent and self-contained, with well-defined inputs and outputs.

- Reusability: Components are designed to be reusable across multiple projects and systems, reducing development time and cost.

- Composability: Components can be combined and assembled in different configurations to create a complete system.

## Component-Based Architecture (CBA)

CBA is a software architecture pattern that emphasizes the decomposition of a system into reusable and interchangeable components.

CBA offers several advantages over other architecture patterns, including:

- Reusability: Components can be reused across multiple projects and systems, reducing development time and cost.

- Scalability: Components can be added or removed as needed to adjust the system's capacity and performance.

- Modularity: Components can be developed, tested, and deployed independently, allowing for faster and more efficient development.

- Interoperability: Components can be developed in different programming languages and run on different platforms, enabling better integration with other systems.

## Props

## What are props and what is “props” short for?

In React, you can create components that represent different parts of your user interface, like buttons, forms, or even entire pages. These components can be reused throughout your app to make it easier to build and maintain.

In React, "props" is a special keyword that stands for "properties". Props are used to pass data from one component to another in a unidirectional flow.

## How are props used in React?

In React, props are used to pass data from one component to another. Here are some of the ways props are used in React:

- `Passing data` from parent to child components: Props can be used to pass data from a parent component to a child component. The parent component can pass down any data it needs to the child component as props, and the child component can use that data to render its content or perform actions.

- `Configuring components`: Props can also be used to configure components with specific values or behavior. For example, a Button component may have a prop for the button text, so it can be easily configured with different text values.

- `Event handling`: Props can be used to pass down event handlers from parent to child components. For example, a parent component may pass down an onClick event handler to a child component to handle a button click event.

- `Conditional rendering`: Props can be used to conditionally render content in a component. For example, a parent component may pass down a boolean prop to a child component to control whether or not a certain element is rendered.

In general, props provide a flexible and powerful way to pass data and behavior down from parent components to child components in a React application.

## What is the flow of props?

Props are uni-directional which means they only flow one way.

The flow of props is as follows:

- A parent component creates a child component and passes data to it using props.

- The child component receives the props as an argument in its function or as a property in its class constructor.

- The child component can then use the props to render content or perform actions.

- If the props are updated in the parent component, the child component will receive the updated values and can re-render accordingly.

This one-way data flow ensures that the components remain modular and reusable, as they don't depend on each other's internal state.