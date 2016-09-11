---
layout: post
title: The Sophisticated Web Request
---

## Blog Topic and Why I Chose It

Last month, I met a friend at Bierocracy, a beer hall located in Long Island City. My friend, whom I will refer to as Dr.Lezaru, has been involved in web development field for over a decade. As we shared our experiences while enjoying the lovely brew and the effects of alchohol on our pallets and minds, I was presented with a question.

![The Philosophy of Moe From Simpons](http://www.dadsbigplan.com/wp-content/uploads/2011/05/beer-is-the-answer.jpg)

Dr.Lezaru asked me to explain, in as much detail as I could, the processes that take place when you enter a URL in a browser and press enter. He added that in his exprience this question is sometimes asked during interviews and many junior developers tend to give an incomplete answer.

After taking another sip of the _Great Divide Yeti Imperial Stout_, I took a moment to compose myself and gather my thoughts. My initial response was not wrong, however, it was only partial. Not only had I skipped over a number of fundamental steps that occur in the process, my answer incomplete and lacked the kind of detail that Dr.Lezaru expected.

![Great Divide Yeti Imperial Stout Pic](http://media-cache-ec0.pinimg.com/736x/6a/35/94/6a359488fab2d49364209ea9d2e02882.jpg)

So, after having another Yeti and hearing about the intricacies behind the processes, I decided that I would come back to this topic and investigate it further, perhaps even write a blog post.

What I have discovered is that the ammount of layers of comlexity that exist when you request that site is staggering. My goal for this post is to condense as much as possible the whole process, so that when I am asked this question again, I can provide a better answer than the one I gave in the past.

## The Answer

URL stands for **Uniform Resource Locator**, more commonly known as a **Web Adress**. It is a reference to a web resource on a computer network and a mechanism for obtaininig that resource.[1]

Rough outline of the process:

* DNS lookup
    * Add detailed steps
* Initiate TCP/IP connection
    * Open the "network socket"
* Client assembles HTTP request and sends it
    * Various information is included in the request
* Server recieves the request payload
    * Web Server application processes the request by launching proper request handler
        * A program that handles web services: PHP, Ruby, Java, Python
        * This program will generate a response which will be sent back
* Client recieves the response payload
    * Various information is included in the reponse
* Client browser processes recieved content
    * Add detailed steps
* Client renders the document


## SOURCES

1. [URL - Wikipedia](https://en.wikipedia.org/wiki/Uniform_Resource_Locator)