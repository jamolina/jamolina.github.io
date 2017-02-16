---
layout:     post
title:      "OWASP Top 10 Part 1 - SQL Injection"
date:       2017-02-06 22:00:00
comments:   true
header-img: "img/owasp-1-1.jpg"
header-img-author: "Blue Coat Photos"
header-img-url: "https://flic.kr/p/qfWcPy" 
tags: [owasp, security]
---

This is the first in a series of post related to OWASP Top 10 Web Application Security Risks. 

These are mostly my notes on [Troy Hunt's](https://www.troyhunt.com/) Pluralsight course: [OWASP Top 10 Web Application Security Risks for ASP.NET](https://app.pluralsight.com/library/courses/owasp-top10-aspdotnet-application-security-risks/table-of-contents)

Now, the #1 vulnerability ([from 2013 data](https://www.owasp.org/index.php/Top_10_2013-A1-Injection)) is Injection. I still remember being burned by this one when I developed a small library management web application for a school library back when I was in college (I would like to say I know better nowadays). [OWASP defines Injection](https://www.owasp.org/index.php/Top_10_2013-Top_10) as:

> Injection flaws, such as SQL, OS, and LDAP injection occur when untrusted data is sent to an interpreter as part of a command or query. The attacker’s hostile data can trick the interpreter into executing unintended commands or accessing data without proper authorization.

Some of the key points from Troy's course on this subject:

* If a site is vulnerable to SQL Injection, an URL like ___mysite.com/page?id=1___ translates to `SELECT * FROM TABLE WHERE ID = 1`

* The first part of the query is trusted (`SELECT * FROM TABLE WHERE ID =`), the querystring (`1`) is untrusted data

* You can try to manipulate the querystring with additional conditions such as "`or 1=1`" to check for vulnerability (for example, a page that is suppossed to filter by a category ID would return every product regardless of its category)

* Check what happens if you send a STRING to a parameter that expects an INT, this might expose errors that give you more data on the DB structure (assuming you are showing errors to the user, which is another topic by itself)

* We can construct queries that will allow us to get table and columns information

Here are some of the things you can do to protect against Injection:

* We must assume that unstrusted data could be malicious

* Untrusted data can come from a wide range of sources:
    
    * From the user (querystring, forms)

    * From the browser (cookies, request headers)

    * From external services

    * Even your own database (user saved data)

* Protect by layers, so each layer has a backup

* Principle of least privilege. Every module can only access the necessary resources it absolutely needs to perform its function

* Query parameterization helps you prevent strings breaking out of the query context

* Stored procedures use a similar idea and are naturally parameterized

* Blacklist is a list of know dangerous values (which is limited to what you know now, so it is not as future-proof)

* Whitelist is an explicit list of valid values that we allow

    * Approaches to whitelisting: type conversion (cast before you query), regular expressions, list of known good values

    * Need to be careful on not limiting valid values

* ORMs can help you mitigate sql injection by automating parameterization

* SPs are not a silver bullet, they can still be exploited

* There are tools like Havij or sqlmap.org that help to find SQL Injections exploits in a very easy way