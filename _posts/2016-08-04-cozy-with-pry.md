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
* Exploring Pry contexts

<br>

### Running shell commands

----

You can run the usual shell commands by using dot notation. That is, by prefacing 
a particular command with a dot while in Pry. E.G.: `.ls`, `.cat`, `.pwd`.

This is particularly helpful if you need to edit or move files on the fly without
leaving the Pry session.

Watch the video for a quick exmaple:

{% youtube -7cNsFJ8gGc %}

<br>

### Editing code

----

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

### Using gist

----

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

----

#### What is a context? 

I found it helpful to think of context as visibility of **"entities"**,
entities being a method, class, object, scope or file. In Prys' case, 
it is usually objects.

When you start Pry from the terminal or outside the scope of a class in any given 
file, Pry will start in default context. The default context is known as `main`.

The `main` context, by default, gives you access to various built in ruby objects.

![Main context example](http://i.imgur.com/wYpsHZM.png)

The fun begins when we start Pry in locations where it has access to various 
other contexts such as: our own classes or objects that we bring into our 
projects via various gems. In addition to starting Pry in specific locations 
that give access to those contexts, we can bring contexts into our Pry session.

We can load class contexts into Pry using `require_relative`.

![Require relative farmer class](http://i.imgur.com/tOhz8eH.png)

Or we can require the whole environment! This will gives us access to all of 
the contexts.

![Require the whole evironment](http://i.imgur.com/aYnCgvh.png)

_NOTE:_ If you use the `edit` command to edit a praticular class, the class 
context becomes available automatically.

#### Starting in a particular context

We can start Pry within a class context or within an instance of a class. when 
we insert a `binding.pry` or `Pry.start` inside the class itself.

_NOTE:_ Keep in mind that when execution hits `Pry.start` it starts a new session!

Lets use `binding.pry` of our example.

**Prying into a class**

![Prying into a class](http://i.imgur.com/9faPp6h.png)

**Prying into an instance of class**

![Prying into an instance of a class](http://i.imgur.com/hnBaNBI.png)

**What is the difference?**

List while in class context:

![ls class context](http://i.imgur.com/LMmfi89.png)

List while in instance context:

![ls instance context](http://i.imgur.com/3Ouci1U.png)

### Listing contents and moving around contexts

Using commands like `cd` and `ls` we can move in and out of contexts or inspect 
those contexts. The behavior of these two commands is similar to how they behave
in bash. `cd` can be used to move in and out of contexts (objects or scopes) and 
`ls` is useful when inspecting the contents of said entities.

When we move into different contexts (e.g.: classes) Pry is keeping track of 
where we are. We can inspect how deeply nested we are by invoking a command 
called `nesting`.

Using `jumpt-to` command we can quickly move around different contexts.

View the below video for examples how these commands work:

{% youtube -RomBt0IpQk %}

### Conclusion

Getting involved with Pry and Prys' more advanced features has proven to be 
invaluable to me. I rely on Pry a lot in order to make sense of what is happening
in the code I am working with at any given time. I highly recommend that you review 
Pry documetation and related resources in order to become more familiar with 
this awesome tool.


### Other useful related tips:

Made a typo while writing a method in Pry?

* Explore how `show-input` works and how to `amend-line #`.

_NOTE:_ Clear input buffer with `!` and check out what searching `history` is.

### Sources

* [Offical Docs](https://github.com/pry/pry/wiki)
* [Intro Screencast](http://vimeo.com/26391171)
* [Useful Features In Pry](http://www.bignerdranch.com/blog/my-top-5-pry-features/)
* [In-Depth Look At binging.pry](http://kyrylo.hatenablog.com/entry/2013/05/29/so-what-is-binding-pry-exactly)
