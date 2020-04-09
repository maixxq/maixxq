---
title: Generating different background color with JavaScript
date: 2020-03-12 20:47:18
excerpt: Revising code snippets for fun! It has been awhile since the last time I played with frontend, so here is a quick and easy-to-follow recap of basic html,css and javascript from Youtube. Credits to KodeBase for the tutorial. Anyone who wants to start with your first frontend project can definitely check this out! 
type: post
blog: true
---

Anyone can create a static website! First, choose your prefered text editor. There are many text editors in the market with extensive features. Some of the common ones are Visual Studio, Atom and Sublime Text. You can even start without any of these text editors and simply using a text editor pad, that works too. Afterall, all of them serves the same purpose - type our code. 

Next, create a project folder with three empty files. Shortcut to create a file in VS is the cmd + n key. Name each of the files as index.html, style.css and script.js. The three fundamental essential tools to build your project. 

## What is HTML? 
 
 HTML stands for HyperText Markup Language, a common mark up language similar to XML or SVG. While it is not a programming language like JavaScript,python or C++ , HTML outlines the structure of a website. It consists of elements which tell the browser (e.g Google Chrome, Safari) how to display the web page. , Think of these elements as pairwise signboards. Content wrapped between these 'open' and 'close' signboards will be displayed according to the elements. 


Another shortkey for creating the backbone of HTML file in VS editor is by typing '!' + TAB. Also, CSS and JavaScript files have to be embedded in the HTML file so the HTML file can point to the separate external files. 

The CSS file is usually put in the head section while the script file is placed at the bottom of the body section to ensure HTML loads before the script.

Basic HTML Template: 
```js

<!doctype html>

<html lang="en">
<head>
  <meta charset="utf-8">

  <title>Website Title</title>
  <meta name="description" content="HTML Template">
  <meta name="author" content="">

  <link rel="stylesheet" href="css/styles.css?v=1.0">

</head>

<body>
  <script src="js/scripts.js"></script>
</body>
</html>

```


## What is CSS?

CSS stands for Cascading Style Sheets. Bascially, this is what beautifies a website. There is a proliferation of CSS properties we can use to style our site. However, remember to check browser compatibaility to newly added CSS features as not all browsers may implement that feature. I was overwhelmed when I was first introduced to css. I love how it can make a website visually so appealng but it seems that there are endless properties to use. A CSS cheatsheet comes in handy in this case. Creating your own unique CSS cheatsheet is a good idea, else there are already many comprehensive cheatsheet exist online thanks to the amazing community. 

CSS can get tricky but it is satisfying to see how your site looks nicer with additional features we put in. It's always a good idea to have an end goal in mind before writing CSS. Sketching the general layout of the site and disecting each parts of the site into boxes can make our progess easier. We call this the Box Model! 

And one way or another, this is something very relatable!

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">hey everyone I finally solved centering things in CSS <a href="https://t.co/aky93AsAr0">pic.twitter.com/aky93AsAr0</a></p>&mdash; Jacob Paris 🇨🇦 (@jacobmparis) <a href="https://twitter.com/jacobmparis/status/1245193222181326848?ref_src=twsrc%5Etfw">April 1, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## What is Javascript?

As stated in MDN web docs, "JavaScript is a scripting or programming language that allows you to implement complex features on web pages". It makes dynamic behaviours possible on a web page. Everytime when you click a button on a website and something pops up or something else loads, it is almost certain that JavaScript is doing its work. It is a language responsible for user-interation, driven by possible 'events' happening on the page.

Here is the final product!

<iframe src="https://giphy.com/embed/S73VQLJsYAwSMErcY2" width="480" height="240" frameBorder="0" class="giphy-embed" style="padding-left: 150px "></iframe>

:tada: 
