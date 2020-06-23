# The Document Object Model (DOM)

## Learning Objectives (_students will be able to..._)

- Explain what the DOM is and how it is structured
- Target DOM elements using JavaScript selectors
- Create, read, update, and delete DOM elements
- Change the attributes or content of a DOM element
- Explore JavaScript methods for DOM manipulation and traversal

## Framing

Today, we will learn about how JavaScript uses objects to represent what you see in the browser. Remember, everything is an object!

The [Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction), commonly referred to as the "DOM", is a programming interface for HTML. When you load HTML into the browser, it gets converted into a dynamic object-based structure. The [visual representation](https://css-tricks.com/dom/) of this is what you see when you open up Developer Tools in the browser.

The DOM is available for us to manipulate as an object, and this object is structured and stored like an upside down tree.

![Element Tree](assets/LXF118.tut_grease.diagram.png)

or


```
html
└── head
│   ├──title
│   ├──meta
│   ├──link[rel="stylesheet"]
|   └──script[type="text/javascript"]
|
└── body
    ├── header
    │   ├── h1
    │   └── nav
    └── section.simplicity
    |   └── h2
    │   └── article
    ├── section.life
    |   └── h2
    │   └── article
    │       └── block_quote
    │       └── block_quote
    └── footer
```

## The Document Object

Each web page loaded in the browser has its own `document` object. The `document` interface serves as an entry point to the web page's content. The document is an example of a **host object**--that is, a JavaScript object provided by and unique to the browser environment.

## Nodes

Everything in the DOM exists as a **node**. HTML elements are called **element nodes**, attributes are called **attribute nodes**, the text inside elements are called **text nodes**. There are even comment nodes for `<!-- html comments like this one --->`. The document itself is called a document node.

You also can refer to nodes by their relationships to each other. For example, in the graphic above, you would say that the body element is the "parent" to the two `div` elements contained inside it, which are called child nodes. The two divs are also "siblings" to one another because they are on the same level in the tree structure.

![DOM Tree Relationships](assets/helloworldtree.jpg)

## Basics of Working with the DOM

Understanding the DOM is central to working in JavaScript. JavaScript uses the DOM to create dynamic HTML. This includes adding new HTML elements and attributes, changing CSS styles in a page, removing existing elements and attributes, and [many more things](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model).

Most of what you do with client-side javascript is going to revolve around manipulating the DOM.

## Getting Data from the DOM

There are two groups of methods you can use to get elements from the DOM. We'll start with the oldest and end with the ones we recommend.

### `getElement(s)By`

Each of these methods follows the same general naming convention:

| Method Name | Description |
| --- | --- |
| `.getElementById()` | Gets a single element by an ID selector |
| `.getElementsByClassName()` | Gets a list of elements with a class selector |
| `.getElementsByTagName()` | Gets a list of elements with a tag (element) selector |

Each of these three methods are part of the `document` object. We'll walk through each individually:

##### `getElementById()`

To use the `getElementById` method, we first need to reference the `document` object (where the method lives). Then, we pass in a string that matches the ID of an element in our HTML

```js
let titleElement = document.getElementById('title')
```

The above code will start at the document (top of the tree), and look for an element with an id called `title` and save it in the variable `titleElement`

##### `getElementsByClassName`

The `getElementById` method returns a single Node item; the `getElementsByClassName` returns a NodeList, which is like an Array of Nodes.

```js
let paragraphElements = document.getElementsByClassName('paragraph')
```

The above code snippet returns a NodeList (like an Array) of every element with a class of 'paragraph' and saves it to the `paragraphElements` variable. Notice that `Elements` in the method name is plural here, where as in `getElementById` it's singular? This is to tell us that `getElementByID` only returns one Node while `getElementsByClassName` returns a list of Nodes.


##### `getElementsByTagName`

The `getElementsByTagName` is a hand way of retrieving elements by their html tag (`h1`, `span`, `a`, `li`, etc). `Elements` is plural in the method name, meaning it too returns a list of Nodes.

```js
let spanElements = document.getElementsByTagName('span')
```

The above snippet returns every `span` element on the page and saves it to the `spanElements` variable.

### Independent Practice: [JS DOM Practice Part 1](https://git.generalassemb.ly/sei-nyc-bees/js-dom-practice)

Clone down and open the practice exercise and work through the prompts in the `getelements.js` file.

### Query Selector

There are only two methods in this group: `querySelector` and `querySelectorAll`. Unlike the `getElement(s)By` group, these are simpler to understand - querySelector returns a single value, and querySelectorAll returns...well...everything that it can find. You can even select multiple IDs this way.

We'll walk through both `querySelector` and `querySelectorAll`, but first a note about selectors:

Unlike with the `getElement(s)By` family of methods, we need to pass a complete selector to both `querySelector` and `querySelectorAll` - it's in the name! What's a selector? A selector is a way of targeting a particular element, something we learned about when we first covered CSS.

The following is a list of CSS selectors and the JavaScript equivalents you would use with `querySelector`:

| CSS Selector | JS Selector |
| --- | --- |
| `.class-name` | `.class-name` |
| `#some-id` | `#some-id` |
| `h1` | `h1` |

They're the same! Phew, that's lucky!

The `querySelector` methods were designed to mimic the way we target elements in CSS, so the selector we pass in is the same we'd use to style that element!

**`querySelector`**

With `querySelector`, we'll pass in a selector for the element we want to retrieve from the DOM. The element that we get back will be the first element that matches that selector.

```js
let title = document.querySelector('.title')
```

We'll only get one element back and it will always be the first element that matches the selector (in this case, `.title`). If we have more than one element in the page with that selector and we want to retrieve them all, then we'd use `querySelectorAll`

**`querySelectorAll`**

With `querySelectorAll`, we'll get back all elements on the page that match the selector we pass in.

```js
let title = document.querySelectorAll('h2')
```

The above code snippet would return a list of all `h2` elements on the page.

### You Do: [JS DOM Practice Part 2](https://git.generalassemb.ly/sei-nyc-bees/js-dom-practice)

Open up the practice exercise and work through the prompts in the `queryselector.js` file.

## Break

## Setting Data in the DOM

Now that we know how to get elements from the DOM, it'd probably be helpful to learn what we can do with them. We'll soon learn about adding event listeners to DOM elements - a way for us to listen for when some event happens to a node (like it gets clicked) and then perform some response. But there are many other things we can do with nodes! Toggle, add or remove classes, change their styling, animate them, move them from one part of the page to another, replace their content with new content, etc. The list goes on!

### Exploring DOM Nodes
> 10 minutes to do personal research, next spend 8 minutes to come up with a demo and explaination as a group. Then 25 minutes to present (5 minutes per group)

We're going to count off and break up in to 5 groups. Each group will be responsible for one of the topic areas below. Your goal is to research this topic area as a group and come up with a demo of how you would use it and why it might be helpful or important. We'll then go around the room and demo what we find! 

**1. Getting and Setting Attributes**

Remember from our HTML lesson that some elements have attributes: the `a` tag has an `href` attribute and the `img` tag has a `src` attribute. In JavaScript, there are ways to access the list of attributes on a node and to get and set attributes.

Every node object has an `attributes` property where it lists it's attributes (like `href` and `src`). You can get and set data using the `getAttribute` and `setAttribute` method.

Look at the `attributes` property of a node. Also look up the `getAttribute` and `setAttribute` methods and how they work. Prepare a demo to showcase these. Your demo should show the following:

- How do we access the list of attributes on a node?
- How to we get the value of a particular attribute (like the `href` attribute)?
- How do we add an attribute (like the `name` attribute)?

**2. Class list API**

A very common task in JavaScript is toggling CSS classes. We'll remove a `.is-hidden` class when the user clicks on something or we'll add an `is-active` class to a navigation element when someone clicks on a hamburger menu.

The way we get and set classes on nodes is with the `classList` API. Every node has a `classList` property and there are methods we can use to add  a class (`add`), remove a class (`remove`) or toggle a class (`toggle`).

Research these methods and think about how they work and why they're useful. Prepare a demo to showcase the following:

- How can we see the list of classes a node has?
- How can we check to see if a node has a class?
- How can we add a class to a node?
- How can we remove a class from a node?
- How can we toggle a class from a node?

**3. Traversing Nodes**

We'll often have a particular node but need to check it's parents, children or siblings. Luckily, each node has this information stored within it!

Look through a node object and see if you can find the following:

- `children` / `childNodes`
- `firstChild` / `firstElementChild`
- `lastChild` / `lastElementChild`
- `nextSibling` / `nextElementSibling` and `previousSibling` / `previousElementSibling`
- `parentNode`

What are these properties? What is the difference between children and child Nodes? What kinds of nodes do you see stored in these properties?

Think about these questions and explore the above list of properties. Prepare a demo to showcase how to access these and what the different options tell you.

**4. Content**

We'll sometimes have an element and want to change the text or html contained within that element. This is commonly called *templating* and there are libraries that will make it a little easier. With the new template literal syntax in ES6, we can often get away without a templating library. We could just use the list of properties below to reset the html or text of an element and interpolate data in to it.

Review these properties of a node:

- `innerHTML` / `outerHTML`
- `innerText` / `outerText`
- `textContent`

What are they? How are they similar? How are they different?

Create a demo to showcase how you might use these and why they might be useful. Can we change the html inside of an element?

**5. Changing the Styling**

Something we may want to perform in JavaScript is updating or changing the styling of an element using JavaScript. A lot of web animation tools do that and there are tools for React (which we'll learn about later) that do this so you can write all your styles in JavaScript.

Explore the `style` property of a node. What do you see in there? How could we see the style of an element like, is it `display: block`? Can we change these style properties, like setting the background color?

### Bonus Lab

Complete the following in-class exercises:

 - [DOM Quotes](https://git.generalassemb.ly/sei-nyc-constellations/js-dom-quotes-lab) exercise.
 
## Reference
- [MDN DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction#Interfaces_and_Objects)
- [Eloquent JS: The Document Object Model](http://eloquentjavascript.net/13_dom.html)
- [What, exactly, is the DOM?](https://bitsofco.de/what-exactly-is-the-dom/)
- [Nodelist vs Htmlcollection vs Arrays?](https://hackernoon.com/htmlcollection-nodelist-and-array-of-objects-da42737181f9)

