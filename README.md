# Basic HTML & CSS training

Introductory  materials about how to get started with writing HTML & CSS

# 1. Structure

All site entries **must** have an `index.html` file.
When you open a URL, the browser looks for the `index.html` or `index.php` file and that is the first one to be loaded.

We use the `public` folder to store static files, files that do not change (eg. styles, images, videos, fonts, etc.)

> [!note]
> Some frameworks might process those files, so putting them inside the `public` folder is not indicated. It's always recommended to read the documentation.

## Custom fonts

You can use any (free) font you find online, either by downloading it, or by embedding the font's url in your project.

- Embedding the font using the `<link>` tag:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DynaPuff:wght@400..700&family=Roboto:ital,wght@0,100..900;1,100..900&display=swap" rel="stylesheet">
```
- or the `@import` at-rule:
```html
<style>
@import url('https://fonts.googleapis.com/css2?family=DynaPuff:wght@400..700&family=Roboto:ital,wght@0,100..900;1,100..900&display=swap');
</style>
```
- or using the `@font-face` at-rule for a downloaded one:
```css
@font-face {
    font-family: "DynaPuff";
    src: url("../fonts/DynaPuff-VariableFont_wdth\,wght.ttf");
    font-weight: 400 700 /* the font weight interval [400, 700] */
}
```

From there on you can use them like so:
```css
your-css-selector {
	font-family: "DynaPuff";
	font-weight: 500
}
```

# The base HTML file

- This is a good starter for any `.html` file:
> [!tip]
> by writing `!` or `doc` inside an `.html` file, the emmet autocomplete should output something (almost) this

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header></header>
    <main></main>
    <footer></footer>
</body>
</html>
```
## Semantics in HTML
In HTML, semantics refers to using the proper tags to convey the function of the *web app* ([Form follows function](https://en.wikipedia.org/wiki/Form_follows_function))
There are specific tags for multiple usages, for example:
- `<aside>` represent a piece of information which is indirectly related to the main topic
- `<header>` representing introductory content, navigational aids, etc.
- `<nav>` to bundle navigational aids
- `<footer>` representing, well..., a footer
- `<section>` used to delimit content
- `<span>` used to group elements for styling purposes
- etc, etc...

Some of the benefits from writing semantic markup are as follows:
- Search engines will consider its contents as important keywords to influence the page's search rankings (see [SEO](https://developer.mozilla.org/en-US/docs/Glossary/SEO))
- Screen readers can use it as a signpost to help visually impaired users navigate a page
- Finding blocks of meaningful code is significantly easier than searching through endless `div`s with or without semantic or namespaced classes
- Suggests to the developer the type of data that will be populated
- Semantic naming mirrors proper custom element/component naming

## Custom HTML tags
You can create your own custom HTML tags.
These tags can also be implemented without using any JavaScript, for the purpose of making the code more readable, setting styles to be reused (not the same as Web Components).
As a convention, we'll prepend all components with a `x-`.
> [!important]
> Custom tags must be closed, `<x-my-custom-tag />` is not allowed.

```html
<x-nav-spacer></x-nav-spacer>

<x-deselect-radio>
	<input type="radio" name="planets" id="deselect" value="deselect">
	<label for="deselect"></label>
</x-deselect-radio>
```

## Classes and ID's and Attributes
HTML tags can contain:
- classes (can be assigned to multiple elements on the same page)
- ID's (can be assigned only to one element on the same page)
- attributes (additional values that configure the elements or adjust their behavior)
```html
<div class="card">
	<input type="radio" name="planets" id="ceres" value="ceres">
	<label for="ceres"><img src="public/images/dwarf-planets/ceres.png"></label>
	<div class="info">
		<h2> Ceres </h2>
		<p> Lorem ipsum dolor... </p>
	</div>
</div>
<!--
"type", "name", "value", "for" and "src" are attributes
the id "deselect" cannot be assigned to another element on the same page
elements with the class "card" and "info" appear multiple times on the page
-->
```
## Custom attributes
The same as with custom HTML tags, you can create custom attributes.
As a convention we'll prepend all the custom attributes with `data-`
```html
<img src="" alt="" data-custom-attribute-1 data-custom-attribute-2="Hello">
```
## The `<a>` tag
The anchor tag is used to create link between **sections on the page (using ID's)**, **pages on the site**, **pages on different sites**
```html
<a href="#home"> home </a>
<a href="planets.html"> planets </a>
<a href="google.com" target="_blank"> google </a>
```
> [!tip]
> Set the attribute `target` to "_blank" navigate to the link by opening a new tab

# CSS
I like to start the CSS with the following style.
Elements by default have some padding and margin, and the `box-sizing` is set to "border-box" so the sizing (width and height) will take in account padding, margins and borders.
```css
*, ::after, ::before {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}
```

## the `:root` selector
The `:root` selector references the base of the web page. It is commonly used to create variables and set-up global styles.
```css
:root {
    /* global settings */
    font-family: "Tektur";
    color: var(--color-white);
    scroll-behavior: smooth;
    scroll-padding: 10px;
    background-color: var(--color-bg);

    /* defining color palette variables */
    --color-bg: #20252A;
    --color-white: #E2E6E9;
    --color-accent-1: #084444;
    --color-accent-2: #6D6DC5;
}
```

## Variables
You can define variables in any CSS selector (eg.: the `:root` pseudo tag for global variables or inside another selector for *scoped* variables)
They are defined by prepending the variable name with a double dash `--`. They can have any value available in CSS.
They can also be defined using the `@property` at-rule. (read more [here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_cascading_variables/Using_CSS_custom_properties))
You can then use the variables with the `var()` function.
```css
:root {
	--main-text-color: red;
	--accents-color: #33AAff;
}

div {
	--border-size: 4rem;
	
	color: var(--main-text-color);
	border: var(--border-size) solid black;
	box-shadow: 2px 2px var(--accents-color);
}
```
## CSS selectors
Selectors are used to select specific elements from the page
- to select a html tag: `tag-name{}`
- to select an element by class name: `.class-name {}`
- to select an element by id name: `#id-name {}`
- to select a specific element having a specific class: `tag-name.class-name {}`
- to select multiple elements: `tag1, .class1, #id1, tag2 {}`
You can read more [here](https://www.w3schools.com/cssref/css_selectors.php)
## CSS combinators
Combinators are used to select elements by creating logic between other elements
- descendant (space): `div .info` selects the element with the `info` class that are inside a `div` tag
- child combinator (>): `div > .info` selects all elements with class `info` that are the direct children of the `div` tag
There are other combinators, that can be found for example [here](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Combinators)
## Responsiveness
The concept of responsiveness refers to the ability of a page to change layout depending on different screen sizes (phone, tables, desktops, etc...)
Elements by default are responsive, so we must be careful when adding styles.

For example it's recommended to use `min-height | max-height` or `min-width | max-width` when defining styles, or **responsive units (vw, vh, rem, em, %)** as much as possible.
There are also functions such as [min()](https://developer.mozilla.org/en-US/docs/Web/CSS/min), [max()](https://developer.mozilla.org/en-US/docs/Web/CSS/max), [clamp()](https://developer.mozilla.org/en-US/docs/Web/CSS/clamp).
For responsive texts or lengths you can use the following site, which gives you a `clamp` function.
[Fluid Style](https://fluid.style/)
<iframe width="100%" height="300" src="https://fluid.style/"></iframe>

You can also use the `@media` at-rule to define styles depending on **screen sizes**, **orientation** and others, but these 2 are the most used ones.
For example the following style applies only on devices with a screen width smaller than 550px
```css
@media screen and (max-width: 550px) {
    #socials-section {
        flex-direction: column;
        align-items: center;
    }
}
```

## View Transition API

The view transition api is used to create animations between page changes or components, this way implementing a Single Page Application (SPA)

It can very easily be implemented using the `@view-transition` at-rule and creating an animation.
```css
@view-transition {
    navigation: auto;
}

:root {
    view-transition-name: root; /* the name can be anything you want */
}

@keyframes slide {

    from {
        transform: translateY(0);
        opacity: 1;
    }
    to {
        transform: translateY(-200px);
        opacity: 0;
   }
}

::view-transition-old(root) {
  animation: 0.4s ease-in both slide;
}

::view-transition-new(root) {
  animation: 0.4s 0.3s ease-in reverse both slide;
}
```
