---
css: sophisticated-web
layout: post
title: Life Cycle Of An HTTP Request
header-img: ""
---

## Blog Topic and Why I Chose It
----

Last month, I met a friend at Bierocracy, a beer hall located in Long Island City. My friend, whom I will refer to as Dr.Lezaru, has been involved in web development field for over a decade. As we shared our experiences while enjoying the lovely brew and the effects of alchohol on our pallets and minds, I was presented with a question.

![The Philosophy of Moe From Simpons](http://www.dadsbigplan.com/wp-content/uploads/2011/05/beer-is-the-answer.jpg)

Dr.Lezaru asked me to explain, in as much detail as I could, **the processes that take place when you enter a URL in a browser and press enter**. He added that in his exprience this question is sometimes asked during interviews and many junior developers tend to give an incomplete answer.

After taking another sip of the _Great Divide Yeti Imperial Stout_, I took a moment to compose myself and gather my thoughts. My initial response was not wrong, however, it lacked some essential details. Not only had I skipped over a number of fundamental steps that occur in the process, my was answer incomplete and lacked the kind of detail that Dr.Lezaru expected.

![Great Divide Yeti Imperial Stout Pic](http://media-cache-ec0.pinimg.com/736x/6a/35/94/6a359488fab2d49364209ea9d2e02882.jpg)

So, after having another Yeti and hearing about the intricacies behind these processes, I decided that I would come back to this topic and investigate it further, perhaps even write a blog post.

What I have since discovered is that the ammount of layers of comlexity that exist when you request a site is staggering. My goal for this post is to condense as much as possible the whole process, assuming no problems occur in any step of the HTTP request, so that when I am asked this question again, I can provide a better answer than the one I gave in the past.

## The Answer
----

Upon entering a URL and requesting a website to be displayed, the user triggers a chain of processes that encompass layers of technologies and protocols. The proccesses are so complex that it would require several college level networking courses to fully explain.

Below is an attempt to provide a reatively rough and simplified summary glossing over the overall process of a quintessential web request.

1. [User Enters URL](user-enters-url)
2. [DNS Lookup Is Performed](dns-lookup)
3. [Browser Initiates TCP/IP Connection](initiate-tcp-ip-connection)
4. [Client Sends HTTP Request](client-http-request)
5. [Server Receives And Processes Payload](server-processes-payload)
6. [Server Prepares And Sends HTTP Response](server-http-response)
7. [Client Interprets And Renders Document](client-renders-document)

### User Enters URL
----

_URL_ stands for **Uniform Resource Locator**, more commonly known as a **Web Address**. It is an identifier of a web resource on a computer network and is a mechanism for obtaininig that resource.

As a mechanism it specifies how information is to be transfered, most commonly using the HTTP protocol. Some other protocols are HTTPS, SSH, FTP, Telnet and more.

![URL explained pic](http://2.bp.blogspot.com/-bUZfwn4_ev0/TqK0eMjVrfI/AAAAAAAAAK0/7_9ffOmZ61E/s1600/url.png)

A URL also contains a domain name which is an alias for an IP address used to identify a machine connected to the web.

### DNS lookup
----

A **Domain Name System** is one of the protocols that comprise TCP/IP suite. It is a service that translates domain names into IP addresses. Domain names are alphabetic which makes them easier to remember and hence more user friendly while web resrouces are actually identified using IP addresses.

Once the browser parses a URL, a DNS lookup is performed. The browser first needs an IP address in order to identify a host and initialize a TCP/IP connection.

The steps of DNS lookup are as follows:

1. Check Browser Cache
    * Browsers cache DNS records for a fixed duration
2. Check OS Cache
    * Browsers make a system call to check OS cache
3. Check Router Cache
    * Typically routers contain a cache of DNS records
4. Check ISP Cache
    * Next up is ISP cache if the above steps fail
5. Perform a Recursive Search
    * Lastly ISPs recursive search kicks in, going through the authoritative DNS hierarchy.

![Authoritative DNS Hierarchy Pic](https://s3-us-west-1.amazonaws.com/umbrella-blog-uploads/wp-content/uploads/2014/07/Screen-Shot-2014-07-16-at-10.56.09-AM.png)

<sup>
(3) Root domain nameservers know the IP addresses of Top Level Domains (TLD) like “.com”, “.edu” or “.gov”.<br>
(4) Authoritative server for “.com” knows where it can find “google.com”.<br>
(5) Then “google.com” is asked where to find “www.google.com”.<br>
</sup>

Assuming the DNS lookup is successful, the client obtains an IP address that uniquely identifies another machine on the Internet.

#### NOTE:

A client can retrieve a resource using an IP directly. Because some websites have multiple servers in multiple locations to support millions of requests simultaneously, by using a URL we let the host decide which IP our client should connect to. This helps prevent bottlenecks, improves scalability, response speed and user experience overall.

![Load balancer pic](http://tutorials.jenkov.com/images/software-architecture/load-balancing-1.png)

<sub>A **load-balancer** for example, is a piece of hardware that listens on a particular IP address and forwards the requests to other servers. Major sites will typically use load balancers to process a higher work load.</sub>

### Initiate TCP IP connection
----

Communication between networked computers is carried out using protocol suits. The most widely used and most widely available protocol suite is the TCP/IP. It provides end-to-end connectivity specifing _how data should be packed, addressed, trasmitted, routed and received_ at the destination. TCP/IP is considered to be a 4 layer system. 

![TCP/IP concept pic](https://cdn.tutsplus.com/net/uploads/2013/07/img004.png)

<sup>
    **Application Layer** includes applications or processes that use transport layer protocols to deliver the data<br>
    **Transport Layer** utilizes various protocols to facilitate data flow between two hosts<br>
    **Network Layer** organizes and handles the movement of data on a network<br>
    **Data Link Layer** consists of drivers on the OS and a network interface which handle communication details
</sup>

For the purposes of this blog, the most important thing to mention is that once a client recieves an IP address, the following step is opening of a **"network socket"** so that a client and server can communicate.

> A socket is one endpoint of a two-way communication link between two programs running on the network. A socket is bound to a port number so that the TCP layer can identify the application that data is destined to be sent to.

#### NOTE on transport layer:

Two most commonly used protocols at transport layer are TCP and UDP.

* **TCP is used where a reliable connection is required.** For example while downloading a file, it is not desired to loose any information.
* **UDP is used in case of unreliable connections.** For example while streaming a video, loss of a few bytes is acceptable.


### Client HTTP request
----

Once a client successfuly initiates a TCP connection with the server, it prepares an HTTP request according to the specification of the HTTP protocol to be sent to the host.

Various information is included in the form of headers.

<p class="http-requests">
    GET http://google.com/ HTTP/1.1<br>
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8<br>
    User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:29.0) Gecko/20100101 Firefox/29.0<br>
    Accept-Encoding: gzip, deflate<br>
    Connection: Keep-Alive<br>
    Host: google.com<br>
    Cookie: datr=1265876274-[...]; locale=en_US; lsd=WW[...]; c_user=2101[...]
</p>

* **Initial Request Line**
* **Accept-Encoding** headers specify the type of responses it will accept
* **User-Agent** header specifies the browser properties
* **Connection** header tells the server to keep open the TCP connection
* **Host** URL
* **Cookies** may be included

An HTTP request is sent out in packets. Similar to how a DNS query was performed earlier. The packets are sequenced so that they can be reassembled once they reach the destination even if they arrive out of order.

### Server Processes Payload
----

Once the request payload arrives at the destination, a web server application processes the request by launching a proper **request handler**. _A request handler is a program (written in PHP, Ruby, Java, Python) that reads the request, its parameters, and cookies_. The handler may interact with a database updating some stored records.

![HTTP Request Diagram pic](https://i0.wp.com/www.dotnetfunda.com/UserFiles/ArticlesFiles/Abhijit%20Jana_634041501029987812_IISProcessRequest.JPG)

The handler will then generate a response which will be sent back to the client. This may be a static page or a dynamic response, generated in a number of different ways.

### Server HTTP Response
----

<p class="http-requests">
    HTTP/1.1 200 OK<br>
    Cache-Control: private, no-store, no-cache, must-revalidate, post-check=0, pre-check=0<br>
    Expires: Thu, 19 Nov 1981 08:52:00 GMT<br>
    Pragma: no-cache<br>
    Content-Encoding: gzip<br>
    Content-Type: text/html; charset=utf-8<br>
    Connection: Keep-Alive<br>
    Content-length: 1215<br>
    Date: Fri, 30 May 2014 08:10:15 GMT<br>
    <br>
    .........[some blob]................
</p>

An HTTP response header is similar to that of the request. It includes information that gives a client metadata in order to process that response.

* **HTTP Version and Status Code**
* **Content Type** specified as MIME type
* **Content Encoding**
* **Content Length**
* **Server info**
* **Date Info**
* **Cache Directives**
* **Cookie Info**
* and more...

### Client Renders Document
----

Using the metadata a browser parses the response to render the web page. The browser may make more requests, using the same procedures outlined above. This is done to fetch any new resource that are found as embedded content. Typically media, style sheets, javascript files.

A DOM tree is built out of broken HTML. Style sheets and javascript files are parsed and DOM nodes are moved and styled to match the directives of aforemantioned files.

Finally, the browser renders the page on the screen accroding to the DOM tree and the style information of each node.

![Content Rendering Pic](http://taligarsiel.com/Projects/image008.jpg)

#### NOTE:

AJAX requests may be made to communicate with the web server even after the page is rendered.

## Conclusion
----

Thinking about the series of events that take place when a URL is entered into an address bar is invigorating. Such a simple step, in the background, triggers an extremely large number of procedures which are layered in an equally large number of abstractions.

Writing this blog post has given me the opportunity to look deeper into the processes that are involved in web applications and networking. I hope that next time I am faced with a question posed earlier, I will be better prepared to give a more through and complete answer.



## SOURCES

1. [URL - Wikipedia](https://en.wikipedia.org/wiki/Uniform_Resource_Locator)
2. [Host Name Resolution](https://technet.microsoft.com/en-us/library/cc958812.aspx)
3. [Difference between Authoritative and Recursive DNS](https://blog.opendns.com/2014/07/16/difference-authoritative-recursive-dns-nameservers/)
4. [TCP/IP Protocol Fundamentals](http://www.thegeekstuff.com/2011/11/tcp-ip-fundamentals/)
5. [A brief overview of TCP/IP communications](http://www.taltech.com/datacollection/articles/a_brief_overview_of_tcp_ip_communications)
6. [What Is a Socket?](https://docs.oracle.com/javase/tutorial/networking/sockets/definition.html)
7. [Quore Related Question](https://www.quora.com/What-are-the-series-of-steps-that-happen-when-an-URL-is-requested-from-the-address-field-of-a-browser)
8. [What really happens when you navigate to a URL](http://igoro.com/archive/what-really-happens-when-you-navigate-to-a-url/)
9. [What happens when you type a URL in browser](http://edusagar.com/articles/view/70/What-happens-when-you-type-a-URL-in-browser)
10. [HTTP Succinctly](http://code.tutsplus.com/series/http-succinctly--net-33683)