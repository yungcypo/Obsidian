# HTML
Hyper-Text Markdown Language  
Used for creating websites  
> Note: HTML is not an programming language

# Basic stuff
First file - `index.html`  
Browser will think that this is our homepage  

```html
<!DOCTYPE html>
```
Lies at the beginning of a file  
Defines the document type of file  
This is gonna be HTML document

HTML document is made of so-called **"tags"**  
- Starting tag: `<html>`
- Ending tag: `</html>`
Together they are paired tags  

## `<html>` 
`<html>` is the main tag of whole file, like overall container, highest level tag  
It contains all the data  

```html
<!DOCTYPE html>
<html>
	There goes anything else...
</html>
```

Inside `<html>` you need to create 2 more tags: `<head>` and `<body>`

## `<head>`
Lies inside `<html>` tag  
Defines data of document, settings, information and more  
### `<head>` tags
These tags are located inside `<head>` tag  
- `<meta charset="UTF-8">`
	- Tells browser, what characters are we using
	- `UTF-8` is like a basic set of characters  
- `<meta name="description" content="The best website in whole world">`
	- Gives a description on website 
	- Inside of this `meta` tag, you are telling what type of information/setting you want to define *(description)* and you are telling what the description should be *(The best website in whole world)*
- `<meta name="author" content="Cypo">`
	- Gives information about the author  
- `<meta name="keywords" content="Programming, HTML, Tutorial">`
	- Provides keywords to search engine
- `<meta name=viewport content="widt=device-width, initial-scale=1.0">`
	- This is gonna control how your website is gonna be displayed
	- Without this, you will see the website the same on Mobile as on PC
- `<title>Cypo's Website</title>`
	- Text inside `<title>` tag is shown in browser on current tab
- There are a lot more tags that you can provide to `<head>`

## `<body>`
Lies inside `<html>` tag
Makes all the actual content of page  

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<meta name="description" content="The best website in whole world">
		More settings here...
	</head>
	<body>
		Content...
	</body>
</html>
```

#### Relations
- `<html>` is parent of `<head>` and `<body>`, because it wraps them  
- `<head>` and `<body>` are children of `<html>`, because they lie inside it  
- `<head>` and `<body>` are siblings, because they lie next to each other  

# Basic tags
These tags are placed inside `<body>` tag  

## `<h1>`
Header 1 tag  
There are multiple Header tags: `<h1>`, `<h2>`, `<h3>`,... `<h6>`   
`<h1>` is the biggest, `<h2>` is bit smaller and so on, `<h6>` is the smallest of all  

### Quick tip on headers
In webpage you should have only one `<h1>` tag that will be like a header of your webpage  
You can put `<h2>`'s under it, to define different sections   
Under it you can put`<h3>` and so on...  
It's not required, but it's a good practice and a lot of people is gonna use it this way  

## `<p>`
Paragraph tag  
Holds text  

## `<b>`
Paragraph for bold text  
Can be put inside `<p>` tag  

If we had tags like this...
```html
<p>This is my <b>bold text</b></p>
```
...it might look something like this: This is my **bold text**  

## `<i>`
Very similar to `<b>`, but makes text italic

| `<p>`     | `<b>`       | `<i>`     |
| --------- | ----------- | --------- |
| Paragraph | Bold        | Italic    |
| Preview   | **Preview** | *Preview* |


You can combine `<b>` and `<i>` tags  
If we had tags like this...
```html
<p>This is my <b><i>bold italic text</i></b></p>
```
...it might look something like this: This is my ***bold italic text***  

---
##### Notes
All tags will be shown in order as we write it  
If we had two [*sibling*](#Relations) tags like this...
```html
<h1>Welcome back!</h1>
<p>Take a look at my page</p>
```
...you will see the `<h1>` at the top and `<p>` bellow it   


Tags have to be closed in the *exact opposite order* as they were open  
If we had tags like this...
```html
<h1>
	<h2><p></h2></p>
</h1>
```
...it will fail to render, because the closing tags are not in the right order  

The order of opening is like this:
1. `<h1>`
2. `<h2>`
3. `<p>`
...so it has to be closed like this:
1. `<p>`
2. `<h2>`
3. `<h1>`

---

## `<big>` and `<small>`
It's pretty obvious,  `<big>` makes the text bigger and `<small>` makes the text smaller  
```html
<p>This is example of <big>big text</big> and <small>small text</small></p>
```

## `<sub>` and `<sup>`
Subscript and Superscript tags  

For example this...
```html
<p>H<sub>2</sub>O</p>
<p>Somehing on <sup>top</sup></p>
```
...will be formatted as "H<sub>2</sub>O" and "Somehing on <sup>top</sup>"

# Single tags
Following tags are called Single, or self-closing tags  
They don't need any content inside of them, so you can "close" them right at the moment when you are creating them  
Single tag can look like this: `<br/>`
In theory, you can make it like this: `<br></br>`, but it's too much typing for nothing  
In theory, you can make any tag self-closing, but it doesn't make any sense... For example `<p/>` is a paragraph tag with nothing inside, therefore it's useless

## `<br/>`
Break tag  
Adds whitespace to your page  
If you try to hit `enter` on your keyboard to create whitespace, it will be ignored  

## `<hr/>`
Horizontal rule tag  
Draws a straight like across our webpage  
It's gonna help us separate content  

# Comments
Comments are small pieces of code, that are going to be ignored while rendering by HTML and your Browser  
Their main purpose is to leave a note for you or another programmers, who are reading your code  
They will not be visible on your webpage 
`<!-- comment -->`

```html
<!--
	Right here i can leave note for future me  
	I can type there anything I want, and it will not be displayed on page  
