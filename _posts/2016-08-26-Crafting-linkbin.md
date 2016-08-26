---
css: crafting-linkbin
layout: post
title: Crafting linkbin
header-img: "img/crafting-linkbin.png"
---

## Coming up with an idea

When thinking about what to make for my Sinatra Assessment project, I tried to put into practice the notion of utilizing the power of computing to create tools that make our lives easier.

Once I began to brainstorm ideas, it wasn't long before I realized that I wanted to make a modest hyperlink management application.

I come across many links every day. Whether it is early in the AM while riding the subway, during my day on the Flatiron campus, or any other given moment that I spend on the Web. I am always coming across links.

My link management solutions are bookmarking or emailing links to myself to be bookmarked later. I manage my bookmarks by creating various folders.

I thought it may be useful to have quick access to a web application that makes it easy for a user to categorize, annotate and store links.

I am not sure if or what alternative applications exist that accomplish this. At this moment in time that is not important to me. The important thing is that it meets my assessment requirements, challenges me to apply various things I have been learning and ideally turns out to be useful.

## Thinking about models and relationships

The next major step was to come up with models and build relationships between those models. With the help of Antion I came up with this.

![linkbin-uml](http://i.imgur.com/Jm6lXec.png)

##### created using [draw.io](https://www.draw.io/)

## Narrowing down scope and features

At the outset of the project, before things started to be built, I noticed that it was easy to overreach and think big. So, after being grounded by Antoin, I pulled back and came up with a more humble foundation.

The basic functionality:

* Choose or create categories with ease
* Add a title
* Add link(s)
* Add text content
* Easy to use on various devices
* Display basic information about each item created

## Starting to code things

Starting to code a project is quite a daunting experience for me. As we have been shown throughout the curriculum so far, I broke down the requirements and tackled them one at a time.

* Deciding how to store data
    * Postgres
* Setting up the project structure
    * Application environment
    * Basic models
    * Writing of migrations
    * Migrating
* Getting the basic logic in place
    * Controllers
        * Application
        * User
        * Note
    * Views
        * Application index
        * Layouts

The bullets above are roughly in the order that I followed to get started. Following that, I implemented the rest of the application.

* Registration
* Login
* Various other views
* Styling of the views
* Refactoring code

## Mobile First & Responsive Design

Prior to implementing the basic functionality, I decided to go with a mobile first approach for this project. Partly because I wanted to put into practice the philosophy, but more so than that, because I feel like having this kind of tool on the go may be useful.

I would like to dedicate the rest of my blog post to the topic of **Mobile-First Responsive Design**.

So what is this Mobile-First Responsive Design?

![Goofy with questions](http://i.imgur.com/TS6hLTu.png)

It is a blend of philosophies and approaches that boils down to wider utilization of best practices and effective strategies.<br>

In other words, due to the fast growing number of devices that get connected to the web, we should consider design experiences that work across a wide range of digital devices.

* Currently there are **1.2 billion mobile users globally**
* In US, 25% of Web users access Internet using mobile device only
* Mobile app download numbers are in billions

### Mobile First 

The approach was created by Luke Wroblewski and it prioritizes mobile context when creating user experiences.

![Luke Wroblewski](http://i.imgur.com/mmRHeie.png)

> LukeW is an internationally recognized digital product leader who has designed and built software used by more than one billion people worldwide.

> Luke is currently a Product Director at Google.

By choosing to go mobile first, you are able to:

1. **Reach more people** and ensure a more analogous experience
2. **Focus your content** and prioritize important information
3. **Utilize latest technologies** that are geared towards small devices

According to [pcmag dot com](http://www.pcmag.com/article2/0,2817,2485277,00.asp), by 2020 global smartphone subscriptions will more than double. More than six billion people, 70% of the population, will own smartphones, and 90% will be covered by broadband networks.

### Responsive Design

The term Responsive Design was coined by Ethan Marcotte who is an independent web designer, speaker and an author. He lives in Boston, Massachusetts and cares deeply about beautiful design, elegant code, and the intersection of the two.

![Ethan Marcotte](http://sparksheet.com/wp-content/uploads/2015/01/ethan-marcotte.jpg)

Responsive Design details how developers and designers can create site layouts for multiple screen resolutions. Responsive Design utilizes:

1. **Fluid grids** - adapt content to user environment
2. **Flexible images and media** - uniform content on various resolutions
3. **Media queries** - introduce breakpoints

If you are not familiar with Ethan's work or just find it interesting I recommend [this article](http://alistapart.com/article/responsive-web-design) by him.

## Conclusion

In conclusion, unless you know that your target audience is strictly non mobile, I encourage you to keep the mobile first approach in mind because of the reasons outlined above. I believe that thinking about the layout, emphasizing content, maintaining clarity and focus and keeping user perspective in mind is an important part of creating web applications.


### Sources

1. [Luke Wroblewski](http://www.lukew.com/about/luke/)
2. [PCmag article on smartphone numbers](http://www.pcmag.com/article2/0,2817,2485277,00.asp)
3. [Mobile First bradfrost dot com](http://bradfrost.com/blog/web/mobile-first-responsive-web-design/)
4. [Ethan Marcotte](http://ethanmarcotte.com/)
5. [Fluid Grids](http://1stwebdesigner.com/fluid-grid-layout/)
6. [Organizing Mobile by LukeW](http://alistapart.com/article/organizing-mobile)