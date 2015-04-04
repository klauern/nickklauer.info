---
author: klauer
comments: true
date: 2012-01-18 08:35:00+00:00
layout: post
slug: java-batch-cli-template
title: Java Batch CLI Template
wordpress_id: 5
---

At work, there have been a couple times that I needed to throw together the equivalent of a batch processing job or one-off command-line application to process some data quick and dirty.  My platform that I have to develop on has it's own Java API, so I lean on using a Java framework or toolset to get this work done.  This ends up simplifying the end-to-end migration of source data --> destination data.




Because of these various projects, I've grown to like a few Java libraries that make working with the language a little less verbose or clunkyWith that, I decided to take these common pieces and make a template applicatino out of it.





Presenting [java-batch-command-line](https://github.com/klauern/java-batch-command-line)





I like my names to be self-explanatory, because there's just too many weird names out there for me to try to remember what they did (hello RubyGem maintainers!).





What is this?





As work is mostly Maven at this point, I decided to stick to it for my command-line apps.  I would love to start digging into Gradle and converting this over to one, but I haven't had the time (on my to-do list, though).





Libraries I've included and stubbed some pieces out:








	
  * [Maven](http://maven.apache.org) (including [AppAssembler](http://mojo.codehaus.org/appassembler/appassembler-maven-plugin/) configuration)

	
  * [JCommander](http://jcommander.org) (it's the best command-line option parsing lib I've found on Java so far)

	
  * [Logback](http://logback.qos.ch) (because log4j was so last year...and the maintainer of log4j made this library telling everyone to move to this)

	
  * Google's goodies ([Guava ](http://code.google.com/p/guava-libraries/)and [Guice](http://code.google.com/p/google-guice/), both excellent in my opinion)




What does this framework give you that you can't do yourself?  I will admit, probably not much.  However, I have had to reinvent the wheel on this a couple times just because I like these tools better than others, so it saves me some time.  It includes in it:












	
  * Maven POM

	
    * defining the dependencies above,

	
    * including [AppAssembler](http://mojo.codehaus.org/appassembler/appassembler-maven-plugin/) for building a standalone command-line app

	
    * pre-defined resource filtering




	
  * Eclipse Project files

	
  * Google Guice stubs for DI management

	
  * CommandLineOpts with default command-line parsing

	
  * [Logback.xml configuration](http://logback.qos.ch/manual/configuration.html) file for logging




This basically saves me an hour or random digging I have had to do in the past, so it's worthwhile to me.  I might go into the libraries in the future, but they are all great tools in my opinion, and I think if you're a Java developer, you probably know about them at least in passing.










[GitHub : java-batch-command-line](https://github.com/klauern/java-batch-command-line)
