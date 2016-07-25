---
css: wts-reader-custom
layout: post
title: WTSReader Gem
header-img: "img/wtsreader.png"
---

## A project by Blaze Burgees & Ozzie Popovas.

----

**Web To Speech Reader Cli** gem uses native OS X text-to-speech capabilities to read 
certain web pages to the user.

More specifically, WTSReader gem performs web scraping using `Nokogiri` gem and 
`OpenURI` module to retrieve text from webpages. The gem then processes the input
and executes `Speech Sythesis Manager` using proccessed input. The gem offers default
and customized settings for audio playback as well as the the ability to save
those customized settings as future defaults.

Projects dependencies are: 

* `Nokogiri`
* `OpenURI`
* `Colorize`

<br>

### The process

----

This project was a collaborative effort between two people.

**Blaze Burgees** implemented: 

* scraping
* processing
* executing content using _Speech Synthesis Manager_
* handling of audio and settings files

**Ozzie Popovas** was responsible for:

* outlining project requirements
* CLI interface
* settings customization
* project organization
* bug fixing

<br>

### Scraping and executing

----

Processing web content is achived using two classes, `Reader` and `Profile`.

`Reader`

Every instance of *Reader* can only have one document. It is initialized with
a URL and default parameters to be passed into *say* app.

The *Reader* class is responsible for checking if a match exists in *Profile*
and using a predifined profile if one is found, otherwise, the class sanitizes
the passed in web document and sends it to *say*.

`Profile`

The *Profile* class targets specific sites to provide a more refined and 
dependable experience for the user. It contains profiles for **Guardian.com**, 
**Learn.co** and **Stackoverflow.com**. Currently, the guardian profile achieves
the best results.

Unlike the *Reader* class, which attempts to cleanse the document of all undesirble
web page noise, *Profile* class targets specific content and returns it. This
is achieved by having the *Reader* class pass the document upon finding a matching
profile and then using CSS selectors to fetch the content.

NOTE: Guardian profile also has a method that returns an array of Tech section 
headlines.

<br>

### CLI and settings

----

`CLI`

This class provides access to the user interface of the gem. Interanlly it 
consists of the `call` and the `setup` methods.

The `call` method initiates the program and allows the user to access `setup`
which then takes over the remainder of the process.

`call` methods' primary function is to ask the user wherther they want to input 
a web address of their choice OR whether they would like to choose from an 
existing list (guardian technology headlines).

Both _CLI_ methods, but mainly the `setup`, heavily relies on the `Helpers` module.

The `Helpers` module contains a multitude of other methods classified into two 
major sub-modules `CliController` and `CliOutputMethods`.

`CliController`

This module provides access to:

* A list of current Guardian.com technology headlines
* Starting the program using default or customized settings
    * Rate of speech (in wpm)
    * Language and voice choices
* Saving and loading of settings
* Access to languages and voices datastructure

`CliOutputMethods`

This module provides access to:

* Various methods to guide the user through the CLI
* Display methods that improve the output of data
* Help commands
    * Available languages
    * Voice names
    * Rates information

    <br>

### Summary

----

This project was challenging and a lot of fun. Working with Blaze was a pleasure. 
The most challenging aspects of this project were understanding another persons 
code, interfacing with said code, making sure the CLI experience is fluid, fixing 
bugs that popped up along the way, E.G.: handling the error when a voice was not 
downloaded, which was causing our gem to shutdown prematurely.

As it stands the gem can handle various content relatively well. For best 
results, however, we recommend that you use Guardian.com.

**NOTE:** The text-to-speech feature on Mac works best with input that matches 
the type of language. On the fly translation is not reliable.

[Project Repository](https://github.com/ozPop/WTS-Reader-cli-gem)



