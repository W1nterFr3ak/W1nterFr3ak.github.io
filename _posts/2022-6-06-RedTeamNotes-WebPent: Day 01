---
title: "Notes — Web Pentest : Day 001"
date: 2022-08-22 22:20:00 +0530
categories: [Red Team Notes,Web, HTB Accademy]
tags: [Web, Basics]
image: /assets/img/Posts/RedNotes/web100/HTTP-arch.jpg 
---

# Overview
>This is the first part of my 100 day of web hacking journey, beginner to hacker
> Day 1 i decided to focus on Web Technology, Architecture and protocol

# Architecture 
The web application architectures is made up 2 parts :
- **Client** : This is medium making requests to the server and in most cases its the browser
- **Server** : Will receive request from the client and either process it as per the programmers instrustion or in most cases another server/application does the processing of the request in such cases the servers role is to foward the request to the application server(ie a databse application).


# Technologies
### Client Side Technologies
Technologies on the client include html, javascript css etc which are used on day to day basis, also the technologies can me a script. 
Client side technologies include tools that the client interacts with or uses to interact with a web service/application.

### Server Side Technologies
On the server side a lot of technologies can be used and even if all may be vulnerable to any web issue, some issues are more likely to happen for a given technology.

The server side can be divided into more sub-categories:

-   Web servers like Apache, lighttpd, Nginx, IIS...
-   Application servers like Tomcat, Jboss, Oracle Application server...
-   The programming language used: PHP, Java, Ruby, Python, ASP, C#, ... This programming language can also be used as part of a framework like Ruby-on-Rails, .Net MVC, Django.

### Storage backend

The storage backend can be located on the same server as the web server or on a different one. This can explain weird behaviour during the exploitation of some vulnerabilities.

A few examples of backends are:

-   Simple files.
-   Relational databases like Mysql, Oracle, SQL Server, PostgreSQL.
-   Other databases like MongoDB, CouchDB.
-   Directories like openLDAP or Active Directory.

An application can use more than one storage backend. For example, some applications use LDAP to store users and their credentials and use Oracle to store information.

# Protocols
## HTTP
Now that we know that a client talks(requests) to a server, the question how emerges. Thats where HTTP comes in,http is an application-level protocol used for communicate between the client and a web server. 
The client (ie browser) sends a request to the server, and then the server responds to this request. 

HTTP stands for *HyperText Transfer Protocol*, from the name we see that its a text protocol meaning the communication is in human readable form hence anybody actively monitoring the communication can view the data being sent.
By default, most web servers are available on port TCP/80. When your browser connects to a URL: http://google.com, it's in fact doing a TCP connection to the port 80 of the IP corresponding to the name google.com.


## **HTTPS - HTTP over SSL**

HTTPs is just HTTP done on top of a Secure Socket Layer (SSL). The SSL part ensures the client that:

-   He's talking to the right server: authentication;
-   The communication is secure: encryption.

Using HTTPS, the computers agree on a "code" between them, and then they scramble the messages using that "code" so that no one in between can read them. This keeps your information safe from hackers.

Multiple versions of SSL exist with some of them considered weak (SSLv1 and SSLv2).

SSL can also be used to ensure the client's identity. Client certificates can be used to ensure that only people with valid certificates can connect to the server and send requests. This is a great way to limit access to a service, and is often used for systems requiring a high security level (payment gateway, sensitive web service). However, maintaining certificates (and revocation lists) can be a pain for large deployments.

Woops Thats It for Day 001 .... See you tomorrow 