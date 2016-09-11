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

Upon entering a URL and requesting a website to be displayed the user triggers a chain of processes that encompass mutliple layers of technologies and protocols. The proccesses are so complex that it would require several college level networking courses to fully explain.

Below is an explanation that covers only the some of the cases and gollses over the overall process of a quintessential web request.

1. [User enters URL](user-enters-url)
2. [DNS lookup](dns-lookup)
3. [Initiate TCP/IP connection](initiate-tcp-ip-connection)
4. [Client HTTP request](client-http-request)
5. [Server Processes Payload](server-processes-payload)
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


### Initiate TCP IP connection

Communication between networked computers is carried out using protocol suits. The most widely used and most widely available protocol suite is TCP/IP protocol suite. TCP/IP is considered to be a 4 layer system. 

![TCP/IP concept pic](http://www.thegeekstuff.com/wp-content/uploads/2011/10/tcp-ip.png)

For the purposes of this blog, the most important thing to mention is that once a client recieves an IP address, the following step is opening of a **"network socket"** so that a client and server can communicate.

> A socket is one endpoint of a two-way communication link between two programs running on the network. A socket is bound to a port number so that the TCP layer can identify the application that data is destined to be sent to.

### Client HTTP request

Once client successfuly initiates a TCP connection with the server, it prepares an HTTP request according to the specification of the HTTP protocol to be sent to the host.

Various information is included in the form of headers.

![Request Header Example pic](https://cdn.tutsplus.com/net/uploads/legacy/511_http/request_header.png)

* **Initial Request Line**
* **Accept-Encoding** headers specify the type of responses it will accept
* **User-Agent** header specifies the browser properties
* **Connection** header tells the server to keep open the TCP connection
* **Host** URL
* **Cookies** may be included


### Server Processes Payload

Web Server application processes the request by launching proper request handler

A program that handles web services: PHP, Ruby, Java, Python

This program will generate a response which will be sent back


* Client recieves the response payload
    * Various information is included in the reponse
* Client browser processes recieved content
    * Add detailed steps
* Client renders the document


## SOURCES

1. [URL - Wikipedia](https://en.wikipedia.org/wiki/Uniform_Resource_Locator)
2. [Host Name Resolution](https://technet.microsoft.com/en-us/library/cc958812.aspx)
3. [Difference between Authoritative and Recursive DNS](https://blog.opendns.com/2014/07/16/difference-authoritative-recursive-dns-nameservers/)
4. [TCP/IP Protocol Fundamentals](http://www.thegeekstuff.com/2011/11/tcp-ip-fundamentals/)
5. [A brief overview of TCP/IP communications](http://www.taltech.com/datacollection/articles/a_brief_overview_of_tcp_ip_communications)
6. [What Is a Socket?](https://docs.oracle.com/javase/tutorial/networking/sockets/definition.html)