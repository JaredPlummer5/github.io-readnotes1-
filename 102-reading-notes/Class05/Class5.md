# Class 5 

## What is CSS?

CSS(Cascading Style Sheet) is baically the part that make the website look pretty.

CSS is a rule-based language — you define the rules by specifying groups of styles that should be applied to particular elements or groups of elements on your web page.

For example, you can decide to have the main heading on your page to be shown as large red text. The following code shows a very simple CSS rule that would achieve the styling described above:

`h1 {`
  
 `color: red;`
 
 `font-size: 5em;`

`}`

n the above example, the CSS rule opens with a selector. This selects the HTML element that we are going to style. In this case, we are styling level one headings `(<h1>)`.


CSS properties have different allowable values, depending on which property is being specified. In our example, we have the color property, which can take various color. We also have the font-size property. This property can change the size of letters/text.

A **CSS property** is a characteristic (like color) whose associated value defines one aspect of how the browser should display the element.

`h1 {`
  
  `color: red;`
 
  `font-size: 5em;`

`}`

`p {`
  
  `color: black;`
  
`}`

More Properties and How to code them below:

## [Click here to learn how to code certain properties in CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)

By click on Modules you will be able to see organized sub titles that let you click on specfic properties.

## How to add CSS

Three Ways to Insert CSS
There are three ways of inserting a style sheet:

## External CSS

- `External CSS` - With an external style sheet, you can change the look of an entire website by changing just one file

An external style sheet can be written in any text editor, and must be saved with a .css extension.

The external .css file should not contain any HTML tags.

Here is how the "mystyle.css" file looks:

`<!DOCTYPE html>`

`<html>`

`<head>`

- `<link rel="stylesheet" href="mystyle.css">`

`</head>`

`<body>`

`<h1>This is a heading</h1>`

    <p>This is a paragraph.</p>

`</body>`

`</html>`

The code below is the specific code to type the `<head>`.

`<link rel="stylesheet" href="mystyle.css">`

## Internal CSS

- `Internal CSS` - Inline CSS(avoid this method) - An internal style sheet may be used if one single HTML page has a unique style.

The internal style is defined inside the `<style> element`, inside the head section.

`<!DOCTYPE html>`

`<html>`

`<head>`

- `<style>`

- `body {`

- `background-color: linen;`

- `}`

- `h1 {`

  - `color: maroon;`

  - `margin-left: 40px;`

- `}`

- `</style>`

`</head>`

`<body>`

`<h1>This is a heading</h1>`

`<p>This is a paragraph.</p>`

`</body>`

`</html>`

## Inline CSS

- `Inline CSS` (avoid this method) - An inline style may be used to apply a unique style for a single element.

To use inline styles, add the style attribute to the relevant element. The style attribute can contain any CSS property.

`<!DOCTYPE html>`

`<html>`

`<body>`

`<h1 style="color:blue;text-align:center;">This is a`
`heading`

`</h1>`

`<p style="color:red;">This is a paragraph.</p>`

`</body>`

`</html>`

## Order

All the styles in a page will "cascade" into a new "virtual" style sheet by the following rules, where number one has the highest priority:

-Inline style (inside an HTML element)

-External and internal style sheets (in the head section)

-Browser default

So, an inline style has the highest priority, and will override external and internal styles and browser defaults.

## CSS Color

 In CSS every color has a number. And CSS has various method for protary that color. There many way to code color in CSS listed below:

- `body {color: hashtag92a8d1}(easier)`

  The code after the hashtag is called a Hex Code

- body {color: rgb round bracket 201, 76, 76 close bracket;}

- `body {color: rgba round bracket 201, 76, 76,  0.6 close bracket;}`

- `body {color: hsl round bracket 89, 43%, 51% close bracket;}`

- `body {color: hsla round bracket 89, 43%, 51%,  0.6 close bracket;}`

## Basic sytax rules

- CSS will change things according to which part of HTML. Along with the areas for the webpage when you `right click` on the webpage and hit `inspect`. So if you wanted to change the body or any other part, you would type something similar to the examples below.

`body {
    text-align: center;
   background-color: rgba(184, 76, 0, 72) ;
}
`

`header {
    border: 20px solid #BEC1C2;
}`

- Every line except  brackets that look like this ,`{}`, must end with a semicolon `;`.

- If you would like to target a specific section you have to type class = a variable in HTML. For example

`<section class="mid-section">`

   ` what ever is in the section

   `</section>`

This variable can be used for more than one section. Then in CSS type:

`.mid-section img {`
    
`color: rgba(185, 245, 250, 98);`

`border: 10px solid #FF9142;`

`}`

For targeting one section name the variable something different and replace the period with a hashtag. You would also have make a different variable each section you would like to target. For example:

`#other-mid-section img {`
    
`color: rgba(195, 200, 300, 50);`

`border: 10px solid #FF9142;`

`}`

`#other-mid-section-2 img {`

`color: rgba(195, 200, 300, 50);`

`border: 10px solid #FF9142;`

`}`

## Summary:

`.` = targets a class you made up

`#` = targets one varible youy made up

## Things I want to learn:

- Making a website look professional

- Animations

[Back to home page](../../README.md)