-->
```

# Style
Style is used to make your page **look** different  
You can apply style to all elements  
Styles is usually written in another file using CSS  
CSS is whole another subject and will be discussed in different file  
You can use style inside HTML file, but it's usually not a good practice to put a lot of styles in HTML

For example this... 
```html
<p style="color: green">Some green text</p>
<p style="color: yellow; background-color: brown">Some more text</p>
```
...will look like this: <span style="color: green">Some green text</span>; and this: <span style="color: yellow; background-color: brown">Some more text</span> 

> Note: this might not render correctly inside `.md` file, but in HTML the text will be green *(1st example)* and yellow text with brown background *(2nd example)* 

You can style all other element, like headers, `<b>` tags, body and so on  
If you put `style` on body, all of its children will have the style applied  

Children overwrites the style of it's parent (see [relations](#Relations))  
So, for example, if we had this...  
```html
<!DOCTYPE html>
<html>
	<head>...</head>
	<body style="color: green">
		<p style="color: red">Hello there!</p>
	</body>
</html>

```
...the text inside `<p>` tag will be **red**

#### Something about colors
You can see all the available colors on [this website](https://www.w3schools.com/colors/colors_names.asp)  
If you want more precise colors, you can also use *Hex* or *RGB* values

| Color name | Hex color code | RGB color code   |
| ---------- | -------------- | ---------------- |
| Red        | `#ff0000`      | `rgb(255, 0, 0)` |
| Green      | `#00ff00`      | `rgb(0, 255, 0)` |
| Blue       | `#0000ff`      | `rgb(0, 0, 255)` |

So the style could look something like this:  
```html
<p style="color: red">Hello</p>
<p style="color: #ff0000">Hello</p>
<p style="color: rgb(255, 0, 0)">Hello</p>
```
All of these tags will make the exact same text  

> Note: A bit more on colors in CSS tutorial (separate file)

# Links  
You can specify a link with `<a>` tag  
`<a>` tag has a property `href=""`, where you specify where you want to link to  
You can specify `target="_blank"` to make it open on new tab  

```html
<a href="https://www.google.com" target="_blank">Open Google</a>
```

