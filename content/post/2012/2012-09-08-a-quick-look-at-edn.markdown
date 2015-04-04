---
author: klauer
comments: true
date: 2012-09-08 02:36:32+00:00
layout: post
slug: a-quick-look-at-edn
title: A Quick Look at edn
wordpress_id: 68
---

I code in Clojure in my free time. It has a nice set of features and syntax that is a vast simplification and improvement over Java. I'm also a pretty big fan of the JVM and it's wealth of libraries and such, so having Clojure run on the JVM makes using Clojure a lot easier.  Anyways, something about Clojure that I found pretty easy to transition to was Clojure's set of data literals.  Things like Maps being defined within {}, sets in #{}, lists as (), and vectors as [] is pretty consistent with Java and actually alot closer to Ruby (another of my favorite languages).

So having just read about Rich Hickey releasing a data format based largely on a superset of Clojure's data types, I was pretty excited:


[tweet https://twitter.com/swannodette/status/243866691728183298]


Alot of people I've read so far are comparing it to JSON, which is probably pretty close.  Here are a couple of things I think improve upon how people use JSON and what makes edn better as a data interchange format:



	
  * namespaced symbols.  These alone make hashmaps and sets easier to parse and define uniqueness.  I suppose you could get by with "string" everywhere, but anything you'd do in a "string" you'd have to implement a parser for more complex logic on either side.   For instance, namespacing your keywords and symbols like so:[sourcecode language="clojure"]
{ :counterparty/name :keywordval
  :counterparty/id 13850
  :counterparty/inception 1930 }
[/sourcecode]

allows you to be alot more flexible in your data, and since it's built in to the spec, there would be no extra work involved in using it.

	
  * tagged elements


Defining your own types that can be interpreted reminded me of Thrift and Protocol Buffers, although I think their implementations were meant more for computer-computer communication moreso than computer-person-computer or some variant thereof.





This could be ported to Java and other languages pretty easily, and I think it marks the state of the next data format.  Even if edn doesn't make it, it shows where JSON needs to improve, if it ever can.  Many can speculate why JSON became popular, but I attribute it to two things:

	
  1. JSON is based on Javascript, and Javascript is the defacto language on the web simply because all browsers support it and nothing else.

	
  2. JSON is more readable than XML to the human eye.  That said, I've never understood why XML was ever used for anything a developer or user would write for, as that was never it's intent.


JSON does lack specific features from edn which I think would put JSON more on par with alot of developers needs.

All in all, I like this, and hope that it picks up some momentum in use.  I will definitely be keeping an eye out for future use of it.

If you'd like to follow along with what alot of people are also thinking about the edn specification, the [Clojure Google Group](https://groups.google.com/d/topic/clojure/aRUEIlAHguU/discussion) has a pretty lively discussion going on right now.
