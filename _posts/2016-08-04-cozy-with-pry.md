---
css: cozy-with-pry
layout: post
title: Getting Cozy With Pry
header-img: "img/cozy-pry.png"
---

Moving beyond the basics.

*Target audience:* Individuals who have some experience with using Pry, Object 
Oriented Ruby.

Discussion points:

* Running shell commands from Pry console
* Editing code from within Pry session
* Using `gist` to create snippets
* Exploring contexts

### Running shell commands

Do a quick intro about the ability to run all sorts of shell commands by prefacing
the command with a dot `.`.

### Editing code

You can edit code from within a Pry session. To do that we use the `edit` 
command. For example, lets edit a class method called `list_animal_types`. Watch
the video below for a quick example of that workflow. (SAVED VIDEO TO DOWNLOADS)

NOTE: [check here](https://gist.github.com/joelverhagen/1805814) on how to embed
video into jekyll blog
[Video example](URL)



### Using gist to create snippets from pry
    * using -l to show line numbers



### Exploring contexts

* what is context?
    * how to load class contexts
        * using require_relative './config/evironment.rb' (img already saved)
    * examples of main context
    * class context
    * instance of class context
* requiring objects
* moving around in different scopes
* showing nesting
* jumpt-to specific scope


Pry Part 3 blog?

* Made a typo in pry?
    * explain how `show-input` works
    * clear buffer with `!`
    * how to `amend-line #`
* Searching history
