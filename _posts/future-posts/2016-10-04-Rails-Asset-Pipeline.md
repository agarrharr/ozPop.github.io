---
layout: post
title: A Glance At Rails Asset Pipeline
header-img: ""
---

* What are assets
* What is the Rails Asset Pipeline
* Define the following in context:
    * Asset concatenation
    * Compression / Minification
    * Preprocessing support
* Example of using SASS (and scss)
* Example of using CoffeeScript
* BONUS:
    * autoprefixer-rails


With the raise of the mobile platform, more sophisticated websites and web development tools there has been a rise in architecting yet additional tools to help manage the growing complexity of developing web applications. Whether some of these tools are necessary or not is up for debate but the reality is that as full stack web developers we should be at least aware of these tools.

In particular, web assets have been affected by rise of new tools. The advent of tools such as pre-processors for CSS and Javascript allow us to leverage new and advanced features when working with with web assets. Task runners such as Grunt, Gulp or Guard introduce automation of various tasks. You can speed up your site by levaraging certain mechanisms to process and prepare assets for transportation.

These mechanisms provide us with the ability to do the following:

* Concatenate assets
* Minifiy assets
* Enable use of pre-processors
* Autoprefixing (add vendor prefixes to CSS rules)
* and more...

In preperation for my Rails assessment at Flatiron School, I wanted to take a look at the Asset Pipeline feature of rails (introduced in Rails v3.1).

## What Are Assets?
----

Assets, in any given web project context, are files that the browser makes additional `GET` requests to receive after it begins processing the directives in the initial web document. These files include: _stylesheets, javascript files, media files such as images, video and etc..._

## The Rails Asset Pipeline

Rails 3.1 and above has built in functionality to enable asset concatentation and minification as well as pre-processor support such as Coffeescript or Sass. Rails achieves this using the Sprockets Ruby library for compiling and serving web assets. Earlier Rails versions required use of third party tools.

The asset pipeline is enabled by default. You can disable it when creating a new application by passing the --skip-sprockets option.

`rails new appname --skip-sprockets`

Sprokets enables support for organizing stylesheets and javascript files into smaller more manageable chunks that can be placed in various directories. Using directives in manifest files, Sprokets allows you to turn multiple files into a single file that is concatenated and minified for better performance.

The main features are:

1. Concatenate assets, which can reduce the number of requests that a browser makes to render a webpage.
2. Assets can be minified (compressed). For CSS files this is done by removing whitespace and comments.
3. Enable support for SASS and CoffeeScript and ERB for both by default.

NOTE: Asset pipeline has seen changes since introduction in Rails 3.1 so please refer to documetation for the version you are using.

### Basic Usage

_Development:_

The asset pipeline automatically pre-processes and prepares assets on the fly based on how they are listed in manifest file.

_Production:_

By default Rails assumes assets have been precompiled and will be served as static assets by your web server. You can also invoke the following command to manually prepare assets:

`bundle exec rake assets:precompile`

NOTE: Defaults can be changed. In Rails 4, asset handling is typically configured in config/initializers/assets.rb

### Manifest

An essential file in the Asset Pipeline is the manifest file. By default manifest is created in app/assets/stylesheets/application.css & app/assets/javascripts/application.js directories.

Your manifest files looks commented out, but the lines starting with *= tell Rails which files to go find and include. The require_tree helper method just grabs everything in the current directory.

```css
/*
 * This is a manifest file that'll be compiled into application.css, which will include all the files
 * listed below.
 *
 * Any CSS and SCSS file within this directory, lib/assets/stylesheets, vendor/assets/stylesheets,
 * or any plugin's vendor/assets/stylesheets directory can be referenced here using a relative path.
 *
 * You're free to add application-wide styles to this file and they'll appear at the bottom of the
 * compiled file so the styles you add here take precedence over styles defined in any styles
 * defined in the other CSS/SCSS files in this directory. It is generally better to create a new
 * file per style scope.
 *
 *= require_tree .
 *= require_self
 */
```

### Output

Rails outputs the final file by creating a file that uses what is known as a fingerprinting technique that makes the filename dependent on the contents of that file. So when the contents change, the filename is also changed.

Files are fingerprinted in order to deal with how assets are cached at various stages of web request lifecycle. Using the fingerpting technique, clients will be forced to request a new copy of the content upon a change in file contents.

## Bonus

[Rails Autoprefixer Gem](https://github.com/ai/autoprefixer-rails)

A tool to parse CSS and add verndor prefixes to CSS rules using values from the [Can I Use](http://caniuse.com/). This gem provides Ruby and Ruby on Rails integration with this JavaScript tool.

Just add `gem "autoprefixer-rails"` and run `rake tmp:clear`.

## Conclusion

Today building well optimized sites that are fast, require less downloads and respond immediately has become a necessart part of web application development.

## Sources

* [Asset Pipeline Rails Guides](http://guides.rubyonrails.org/asset_pipeline.html)
* [Rails Asset Pipeline LaunchSchool](https://launchschool.com/blog/rails-asset-pipeline-best-practices)
* [Rails Asset Pipeline Odin Project](http://www.theodinproject.com/ruby-on-rails/the-asset-pipeline)
* [12 Tips for the Rails Asset Pipeline](https://www.reinteractive.net/posts/116-12-tips-for-the-rails-asset-pipeline)





