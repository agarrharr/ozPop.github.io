---
css: cozy-with-pry
layout: post
title: Getting Cozy With Pry
header-img: "img/cozy-pry.png"
---

Moving beyond the basics.

_Target audience:_ Individuals who have some experience with using Pry, Object 
Oriented Ruby.

Discussion points:

* Running shell commands from Pry console
* Editing code from within Pry session
* Using `gist` to create snippets
* Exploring contexts

<br>

### Running shell commands

You can run the usual shell commands by using dot notation. That is, by prefacing 
a particular command with a dot while in Pry. E.G.: `.ls`, `.cat`, `.pwd`.

This is particularly helpful if you need to edit or move files on the fly without
leaving the Pry session.

Watch the video for a quick exmaple:

{% youtube -7cNsFJ8gGc %}

<br>

### Editing code

You can edit code from within a Pry session. To do that we use the `edit` 
command. Just point the command to a whole file or tell Pry you want to edit a 
specific method.

For example, lets edit a class method called `list_animal_types` in which we 
correct some code. Watch the video below for a quick example of that workflow.

_NOTE:_ Please edit your _~/.pryrc_ file and specify your desired editor. In the
case of sublime, just add:

`Pry.config.editor = 'sublime -n'` (the `-n` flag will open a new sublime window)

{% youtube QwbzJbQB0JA %}

<br>

### Using gist to create snippets from pry

We can create snippets of code without leaving pry. Using the `gist` command,
Pry allows us to push code to [GitHub Gist](https://gist.github.com/) on the fly.

_NOTE:_ In order to be able to use this feature you may have to install the 
**gist gem**. Just run `gem install gist` in case you dont have the gem and 
want to use this feature.

_NOTE#2:_ I am using `-l` flag at the end in order to display line numbers.

How to create a gist in Pry:

![How to create a gist](http://i.imgur.com/olvVRct.png)

![Gist](http://i.imgur.com/CS2A2uF.png)

<br>

### Exploring contexts

* what is context?
    * how to load class contexts
        * using require_relative (http://i.imgur.com/aYnCgvh.png)
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
