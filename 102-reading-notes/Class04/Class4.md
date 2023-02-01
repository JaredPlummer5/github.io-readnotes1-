# Class 4

## HTML

## Wireframing

Wireframing is a rough draft of what you want your website to look like. Wireframing is benefical because you get a visual of your website. You can pre-determine what code goes where before you even code anything. A good example of wireframing consist of everything you want on your website ranging from text to imgages you want to add.

## HTML Rules and Sytax

HTML is the code that is used to structure a web page and its content. HTML is a markup language that defines the structure of your content. HTML consists of a series of elements. The enclosing tags can make a word or image hyperling to somewhere else and do a little bit with the format of words or text. For example, if you wanted to say "I have finish my code fellow 102 classes." You would simply type the code below:

`<p>I have finish my code fellow 102 classes</p>`

Attibutes contain extra info about the elemeant that you don't want to appear in the actual content. Below, `class`, is the attribute name and editor note is the attirbute value. The `class` attribute allow you to give the element a non-unique identifier that can be used to target it (and  any other elements with the same `class` value) with style info and other thing

## Semantics

Semantics refers to the meaning of a piece of code — for example "what effect does running that line of JavaScript have?", or "what purpose or role does that HTML element have" (rather than "what does it look like?".)

In HTML, for example, the `<h1>` element is a semantic element, which gives the text it wraps around the role (or meaning) of "a top level heading on your page."

List of Semantics in HTML:

- `<article>`

- `<aside>`

- `<details>`

- <`figcaption>`

- `<figure>`

- `<footer>`

- `<header>`

- `<main>`

- `<mark>`

- `<nav>`

- `<section>`

- `<summary>`

- `<time>`

Some semantic element can be found in the link below:

[Semantics](https://developer.mozilla.org/en-US/docs/Glossary/Semantics)

## HTML Elements

To sumarize an element may contain a data item or a chunk of text or an image, or perhaps nothing. A typical element includes an opening tag with some attributes, enclosed text content, and a closing tag. There are a lot of HTML elements. All elements can be found in the link below:

[HTML_Elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

## Basic things You need to know

### Headings

`<h1>My main title</h1>`

`<h2>My top level heading</h2>`

`<h3>My subheading</h3>`

`<h4>My sub-subheading</h4>`

`<h5>My sub-sub-subheading</h5>`

`<h6>My sub-sub-sub-subheading</h6>`

Heading elements allow you to specify that certain parts of your content are headings — or subheadings.
HTML contains 6 heading levels, `<h1> - <h6>`

### Paragragh

As explained above, `<p>` elements are for containing paragraphs of text; you'll use these frequently when marking up regular text content:

`<p>This is a single paragraph</p>`

### List

Marking up lists always consists of at least 2 elements. The most common list types are ordered and unordered lists:

1. Unordered lists are for lists where the order of the items doesn't matter, such as a shopping list. These are wrapped in a `<ul>` element.

2. Ordered lists are for lists where the order of the items does matter, such as a recipe. These are wrapped in an `<ol>` element.

Each item inside the lists is put inside an `<li>` (list item) element.

`<p>At Mozilla, we're a global community of</p>`

`<ul>`

 `<li>technologists</li>`

 `<li>thinkers</li>`

 `<li>builders</li>`

`</ul>`

`<p>working together…</p>`

### Links

To add a link, we need to use a simple element — `<a> `— "a" being the short form for "anchor".

1. Choose some text. We chose the text "Mozilla Manifesto".

2. Wrap the text in an `<a>` element, as shown below:

`<a>Mozilla Manifesto</a>`

Copy to Clipboard

Give the `<a>` element an href attribute, as shown below:

`<a href="">Mozilla Manifesto</a>`

Copy to Clipboard

Fill in the value of this attribute with the web address that you want the link to:

`<a href="https://www.mozilla.org/en-US/about/manifesto/">Mozilla Manifesto</a>`




Copy to Clipboard

Thing I want to learn about:

- How to make a functioning website with HTML

[Back to home page](../../README.md)
