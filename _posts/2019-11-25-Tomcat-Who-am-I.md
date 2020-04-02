---
layout: post
title: "Tomcat\_: Who I am and What I do"
categories: [Notes]
tags: [Server]
---

It has been little over an year since I started my career with a software Job. As it is with most software jobs there are things that you can only learn and understand when you get your hands dirty. So in the past one year as a junior developer I got a chance to work with various technologies about which I had no clue of. I will try to share my understanding about these technologies/ topics through these posts so that they don’t go undocumented.

![Photo by [Mikhail Vasilyev](https://unsplash.com/@miklevasilyev?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/800/0*tIfitQgbitKSKybE)
Photo by [Mikhail Vasilyev](https://unsplash.com/@miklevasilyev?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

### **My first Encounter**

As with any developer even before you start writing code for your project, it is required that you get your local set up done. It is during one such endeavor that I observed that we were using one peculiar piece of software, on which we ran almost all of our Java based web applications. It was Apache Tomcat. In the beginning I thought that it was a Application server. But I was wrong.

### **Tomcat an Application Server?**

No, Tomcat is not a full fledged application server, though we can do more than just deliver static content using Tomcat, but it doesn’t meet all the requirements of J2EE compliant application server. For instance Tomcat doesn’t support J2EE EJB specification. So currently consider it to be a beefed up version of a Web server or a Servlet Container.  
The following table shows the support Tomcat provides out of the Box.

![Supported Specifications](https://cdn-images-1.medium.com/max/800/1*i-1Tu3ZABlYg4A4FYcl9Fw.png)
Supported Specifications

<div class="message">
<b>As mentioned in Oracle’s Docs</b>  
<p>A Java EE application server, also known as a Java EE container, is any server that is **fully compliant** with the J2EE or Java EE platforms. Unlike a regular web server, an application server can run full enterprise applications, EJB modules, and web services. It can also manage transactions of persistent entity objects and communicate with databases.</p>
</div>

But to know how we our Java applications actually run on Tomcat, it is important that we have an understanding about it’s architecture.

### **Tomcat and it’s Architecture**

Tomcat is developed and maintained by an open community of developers under the belt of the Apache Software Foundation, released under the Apache License 2.0 license.

<div class="message">
<b>As mentioned in Apache’s website</b>  
<p>The Apache Tomcat software is an open source implementation of the Java Servlet, JavaServer Pages, Java Expression Language and Java WebSocket technologies. It is often categorized as a web Server. Out of all the implementations this post focusses on Catalina which implements Java specifications for servlet and JavaServer Pages (JSP).</p>
</div>

Tomcat contains multiple components. But whenever we refer to Tomcat server, we refer to all the components as a whole. _Jasper, Cayote, Catalina_ are some of the main components. But the core component of Tomcat that we are concerned about is the Catalina component which is a Servlet container as it implements Java specification for Servlet API. Whenever we say that we have started our Tomcat it means we have actually started the Catalina instance.

![Components of Tomcat Server](https://cdn-images-1.medium.com/max/800/1*gjsyH_NXpQ7qG3HVEmZ4pA.png)
Components of Tomcat Server

#### **Catalina as a Servlet Container**

One of the key requirements worked into the Servlet specification is that they only are expected to handle certain parts of the total data transaction process. For example, the servlet code itself will never listen for requests on a certain port, nor will it communicate directly with a client, nor is it responsible for managing its access to resources. Rather, these things are managed by Tomcat, the servlet container.

1.  Whenever we try to deploy our java application to Tomcat, it searches for the Deployment Descriptor(Web.xml) file which contains information about URL and servlet mappings.
2.  Based on the configuration in deployment descriptor file, Tomcat can load/ initialize the servlet classes on startup or as a response to a request.
3.  When Tomcat receives a request, it decides on which servlet should handle the request.
4.  Once the request has been mapped to the appropriate servlet, Tomcat checks to see if that servlet class has been loaded. If it has not, Tomcat compiles the servlet into Java bytecode, which is executable by the JVM, and creates an instance of the servlet.
5.  Tomcat invokes the service method of the servlet, to handle client’s request.

Apart from _web.xml_ we must remember that there is one more configuration file i.e_. server.xml,_ which has the details regarding what components need to be included in the server, their configuration like what ports to open, how to interconnect them and how to boot up the tomcat instance.

#### Coyote as a Connector

But aren’t we forgetting something in the first place? Catalina by itself is just a servlet container How does Tomcat even receive the client request? This is facilitated by Tomcat’s connector component — Coyote.

<div class="message">
<b>As mentioned in Apache’s website</b>  
<p>The Coyote HTTP/1.1 Connector element represents a Connector component that supports the HTTP/1.1 protocol. It enables Catalina to function as a stand-alone web server, in addition to its ability to execute servlets and JSP pages. A particular instance of this component listens for connections on a specific TCP port number on the server. One or more such Connectors can be configured as part of a single service.</p>
</div>

Understanding the underlying architecture of Tomcat helps us understand why it can do more than just serve static content.

### **Why Tomcat?**

There are few options an enterprise can choose for their java server solution.  
**web servers:** Jetty, Tomcat**application servers:** Glassfish, WebSphere, WildFly.  
Even though Tomcat doesn’t provide all the features of an application server like IBM’s WebSphere, it has become the most popular choice for Java application deployments. Mostly due to:

1.  It is Lightweight, with short load and redeploy times
2.  Open source software which has been around for a long time
3.  Tomcat is free, compared to high cost associated with some of the other popular application server solutions
4.  Even for the features that Tomcat doesn’t come with we can include them as external dependencies.
5.  Tomcat is very flexible and extendable — scaling to Enterprise support via TomEE, JBoss, WildFly is possible.
6.  It can be easily integrated with different Java frameworks like Spring.

### **References**

[Deployment Descriptors](https://cloud.google.com/appengine/docs/standard/java/config/webxml)

[Catalina Component of Tomca](https://www.mulesoft.com/tcat/tomcat-catalina)t

[Web Servers and Application Servers](https://howtodoinjava.com/tomcat/a-birds-eye-view-on-how-web-servers-work/)

[J2EE specifications supported by Tomcat](https://tomcat.apache.org/whichversion.html)

[Web Server with Application Server](https://www.theserverside.com/feature/Understanding-How-the-Application-Servers-Web-Container-Works)

[Thread on Tomcat configuration files server.xml vs Web.xml](https://coderanch.com/t/612586/application-servers/Difference-server-xml-context-xml)

[Tomcat Architecture and Directory structure](https://www.ntu.edu.sg/home/ehchua/programming/howto/Tomcat_More.html)