You can always combine tags  
```html
<a href="https://cyprich.github.io">Click here to open <b>the coolest site ever</b></a>
```
Just remember to close them properly, as stated in [notes](#Notes) after `<i>` tag

# Audio-visual stuff
## `<image>`
You can insert images to your website with `<img>` tag  
Image can be used as a [single tag](#Single%20tags)  

```html
<img width="" height="" src="" alt=""/>
```
- `width` and `height`
	- Provides dimensions of the image
- `src`
	- Provides path to the actual images
	- It can be
		- Local file - stored alongside HTML file
		- Link to file - image from another website
- `alt`
	- Alternative
	- You can provide a text that will be shown in case the image is not accessible  

You can combine images with links like this: 
```html
<a href="userprofile.html">
	<img width="200" src="profilepicture.jpg"/>
</a>
```
Now, if you click on the Profile Picture, it will take you to User Profile page  

## `<video>`
Similar to images, but *(you guessed it)* shows a video  
```html
<video src=""/>
```

You can add more stuff to the video
```html
<video width="" src="" poster="thumbnail.jpg" controls autoplay muted loop/>
```

## `<audio>`

```html
<audio controls>
    <source src="audio/meow.mp3" type="audio/mpeg">
    <source src="audio/meow.ogg" type="audio/ogg">
</audio>
```

## iFrames
With iFrame, you can add for example a video from YouTube to you webpage  
iFrame is like a part of different website on your webpage
Its just a piece of code that you just paste into your webpage  
Some popular sites makes you able to use their iFrame  

1. Find a video on YouTube
2. Click share -> Embed -> Copy shown code
3. Paste copied code into your HTML file

Now you have a YouTube video on your webpage  
You can edit the `width` and `height` as needed  
There might be similar steps for Spotify iFrames and whatever you can imagine



# Lists
There are 3 types of lists: [Unordered lists](#Unordered%20lists), [Ordered lists](#Ordered%20lists) and [Description lists](#Description%20lists)
## Unordered lists
Lists, where the order of items doesn't matter  
There is a dot before every item  
```html
<p>List of fruits</p>
<ul>
	<li>Apples</li>
	<li>Bananas</li>
	<li>Oranges</li>
</ul>
```
## Ordered lists
Lists, where the order of items does matter  
There is a number before every number  
```html
<p>How to put giraffe into a fridge</p>
<ol>
	<li>Open the fridge</li>
	<li>Take out the elephant</li>
	<li>Put a giraffe there</li>
	<li>Close the fridge</li>
</ol>
```

You can specify the type of Ordered list

| Code            | Style                  |
| --------------- | ---------------------- |
| `<ol type="1">` | `1. 2. 3.` *(default)* |
| `<ol type="A">` | `A. B. C.`             |
| `<ol type="a">` | `a. b. c.`             |
| `<ol type="I">` | `I. II. III.`          |
| `<ol type="i">` | `i. ii. iii.`          |

## Description lists
Lists, where you want to provide description to items  
```html
<p>Shopping list</p>
<dl>
    <dt>Apples</dt>
    <dd>They are red</dd>
    <dt>Bananas</dt>
    <dd>They are yellow</dd>
</dl>
```
`<dl>` - description list
`<dt>` - description term
`<dd>` - describe description term  

> Note: remember that you can combine tags, lists included  
> 	Inside `<li>` you can put `<h1>`, `<img>`, another list or anything you want

# Tables
## Default tags
There are some default tags to make a table   
```html
<table>
	<tr>
		<td></td>
	</tr>
</table>
```

| Tag       | Meaning    | Descitption                       |
| --------- | ---------- | --------------------------------- |
| `<table>` | -          | Stores content of the whole table |
| `<tr>`    | Table Row  | Individual rows of the table      |
| `<td>`    | Table Data | Individual columns of the table   |
## Additional tags
There are also some additional tags  
These are not required to use, but it can be a good practice  

| Tag         | Meaning    | Description                                            |
| ----------- | ---------- | ------------------------------------------------------ |
| `<caption>` | -          | Provides caption/description to the table              |
| `<thead>`   | Table Head | Like the first row of table, text inside is bold *(?)* |
| `<tbody>`   | Table Body | Everything other that `<thead>`                        |
| `<th>`      | ?          | Similar to `<td>`, but text inside is bold             |

## `rowspan` and `colspan`
These can be used on `<td>`  
Makes `<td>` take up more cells than it would normally  

`<td colspan="2">` would make a cell take up 2 spaces horizontally   
`<td rowspan="2">` would make a cell take up 2 spaces vertically  

You can also combine these two and make a cell take up as much space as you want by doing something like `<td colspan="3" rowspan="6">`

# `<span>` and `<div>`
These two tags are called "containers"  
Is basically an empty box, in which you can put other elements  
You can't see them on your page *(unless they are styled)*  
When using CSS, you can apply some style to container to apply something to all it's children  

**The difference** between `<span>` and `<div>` is only that `<span>` takes as *less* horizontal space as possible, while `<div>` takes as *much* horizontal space as possible *(unless they are styled)*  
In terms of vertical space, they both take as less vertical space as possible *(unless they are styled)*  

|                  | `<span>`            | `<div>`             |
| ---------------- | ------------------- | ------------------- |
| Horizontal space | As less as possible | As much as possible |
| Vertical space   | As less as possible | As less as possible |
|                  | Inline element      | Block element       |

# User Input and forms  
To actually get and use user input, you will have to learn JavaScript, which is another giant subject  
For now, it's enought to understand the HTML part of it - "defining" things like input boxes and text areas  

## `<input>`
There are a lot of different types of input, as you can see in the table bellow  
The `<input>` tag is a [single tag](#Single%20tags)  

```html
<input type="text"/>
```

| `<input>` type | Desctiption                                                                                |
| -------------- | ------------------------------------------------------------------------------------------ |
| `text`         | Provides you a text box which you can type into                                            |
| `password`     | Similar to `text`, but typed characters are hidden - replaced with `•`                     |
| `email`        |                                                                                            |
| `date`         | Additional attributes: `min`, `max`                                                        |
| `range`        | Additional attributes: `min`, `max`, `step`                                                |
| `file`         |                                                                                            |
| `checkbox`     | A box which you can check/uncheck                                                          |
| `radio`        | A circle. When you have multiple radio buttons with the same name, only one can be checked |
| `submit`       | Used in forms                                                                              |

(Almost) all of these can have following attributes:
- `value=""` - a "default value". This is gonna be there before you start to type
- `placeholder=""` - a text that will be shown in the input box. The difference between this and `value`, is that `value` is actually written there, `placeholder` is just displayed in the background when no value is provided  
- `name=""` - useful when working with JavaScript. Also, it differs radio buttons (`type="radio"`)
- `required` - as the name states, input with this attribute must be filled in  

### `<label>`
Provides a label for input  
Label is like a header above/before the input field  


Example
```html
<label>
	Enter your username
	<input type="text" name="username" placeholder="Username..." value="Cypo">
</label>
```

<label>
	Enter your username
	<input type="text" name="username" placeholder="Enter your username..." value="Cypo">
</label>


## `<textarea>`
Similar to [`<input>`](#`<input>`), but this one is bigger and can be resized  
```html
<textarea>
Write an essay...
</textarea>
```

<textarea>
Write an essay...
</textarea>

## `<form>`
This tag is useful when working with JavaScript
Stores input  
*(?)*









































# Webpage example
There is a code to provide an example on very simple blog page  
You can see it by opening `HTML-example.html` file in your browser  

```html
a
```

