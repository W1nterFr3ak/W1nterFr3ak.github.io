---
title: "Tryhackme — Wgel: Easy"
date: 2022-6-04 12:30:00 +0530
categories: [Tryhackme,Linux Machines]
tags: [tryhackme, sudo, wget, web, python]
image: /assets/img/Posts/wgel.png
---

> Wgel is an intresting easy box that shows how we can make use of wget  which is allowed to run as superuser by `sudo`, it does not drop the elevated privileges and may be used to access the file system, escalate or maintain privileged access.

## Nmap scan
We start our journey by scanning the host for open ports
```shell
➜  wgel nmap -sCV -oN nmap/wgel-scan 10.10.154.44
Starting Nmap 7.92 ( https://nmap.org ) at 2022-06-04 17:26 EAT
Nmap scan report for 10.10.154.44
Host is up (0.22s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 94:96:1b:66:80:1b:76:48:68:2d:14:b5:9a:01:aa:aa (RSA)
|   256 18:f7:10:cc:5f:40:f6:cf:92:f8:69:16:e2:48:f4:38 (ECDSA)
|_  256 b9:0b:97:2e:45:9b:f3:2a:4b:11:c7:83:10:33:e0:ce (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.18 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 45.86 seconds


```
Port Scan Summary :
- port 80    htpp
- port 22    ssh


## Port 80
Port 80 is the **port number assigned to commonly used internet communication protocol, Hypertext Transfer Protocol (HTTP)**. It is the default network port used to send and receive unencrypted web pages.
Browsing to the website we find an apache landing page.
### View Source Code
![](/assets/img/Posts/wget-img/source.png)

Viewing the source code we find a message left for user Jessie to update the website. From this we can note down that there is a user jessie who has permisions to modify the website and we assume its via ssh. 

### Fuzzing
Finding nothind else in the source we proceed to fuzzing for  hidden directories and files.

![](Pasted image 20220604190227.png)
We find a directory sitemap, navigating to it we get a  unap template which had nothing of intrest so we can procede to fuzz the sitemap path for any hidden files or directories

### Fuzzing sitemap
![[Pasted image 20220604184143.png]]
We get a .ssh directory which contained jessie's id_rsa private key which we can use to get our initial foothold.

## Initial Foothold
Using the id_rsa we ssh into the box and get our first flag in the Documents directory

![[Pasted image 20220604184923.png]]

### Privilage Escalation
Checking for programs that can be executed as sudo without a password we find wget.
![[Pasted image 20220604185041.png]]
From this we can download the passwd and shadow file offline for cracking.

![[Pasted image 20220604191116.png]]
Downloading the shadow file we find that the root user had no password set. This changes our plan from cracking to modifying the shadow file then reuploading to the box.

First we create a unix password hash using pythons crypt module then we add it to the shadow file we create on our machine.
![[Pasted image 20220604192038.png]]
![[Pasted image 20220604192302.png]]

We then start up an http server using python then proceed to download it on the target machine taking advantage of wget which we can run as root without a password to overwrite the shadow file with our own.
![[Pasted image 20220604192937.png]]
Now we can switch to the root user using our modified password.
![[Pasted image 20220604193141.png]]

###### FIN
Thats it for Wgel 
