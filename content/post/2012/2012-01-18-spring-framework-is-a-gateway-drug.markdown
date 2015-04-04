---
author: klauer
comments: true
date: 2012-01-18 08:46:00+00:00
layout: post
published: false
slug: spring-framework-is-a-gateway-drug
title: Spring Framework is a Gateway Drug
wordpress_id: 4
---


    

I was going to mention about my previous post why I didn't pick [Spring DI](http://www.springsource.org/features) over [Guice](http://code.google.com/p/google-guice/).  It's not that I dont' think Spring is a good choice, but I believe that Spring is a gateway drug to evil things...







Spring DI by itself was a lifesaver for the Java EE developer, as it made your code mostly just Beans and POJO's.  This is great, and it's what attracted me to it.  However, after it's initial success, it expanded into a plethora of tools and frameworks, even going so far as to [make it's own IDE](http://www.springsource.org/downloads/sts), acquire the Groovy and Grails teams, and be bought out by VMWare in turn.  It now encompasses a [plethora of domains](http://www.springsource.org/documentation), and has an end-to-end stack for deploying to the cloud, mobile, web, security, and just-about-anythign-you-can-think-of.  I believe this has turned it into the monster it was created to slay (Java EE), by being a modular, bloated framework.  It's only slightly more modular than Java EE.  I don't quite understand how it can have such a huge collection of disparate tools and not be considered bloated.







What always ends up happening in architecture designs is that when you bring Spring in to handle your DI, you start to think, "well, now that Spring is the DI tool, I guess I could use Spring JDBC for the database calls," so you add a little more.  Then, when you want to do a Mailer, you think, "does Spring have a mailer?", and lo-and behold, it does!  Next, you may have to handle some user authentication or whatnot, and think, "...Spring?", yeah, it does that, too.







This isn't a problem if you like Spring, but it tends to be either "trivially easy" to do in Spring, or makes comparisons against other tools more difficult.  "Why choose anything other than Spring JDBC?  I mean, it's a Spring app, so why bother?" end up being the argument.  Who knows, maybe the other library is better by a mile, or even just marginally better, but because you've already chosen Spring to start your framework, you're basically going to roll around in the thing until you're completely covered in Spring mud.







It's much like that oft-repeated quote:







<blockquote>XML is like violence; if it doesn't solve your problem, you're not using enough of it.</blockquote>







Spring is like that.  It makes choosing a good toolset harder, as it ends up making the burden of proof on whether the thing you want to use is **better** than Spring's offering, versus just trying to find a good tool to do the job.







I may use Spring in other jobs, but I find that it limits you to their way of configuring things, and doesn't have the fun of some of the simpler tools like the Java [Spark](http://www.sparkjava.com/) framework, or [Date4J](http://www.date4j.net/).  It's become the enterprise monster it was sent out to defeat.  "Power corrupts: absolute power corrupts absolutely".  Don't let Spring into an app that doesn't have it unless you're prepared to fight over every minor thing that Spring "can do for you"...


  
