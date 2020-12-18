---
layout: post
title: "Introduction to OWASP"
date: 20-12-18
author: s
categories: owasp_introduction
tags: security owasp vulnerabilities
cover: "/assets/wolf1.png"
---

Hello readers ,
After reading this article you will be able to:

- Learn the concepts of web application security
- Why should I be concerned about it ?
- what is OWASP ?
- What are the OWASP TOP TEN ?

## What is web application security ?

It is the process of protecting website , online services ,api's etc.. against the different security threats that can be the root cause of out vulnerabilities in our web applications.

## Why should I be concerned about it? What harm can it cause to me ?

Imaging your business is going very well, and suddenly your database is compramised and the information got deleted or the data is leaked and you are losing all your clients. Do you like that ? No one would . The main cause of that exploit is because of the poor implementation of security practises in your applications code. There are many vulnerabilities that are discovered every month and some are already handled by the application's framework, but a small bug in our code can ruin our entire business. Here's a solution for that. Do you know about OWASP and their famous project OWASP TOP TEN ? Let me explain

## What is OWASP ?

OWASP stands for Open Web Application Security Project.

From the owasp official site ,it states

> The Open Web Application Security Project® >(OWASP) is a nonprofit foundation that works >to improve the security of software. Through >community-led open source software projects, >hundreds of local chapters worldwide, tens >of thousands of members, and leading >educational and training conferences, the >OWASP Foundation is the source for >developers and technologists to secure the >web.
>
> Tools and Resources <br>
> Community and Networking <br>
> Education & Training

So basically is an online community with tens of thousands of contributors that produces articles , tools , methodologies and best practices in the field of web application security.
And coming to OWSAP TOP TEN , It is the list of top ten most common application vulnerablities. They are updated every three to four year. Lets dive deeper into owasp top ten

## OWASP TOP TEN

From their official site ,

> The OWASP Top 10 is a standard awareness document for developers and web application security. It >represents a broad consensus about the most critical security risks to web applications.
>
> Globally recognized by developers as the first step towards more secure coding.
>
> Companies should adopt this document and start the process of ensuring that their web applications >minimize these risks. Using the OWASP Top 10 is perhaps the most effective first step towards >changing the software development culture within your organization into one that produces more >secure code.

Sounds Interesting , isnt it ? Lets explore each of the top 10.
The top ten vulnerabilities as of 20020 are :

- Injection
- Broken Authentication.
- Sensitive Data Exposure
- XML External Entities (XXE)
- Broken Access Control
- Security Misconfiguration
- Cross-Site Scripting (XSS)
- Insecure Deserialization
- Using Components with Known Vulnerabilities
- Insufficient Logging & Monitoring

These are the top ten web application security risks. There may ne some of them that you already know of and some of them you dont have any idea about. Dont worry. We'll be discussing each of them in depth with certain examples and pictures so it makes perfect sense why we should immediately be redesigning our application addressing these security concerns.
