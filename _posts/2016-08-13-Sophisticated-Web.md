---
layout: post
title: The Sophisticated Web Request
---

Topic question:

Explain to me, in as much detail as you can, the steps that take place when you enter a URL in browser and hit enter.

URL: **Uniform Resource Locator**, more commonly known as a **Web Adress**, is a reference to a web resource on a computer network and a mechanism for obtaininig that resource.

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