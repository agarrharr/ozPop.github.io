---
layout: post
title: The Sophisticated Web Request
---

## Blog Topic and Why I Chose It

Last month, I met a friend at Bierocracy, a beer hall located in Long Island City. My friend, whom I will refer to as Dr.Lezaru, has been involved in web development field for over a decade. As we shared our experiences while enjoying the lovely brew and the effects of alchohol on our pallets and minds, I was presented with a question.

![The Philosophy of Moe From Simpons](http://www.dadsbigplan.com/wp-content/uploads/2011/05/beer-is-the-answer.jpg)

Dr.Lezaru asked me to explain, in as much detail as I could, **the processes that take place when you enter a URL in a browser and press enter**. He added that in his exprience this question is sometimes asked during interviews and many junior developers tend to give an incomplete answer.

After taking another sip of the _Great Divide Yeti Imperial Stout_, I took a moment to compose myself and gather my thoughts. My initial response was not wrong, however, it was only partial. Not only had I skipped over a number of fundamental steps that occur in the process, my answer incomplete and lacked the kind of detail that Dr.Lezaru expected.

![Great Divide Yeti Imperial Stout Pic](http://media-cache-ec0.pinimg.com/736x/6a/35/94/6a359488fab2d49364209ea9d2e02882.jpg)

So, after having another Yeti and hearing about the intricacies behind the processes, I decided that I would come back to this topic and investigate it further, perhaps even write a blog post.

What I have since discovered is that the ammount of layers of comlexity that exist when you request that site is staggering. My goal for this post is to condense as much as possible the whole process, so that when I am asked this question again, I can provide a better answer than the one I gave in the past.

## The Answer

Upon entering a URL and requesting a website to be displayed the user triggers a chain of processes that encompass mutliple layers of technologies and protocols. The proccesses are so complex that it would require several college level networking courses to fully explain and cover all the parts.

Below is an explanation that covers only the some of the cases and gollses over the overall process of a quintessential web request.

1. User enters URL
2. DNS lookup
3. Establishing Client/Server connection
4. Client HTTP request sent
5. Server processing
6. Server HTTP response sent
7. Client processing
8. Client renders document

### User Enters URL

URL stands for **Uniform Resource Locator**, more commonly known as a **Web Address**. It is an address identifier of a web resource on a computer network and is mechanism for obtaininig that resource.

As a mechanism it specifies how information is to be transfered, most commonly using the HTTP protocol. Among others are HTTPS, FTP, EMAIL and more.

It also contains a host name which is an alias for an IP address used to identify a machine connected to the web.

### DNS lookup

Once the browser parses the URL that has been passed into the address field, a DNS lookup is performed. The browser first needs an IP address in order to identify a host and initialize a TCP/IP connection.

The steps of DNS lookup:

* Check browser cache
    * Browsers caches DNS records for a fixed duration
* Check OS cache
    * Browsers makes a system call to check OS cache
* Router Cache
    * Typically routers contain a cache of DNS records
* ISP Cache
    * Next up is ISP cache if the above steps fail
* Recursive Search
    * Lastly ISPs recursive search kicks in, going through the authoritative DNS hierarchy.

![Authoritative DNS Hierarchy Pic](https://s3-us-west-1.amazonaws.com/umbrella-blog-uploads/wp-content/uploads/2014/07/Screen-Shot-2014-07-16-at-10.56.09-AM.png)

<sup>
(3) Root domain nameservers know the IP addresses of Top Level Domains (TLD) like “.com”, “.edu” or “.gov”.<br>
(4) Authoritative server for “.com” knows where it can find “google.com”.<br>
(5) Then “google.com” is asked where to find “www.google.com”.<br>
</sup>

#### NOTE:

A client can retrieve a resource using an IP directly however, some websites have multiple servers in multiple locations to support millions of requests simultaneously. Using a URL, we let the host decide which IP our client should connect to. This involves a **load-balancer** which is a piece of hardware that listens on a particular IP address and forwards the requests to other servers. Major sites will typically use load balancers.


### Initiate TCP/IP connection
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
2. [Host Name Resolution](https://technet.microsoft.com/en-us/library/cc958812.aspx)
3. [Difference between Authoritative and Recursive DNS](https://blog.opendns.com/2014/07/16/difference-authoritative-recursive-dns-nameservers/)