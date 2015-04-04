---
author: klauer
comments: true
date: 2012-10-18 03:14:51+00:00
layout: post
slug: resources-for-learning-datomicdatalog
title: Resources for Learning Datomic/Datalog
wordpress_id: 173
---

Okay, so there's alot of talk about NoSQL, and as you would rightly guess, everybody has thrown their implementation in the ring.  I think out of most of them, [Datomic](http://www.datomic.com) is one of the more unique entries in the field.

However, it's hard for me (and probably anyone with SQL knowledge) to really understand what makes Datomic useful or anything more than an incremental improvement at the cost of eschewing SQL as a querying language (well, that was my initial thought at the time--it's changed since then).

I think that with the recent release of [codeq](http://blog.datomic.com/2012/10/codeq.html), the guys behind Datomic are trying to point out the usefulness and simplicity of their database model, and make it accessible to a larger audience.


Now, what do you want to learn to understand codeq?  Well, you could start by reading the blog post about it:




[http://blog.datomic.com/2012/10/codeq.html](http://blog.datomic.com/2012/10/codeq.html)


After that, you might want to get Datomic installed and running on your system.  I'd recommend downloading the free edition for tinkering: [http://downloads.datomic.com/free.html](http://downloads.datomic.com/free.html)

Once you have it downloaded, you'll probably want to understand how to get it running.  The [codeq README](https://github.com/Datomic/codeq#codeq) has that wrapped up.  It links to the [Datomic Getting Started](http://docs.datomic.com/getting-started.html) page to understand how to get it running.  It couldn't be easier than this, though:


<blockquote>

>     
>     $ cd /wherever-you-extracted-datomic/
>     $ bin/transactor
>     ... watch it start up
> 
> 
</blockquote>


Installing codeq is explained [on their site, too](https://github.com/Datomic/codeq#usage), although it would be nice for them to supply a runnable .jar instead of asking for everyone to install [Leiningen](https://github.com/technomancy/leiningen) and run `**lein uberjar**`, but it's simple enough if you're into Clojure.

Now, to review, the steps to get up-and-running with Codeq and a git repo (Clojure-based at the moment) of your choice are:



	
  1. [Get Datomic installed](http://www.datomic.com/get-datomic.html)

	
  2. [Start the Datomic transactor](http://docs.datomic.com/getting-started.html)

	
  3. [build Codeq](https://github.com/Datomic/codeq#usage)

	
  4. [run Codeq on your git repo](https://github.com/Datomic/codeq#usage) and

	
  5. import it into Datomic


You'll probably wonder what the heck to do next, such as how to query it.  Here's a couple links that got me started:

	
  * [Querying Tutorial](http://docs.datomic.com/query.html) for Datalog in Datomic

	
  * [Datalog examples using Clojure data structures itself](https://gist.github.com/2645453) (this alone makes datalog useful for Clojure coding as you don't even need Datomic in some cases to use it)

	
  * [code examples](https://github.com/jonase/codeq/blob/queries/src/datomic/codeq/examples.clj) from this [google group post](https://groups.google.com/d/msg/datomic/Xx2nLvCl4s4/y6LQPO7xyCgJ) querying some git internals

	
  * Finally, looking at the [codeq git schema](http://cloud.github.com/downloads/Datomic/codeq/codeq.pdf) might make some sense for you now





## Summary


It would be nice if this was pre-packaged, but it's only a week old, so I have hopes that this will come along pretty quickly.

I actually wouldn't be surprised if someone decides to do something akin to what [rubydoc.info](http://rubydoc.info/) does for documentation.  Rubydoc.info will generate YARD documentation for all of the gems in rubygems, as well as many Github projects, too.  This is a great resource, and it's done because it's simple enough to just run the same documentation tool against all of the same kinds of projects.

With codeq, all that's needed to index a project is: 1) a Clojure project 2) backed by git.  You could probably do that for most of the projects on Clojars.org if they specify a Git repo, and then provide some front-end site that would have common queries (as seen by some of the code examples in codeq so far).  The great thing about codeq is that since the schema is the same across all git repos, useful queries and very portable across projects, and so it makes perfect sense for those kinds of queries to be reused.
