---
author: klauer
comments: true
date: 2012-03-15 16:06:26+00:00
layout: post
slug: dropwizard-simple-self-contained-restful-web-services-in-java-httpdropwizard-codahale-com
title: 'Dropwizard: simple, self-contained RESTful web services in Java'
wordpress_id: 67
---

I’ve been meaning to dig into this before, but I had some time to recently and I’m really impressed with the setup and had to share. Dropwizard is a framework for building RESTful web services in Java backed with JSON. I’m not sure for the rest of the teams, but I can speak to EMO in saying that many of their choices in libraries mirror our own or do one better:



	
  * Jersey for REST

	
  * Jackson for JSON processing

	
  * Jetty for in-app deployment (it can compile to a .jar that you could just run simply by typing **java –jar app.java config.yml**)

	
  * log4j for logging

	
  * [jdbi](http://www.jdbi.org/) for database integration (this alone is worth looking at [http://www.jdbi.org/](http://www.jdbi.org/))


In addition to these, it has a really nice [Getting Started](http://dropwizard.codahale.com/getting-started/) guide that you might find fun. I was able to walk through the whole thing in an hour (including distractions, running Eclipse, Maven, etc) and have a runnable app. I’m definitely going to consider this when I need a REST service in the future.

In looking at how this framework behaves, it’s really a sprinkling of glue code and some special magic from Yammer to make development of these services a lot less painful. I found that it took what I was already doing, and added a few more helpers and concepts such as [ health checks](http://dropwizard.codahale.com/manual/core/#health-checks) (which are really awesome) that make this something I would look to for development without fuss.

If you’re interested, check out the links, GitHub site, and examples:



	
  * [Dropwizard](http://dropwizard.codahale.com/) – [ http://dropwizard.codahale.com/](http://dropwizard.codahale.com/)

	
  * [GitHub source](https://github.com/codahale/dropwizard) – [https://github.com/codahale/dropwizard](https://github.com/codahale/dropwizard)

	
  * [Example project](https://github.com/codahale/dropwizard/tree/master/dropwizard-example) – [ https://github.com/codahale/dropwizard/tree/master/dropwizard-example](https://github.com/codahale/dropwizard/tree/master/dropwizard-example)


I’m really impressed with how this is laid out, and their choices for other modules (such as using the jbdi project for database) is slick.

Addendum:

The team at [Simple](http://www.simple.com) ([http://www.simple.com](http://www.simple.com)) have been using it for their services, and one of the team [presented at BashoChats explaining their use of it](http://vimeo.com/37930578).
