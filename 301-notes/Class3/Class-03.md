# Passing Functions as Props

## What does .map() return?

`.map()` is a built-in method in JavaScript that can be used to iterate over an array and perform an operation on each element of the array. It returns a new array that is the result of applying the operation to each element of the original array. For example, if we have an array of numbers [1, 2, 3], we can use `.map()` to create a new array with each number multiplied by 2: [2, 4, 6]. The `.map()` method is commonly used in React to create lists of elements based on data in an array.

If I want to loop through an array and display each value in JSX, how do I do that in React?
To loop through an array and display each value in JSX, we can use the `.map()` method in combination with JSX. Here's an example:

![Mapping Example](mapping.png)

In this example, we have an array of numbers and we want to display each number in an unordered list using JSX. We use the .map() method to create a new array of `<li>` elements, with each element containing a number from the original array. We then include the numberList array inside the `<ul>` element to display the list on the page.

## Each list item needs a unique __key__.

Each list item needs a unique "key". When we create a list of elements in React, we need to include a "key" prop on each element. This helps React keep track of which items have been added, removed, or modified in the list. The "key" should be a unique identifier for each item in the list, such as an ID or a unique value from the data. For example:

![Key Example](key.png)

In this example, we have an array of items with each item containing an id and a name. We create a list of `<li>` elements using .map(), and we include a key prop on each element with the id of the item. This ensures that each item in the list has a unique identifier that React can use to manage the list efficiently.

## What is the purpose of a key?

The purpose of a __"key"__ in React is to help the library keep track of which items have been added, removed, or modified in a list of elements. When we create a list of elements in React, we need to include a __"key"__ prop on each element. This key should be a unique identifier for each item in the list, such as an ID or a unique value from the data. React uses the key to identify which elements in the list have changed, and it updates the UI accordingly. Without a __key__, React would have to rerender the entire list every time a change occurs, which can be slow and inefficient. By using keys, React can update only the necessary parts of the list, resulting in a faster and more efficient UI.

