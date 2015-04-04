---
author: klauer
comments: true
date: 2012-10-23 19:58:43+00:00
layout: post
slug: stopping-an-ejb-programmatically
title: Stopping an EJB Programmatically
wordpress_id: 193
---

Below is a small story and a snippet or two of code to shut down an EJB programmatically. However, I hope that by posting what I did to dig in to this, I can show how you can use JMX and MBeans to your advantage programmatically for _any_MBean.

In looking at [ JVisualVM](http://docs.oracle.com/javase/6/docs/technotes/guides/visualvm/index.html) (bundled with all JDK’s since recent Java 6 updates), I opened up the Glassfish server and looked up the MBeans that are deployed out there. The project I’m working with (and the class name) is **VendorUpdateToTREES**:

[![](http://klauer.files.wordpress.com/2012/10/image001.png)](http://klauer.files.wordpress.com/2012/10/image001.png)

In this bean, there’s another sub-bean:

[![](http://klauer.files.wordpress.com/2012/10/image002.png)](http://klauer.files.wordpress.com/2012/10/image002.png)

Its name is:

[![](http://klauer.files.wordpress.com/2012/10/image003.png)](http://klauer.files.wordpress.com/2012/10/image003.png)

Note the only difference between the two is the **servermgt=true** field.

If you were to look at both beans, one shows controls the EJB itself, while the **servermgt** bean appears to control topics and queues. We won’t be needing that functionality, so we need to be sure to exclude this bean.

Now, on to the code:

[![](http://klauer.files.wordpress.com/2012/10/image004.png)](http://klauer.files.wordpress.com/2012/10/image004.png)

Some reference bits:

Sets#filter, is from Google Guava: [ http://docs.guava-libraries.googlecode.com/git-history/release/javadoc/com/google/common/collect/Sets.html#filter(java.util.Set, com.google.common.base.Predicate)](http://docs.guava-libraries.googlecode.com/git-history/release/javadoc/com/google/common/collect/Sets.html#filter(java.util.Set,%20com.google.common.base.Predicate))

ObjectNameStartsWithFilter, is a Predicate object that I implemented to do one simple thing: filter out ObjectNames that don’t start with the parameter passed in:

[![](http://klauer.files.wordpress.com/2012/10/image005.png)](http://klauer.files.wordpress.com/2012/10/image005.png)

That’s about as easy as a Predicate can get. Note that **User:Name=** is part of the name for our EJB:

[![](http://klauer.files.wordpress.com/2012/10/image006.png)](http://klauer.files.wordpress.com/2012/10/image006.png)

So, while I showed how I found the name to the MBean, the code to shut it down should be simple enough to copy/paste with no changes to **any** EJB deployed in Glassfish. I don’t know exactly how the MBeans look on Tomcat, WebLogic, or others, but the same principle applies in how it would be structured, so you could easily adapt this to other containers.
