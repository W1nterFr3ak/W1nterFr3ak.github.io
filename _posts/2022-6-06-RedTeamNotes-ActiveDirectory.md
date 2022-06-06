---
title: "Notes — Active Directory"
date: 2022-06-06 12:30:00 +0530
categories: [Red Team Notes]
tags: [Active Directory, Basics]
image: /assets/img/Posts/RedNotes/ADbasics/AD.jpg 
---

# Overview
>Active Directory (AD) is a database and set of services that connect users with the network resources they need to get their work done.It allows network administrators to create and manage domains, users, and objects within a network hence creating a centralized user and rights management, as well as centralized control over computer and user configurations.
>It  contains critical information about your environment, including what users and computers there are and who’s allowed to do what. For example, the database might list 100 user accounts with details like each person’s job title, phone number and password. It will also record their permissions.

# Structure 
The Active Directory structure includes three main tiers:  Domain, Tree and Forest
- **Domain** – The objects of the directory are contained inside the domain. Inside a "forest" more than one domain can exist and each of them will have their own objects collection.
- **Tree** – Group of domains with the same root. Example: _dom.local, email.dom.local, www.dom.local_
- **Forest** – The forest is the highest level of the organization hierarchy and is composed by a group of trees. The trees are connected by trust relationships.

##### Other Important terms
- **Directory**– Contains all the information about the objects of the Active directory
- **Object**– An object references almost anything inside the directory (a user, group, shared folder...)

Basically several objects that use the same database can be grouped to a single domain. Multiple domains can be grouped to form a tree. And finally multiple trees can be grouped to form a forest.
A domain is a management boundary, meaning, the objects for a given domain are stored in a single database and can be managed together, whereas  a forest is a security boundary meaning  objects in different forests are not able to interact with each other unless the administrators of each forest creates a trust between them. For instance, if you have multiple disjointed business units, you probably want to create multiple forests.

## Active Directory Domain Services (AD DS)
The main Active Directory service is Active Directory Domain Services (AD DS), which is part of the [Windows Server operating system](https://www.quest.com/solutions/windows-server/). These services include:
- **Domain Services** – stores centralized data and manages communication between users and domains; includes login authentication and search functionality
- **Certificate Services** – creates, distributes, and manages secure certificates
- **Lightweight Directory Services** – supports directory-enabled applications using the open (LDAP) protocol
- **Directory Federation Services** – provides single-sign-on (SSO) to authenticate a user in multiple web applications in a single session
- **Rights Management** – protects copyrighted information by preventing unauthorized use and distribution of digital content
- **DNS Service** – Used to resolve domain names.

# How does Active Directory work?

The servers that run AD DS are called domain controllers (DCs). Organizations normally have multiple DCs, and each one has a copy of the directory for the entire domain. Changes made to the directory on one domain controller — such as password update or the deletion of a user account — are replicated to the other DCs so they all stay up to date. A Global Catalog server is a DC that stores a complete copy of all objects in the directory of its domain and a partial copy of all objects of all other domains in the forest; this enables users and applications to find objects in any domain of their forest. Desktops, laptops and other devices running Windows (rather than Windows Server) can be part of an Active Directory environment but they do not run AD DS. AD DS relies on several established protocols and standards, including LDAP (Lightweight Directory Access Protocol), Kerberos and DNS (Domain Name System).

It’s important to understand that Active Directory is only for on-premises Microsoft environments. Microsoft environments in the cloud use Azure Active Directory, which serves the same purposes as its on-prem namesake. AD and Azure AD are separate but can work together to some degree if your organization has both on-premises and cloud IT environments (a hybrid deployment).

##### Fin
Thats it for Active directory Basics, see you in the next post.