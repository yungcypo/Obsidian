# JavaScript

JavaScript (also known as JS, _has nothing to do with Java_) is a programming language used mainly in Web Development alongside HTML and CSS
JavaScript is a huge concept, only a bit of it will be discussed here  
Also check out [React](./React.md), which is a JavaScript library
Also check out [TypeScript](./TypeScript.md), which is a programming language that extends JavaScript

# Basic stuff

This is a basic Hello World program

```javascript
console.log("Hello World!");
```

The output will be written in console  
To open up console, hitting `F12` on your keyboard works on most browsers  
Hit `F12` to open Debug Menu and go to Console

There are 3 ways to output text to console:

```javascript
console.log("This is a normal message");
console.warn("This is a warning");
console.error("This is an error");
```

First, I will talk about the really basics of JavaScript, then I will move onto [how to use JavaScript with HTML](#JavaScript%20&%20HTML)

## Using JavaScript

Where should I write JavaScript code?  
There are 2 ways to use JavaScript: `<script>` tag or separate `.js` file

### `<script>` tag

See the prefferred location of `<script>` tag bellow

```html
<body>
  <h1>Header</h1>
  <p>*all the other content*</p>
  <script>
    /* JavaScript goes here */
  </script>
</body>
```

This way the browser renders all content before loading the script, so it's a lot faster

### `.js` file

Technically, this way you are also using the `<script>` tag, but inside of it, you are only telling the browser to use separate `.js` file

```html
<script src="app.js" />
```

It's preferred to use this method, because you can write the code in file once, and use it in many HTML files

> Note: See [the chapter before](#`<script>`%20tag) for proper location of `<script>` tag

# Primitive Datatypes

| Name        | Example                         |
| ----------- | ------------------------------- |
| `string`    | "Hello"<br>'This is JavaScript' |
| `number`    | 2<br>3.0<br>10000<br>-0.009     |
| `boolean`   | `true` or `false`               |
| `null`      |                                 |
| `undefined` |                                 |

# Variables

Variables are capable of storing any kind of datatype

```javascript
var age = 21;
console.log(age);
age = 22;
```

Rules for naming variables:

- Name can't have spaces
  - `var my age = 21;` will not work
  - You can use underscore (`_`) instead of whitespace: `var my_age = 21;`
- You can use only letters and digits
  - Special characters like `()` or `$` would not work
- You have to start the name of variable with letter
  - `var 5my_number = 12345;` will not work
  - You can use numbers in the name, just not at the beginning

You can set variable to have a value of another variable

```javascript
var name = "peto";
var something = "";
something = name;
```

# Operators

JavaScript has all the common operators as other languages, such as `=`, `+`, `-`, `*`, `/`, `%`, `+=`, `++`, `==`, `&&`, `||`,...

There is one operator in JavaScript that is not that common in other languages, its the `===` operator  
While `==` operator checks if two values are the same, `===` operator checks if the values are the same **and has the same type**

```javascript
var x = 10;
var y = "10";

console.log(x == y); // true
console.log(x === y); // false
```

We can see here, that the second statement is false, because `x` is a `number` but `y` is a `string`  
The same goes with `!=` and `!==`

# Comments

Single-line comment is made with `//`  
Everything in line after `//` will be considered as a comment

```javascript
console.log("Hello"); // this line will print hello to the console
```

Multi-line comments are made with `/*` and `*/`

```javascript
var x = 10;
/*
this
is 
an
example
of
multiline
comment
*/
console.log(x);
```

# Conditions

```javascript
var name1 = "peto";
var name2 = "Peto"; // uppercase P
var name3 = "peto";

console.log(name1 == name2); // false
console.log(name1 == name3); // true

console.log(name1 == name2 && name1 == name3); // false
console.log(name1 == name2 || name1 == name3); // true
```

Also, an example from [Operators section](#operators) is a good example

# Functions

```javascript
function add(a, b) {
  return a + b;
}

var x = add(3, 4);
var y = add(6, 9);

console.log(add(1, 2));
```

# `if`, `else`, `else if`

```javascript
if (5 > 10) {
  console.log("something isn't right");
} else if (5 == 10) {
  console.log("something is still not right");
} else {
  console.log("i knew it...");
}
```

# JavaScript & HTML

First of all, make sure you have imported your `.js` file  
If you don't know how, check [the chapter about `.js` file](#`.js`%20file)

## Click `<button>`

If you had a button like this...

```html
<button onclick="do_something()" />
```

...it will call the function `do_something()` from JavaScript file every time the button is clicked

```javascript
function do_something() {
  console.log("congratulations, you clicked on a button");
}
```

## Changing HTML with JavaScript

Although [React](React.md) might be better for this, here is an example on how to change the text of `<p>` with JavaScript  
You can also change style this way

Here, _ID's_ of HTML elements comes in handy, as stated in CSS tutorial

```html
<p id="text-paragraph">Some boring text</p>
<h2 id="random-header"></h2>
<button onclick="do_something()">Change the text</button>
```

```javascript
function do_something() {
  document.getElementById("text-paragraph").innerHTML =
    "Some really awesome text";
  document.getElementById("random-div").style.color = "red";
}
```

## Getting value of `<input>`

```javascript
var text = document.getElementById("paragraph").value;
console.log(text);
```
