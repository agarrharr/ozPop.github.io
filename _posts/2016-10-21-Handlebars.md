---
css: handlebars
layout: post
title: Templates in Handlebars.js
header-img: "img/handlebars.jpg"
---

### Target audiance

Someone who has not used Handlebars.js.

### Blog topic
----

This is a guide to setting up Handlebars.js templates. Handlebars.js templates can be written in the HTML file or separately. In this blog I will cover how to setup the template inside an HTML file and how to pre-compile your templates inside a separate folder.

### Handlebars.js
----

[Handlebars.js](http://handlebarsjs.com/) is a Javascript templating language. It is an extension of Mustache, with a few additional features. It renders Mustache templates in addition to Handlebars.js templates. Unlike Mustache, which is a logicaless templating system, Handlebars.js adds extensibility and minimal logic through what are known as *helpers*. There exist a number of alternatives to Handlebars.js.

* [Mustache](http://mustache.github.com/) - Available in various languages
* [mustache.js](https://github.com/janl/mustache.js) - Javascript port of Mustache
* [Emblem.js](http://emblemjs.com/) - Alternative for Handlebars.js
* and more...

### What does it do?
----

To understand what Handlebars.js accomplishes, we first need to define what a semantic template is. 

> Semantic templates are an alternative to constructing long strings of HTML within your Javascript logic. They take a property of a Javascript object and render it straight into the template. [Source](http://codinghouse.co/blog/getting-started-with-handlebars-js/)

- Handlebars.js compiles semantic templates with variables and gives us back a Javascript function which accepts an object as an argument.
- The object (usually in JSON format) is known as _context_ containing the values of the variables specified in the template.
- That function returns a string that contains the generated HTML filled with values in place of those variables.

Handlebars.js accomplishes a number of things:

* Keeps HTML pages clean separating templates from business logic in Javascript files. This improves application structure, maintainability and scalability
* Provides an easier way of updating the data on the view
* Comes with built in helpers and allows for creation of your own helpers
* Allows pre-compiling of templates which speeds up your application

### Templates inside HTML
----

The initial step is to link the required resources. If you are using jQuery link that, the Handlebars.js library and your Javascript source.

```html
<script src="jquery-3.1.0.min.js"></script>
<script src="handlebars.js"></script>
<script src="index.js"></script>
```

Next up is adding your template at the bottom of `<body>`, below the `<script>` tags shown above.

{% raw %}
```html
<script id="info-template" type="text/x-handlebars-template">
  <p>My name is {{name}} and my interests are {{interests}}</p>
</script>
```
{% endraw %}

The variables are written in double curly braces {% raw %}`{{}}`{% endraw %} and are known as expressions which will be filled with values from your data source.

Final HTML:

{% raw %}
```html
<body>
  <main id="main">
  <div class="flexbox-container">
    <div class="contents-wrap">
      <button id="display">Display Info</button>
      <h3>Info</h3>
      <div id="info"></div>
    </div>
  </div>
  <script src="jquery-3.1.0.min.js"></script>
  <script src="handlebars.js"></script>
  <script src="index.js"></script>
  <script id="info-template" type="text/x-handlebars-template">
    <p>My name is {{name}} and my interests are {{interests}} </p>
  </script>
</body>
```
{% endraw %}

Next up is your Javascript file.

{% raw %}
```javascript
    /*jshint esversion: 6 */
    $(document).ready(function() {
      clickHandler();
    });
    const data = { "name": "Dong", "interests": "Crocodile Hunting" };
    function clickHandler() {
      $('#display').on('click', showInfo);
    }
    function showInfo() {
      let source = $('#info-template').html();
      let template = Handlebars.compile(source);
      let html = template(data)
      $('#info').append(html);
    }
```
{% endraw %}

The lines that matter to us are inside the `showInfo()`. Lets break them down.

{% raw %}
```javascript
    // Retrieve the template data from the HTML using jQuery
    let source = $('#info-template').html();

    // console.log() output
    <p>My name is <span>{{name}}</span> and my interests are <span>{{interests}}</span> </p>
```
{% endraw %}

{% raw %}
```javascript
    // Compile the template data into a function
    let template = Handlebars.compile(source);

    // console.log() output
    function ret(context, execOptions) {
        if (!compiled) {
          compiled = compileInput();
        }
        return compiled.call(this, context, execOptions);
    }
```
{% endraw %}

{% raw %}
```javascript
    // Generate HTML by passing your context (data) into the compiled function
    let html = template(data);

    // console.log() output
    <p>My name is <span>Dong</span> and my interests are <span>Crocodile Hunting</span> </p>    
```
{% endraw %}

```javascript
    // Finally insert the HTML into the page
    $('#info').append(html);
```

#### [View working example](https://codepen.io/anon/pen/gwQNqg)

### Pre-Compiling Templates
----

Lets say your are planning to use Handlebars.js extensively and placing the templates inside your main HTML file is not what you want. As you have seen above, the first thing Handlebars.js does is compile the template into a function. This operation is expensive on the client. We can remedy this by utilizing what is known as **template pre-compilation**.

Choosing to do this, we can improve the performance of the application by having the client perform only the execution of that function, not the actual compilation of it.

First step is to install Handlebars.js globally.

`$ npm install -g handlebars`

Create a folder in your projects js directory and call it templates. You can use any directory name you want but then make sure to edit the commands provided below.

`$ mkdir js/templates`

Lets say your have this template inside your HTML.

{% raw %}
```html
<script id="info-template" type="text/x-handlebars-template">
  <table cellspacing="10">
    <thead>
      <th>Name</th>
      <th>Interests</th>
    </thead>
    <tbody>
      {{#items}}
        <tr>
          <td>{{name}}</td>
          <td>{{interests}}</td>
        </tr>
      {{/items}}
    </tbody>
  </table>
</script>
```
{% endraw %}

Grab your template and put it into the newly created templates directory by creating a file with the extension `.handlebars`. For this example I am creating a file named `info.handlebars`. Inside these files you do not need script tags. Your file should look like this.

{% raw %}
```handlebars
<table cellspacing="10">
  <thead>
    <th>Name</th>
    <th>Interests</th>
  </thead>
  <tbody>
    {{#items}}
      <tr>
        <td>{{name}}</td>
        <td>{{interests}}</td>
      </tr>
    {{/items}}
  </tbody>
</table>
```
{% endraw %}

Now open bash and run the following command:

`$ handlebars js/templates -f js/templates/templates.js`

The `-f` flag just means your outputting into a file. There are other flags that minify or create a source map file, details available via the `$ handlebars -h` command.

Now back in your main HTML file link the newly created `templates.js` file and download the [runtime file](http://builds.handlebarsjs.com.s3.amazonaws.com/handlebars.runtime-v4.0.5.js). Having pre-compiled your templates you no longer need the full Handlebars.js library.

```html
    <body>
      <main id="main">
      <div class="flexbox-container">
        <div class="contents-wrap">
          <button id="display">Display Info</button>
          <h3>Info</h3>
          <div id="info"></div>
        </div>
      </div>
      <script src="jquery-3.1.0.min.js"></script>
      <script src="handlebars.runtime-v4.0.5.js"></script>
      <script src="index.js"></script>
      <script src="js/templates/templates.js"></script>
    </body>
```

Going back to the Javascript file, modify the `showInfo()` function to reflect the changes in approach.

**Previous**

```javascript
    function showInfo() {
      let source = $('#info-template').html();
      let template = Handlebars.compile(source);
      let html = template(data)
      $('#info').append(html);
    }
```
**Updated**

```javascript
    function showInfo() {
      let template = Handlebars.templates['info'];
      $('#info').html(template(data));
    }
```

#### [For a working example, click here.](https://codepen.io/anon/pen/GjPKEP)

### Conclusion
----

Upon reaching the Ajax labs in jQuery section (fullstack track), Handlebars.js is something that you are expected to figure out on your own. Perhaps the idea is to make you work without guidance and possibly to make you realize that you can take something relatively unfamiliar and figure it out. I hope this blog will help those who are trying to do just that. Get a handle on Handlebars.js.

This guide barely scratched the surface of what Handlebars.js can do for you.  For more information please check the resources below.

### Sources
----

* [Wiki page](https://en.wikipedia.org/wiki/Handlebars_(template_system))
* [Official Docs](http://handlebarsjs.com/installation.html)
* [A Beginner’s Guide to Handlebars](https://www.sitepoint.com/a-beginners-guide-to-handlebars/)
* [Getting Started With Handlebars.js](http://codinghouse.co/blog/getting-started-with-handlebars-js/)
* [How to Precompile Handlebars Templates](http://www.adamwadeharris.com/how-to-precompile-handlebars-templates/)
* [A Look Into: Handlebars.js](http://www.hongkiat.com/blog/a-look-into-handlebarsjs/)
* [Step-by-step getting started tutorial](http://learnwebtutorials.com/step-by-step-getting-started-tutorial-using-handlebars-js)
* [Getting Started with Handlebars.js](http://blog.teamtreehouse.com/getting-started-with-handlebars-js)
* [Handlebars.js Part 2: Partials and Helpers](http://blog.teamtreehouse.com/handlebars-js-part-2-partials-and-helpers)

