---
author: klauer
comments: true
date: 2012-04-26 04:15:27+00:00
layout: post
slug: future-of-browser-development
title: Future of Browser Development
wordpress_id: 78
---

So I was thinking about how Javascript is the _new_ hot thing to develop on, with languages like [Coffeescript](http://coffeescript.org) to make it more palatable, and I wonder how long it'll last before the dev community says 'fuck this stupid shit' and move on? I think it's already happening.  There are a couple things that triggered this.  
  
1. [Coffeescript](http://coffeescript.org)  
  
People didn't like Javascript (or at least got tired of it's warts), so they tried to make a Ruby-like language that 'compiles' to Javascript.  In this case, you write Coffeescript and convert it to Javascript.  In most cases, you don't have to pay much attention to he Javascript you create, and things more-or-less work. This is cool, but the tooling isn't there yet.  I have a feeling it'll come along as extensions to browsers start to add Coffeescript bindings or ways to map your app to the Javascript it generated better (and Chrome is already starting down that path with [source maps](http://www.coffeescriptlove.com/2012/04/source-maps-for-coffeescript.html), so it might come sooner than later).  
  
2. [Sencha](http://sencha.com)  
  
[Sencha](http://www.sencha.com) is the company behind [ExtJS](http://www.sencha.com/products/extjs/), which is a Javascript toolkit for building Rich UI apps.  ExtJS is a great framework itself, as it wraps up alot of nice, rich UI elements in simple Javascript widgets, with a framework to put them together.  Building on this base, Sencha has been on a roll recently, with their [Sencha Touch](http://www.sencha.com/products/touch) toolkit that gives users a UI kit for mobile apps that look like native apps, and now further with things like Ext Designer (now [Sencha Architect](http://www.sencha.com/products/architect)), which gives you a drag-and-drop interface to building your rich interface.  
  
More recently, Sencha came out with [Sencha Animator](http://www.sencha.com/products/animator/), which to me looks like something Adobe would have written up to create rich Flash applications.  All the while, these tools are just leveraging HTML5+JS+CSS3+ and working pretty seamlessly.  I think it's only a matter of time that people would be experts in these tools with little to no knowledge of the underlying components.  Why not?  
  
3. [ClojureScript](https://github.com/clojure/clojurescript)  
  
So the Clojure community came up with the idea that they could map their language to the [Google Closure compiler](https://developers.google.com/closure/) and provide their community a way to write Clojure on the browser.  Again, this would compile to Javascript.  There are some pretty neat things going on with the Clojure community, too, like the [ClojureScript One](http://clojurescriptone.com/) project and [Light Table](http://www.kickstarter.com/projects/ibdknox/light-table), that provide a development environment for you in the browser.  All of which makes me think Clojure stands a chance of really shining in the years to come on the browser.  
  
All of these things are neat by themselves, but taken together, you can begin to see that while we might not see browsers supporting other languages than Javascript, the developer/language communities are not going to take that sitting down, and will instead provide developers the tools they need to continue being productive in the web without having to learn Javascript.  Maybe that's a bad thing, but I see it as being the same kind of advancement we saw with C being more-or-less a fancy compiler/converter for Assembly, and how Java became a step up from C with the addition of a GC and a managed runtime.  
  
It's interesting times, and I'm kind of excited to see how this turns out.  I don't mind Javascript, but I certainly don't think I want my future to be burdened with the problems of having to learn HTML+CSS+Javascript, and the idiosyncracies between MS, Apple, Google, and their varying browser support (both mobile and desktop)
