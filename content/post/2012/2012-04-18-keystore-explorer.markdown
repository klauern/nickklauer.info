---
author: klauer
comments: true
date: 2012-04-18 13:41:01+00:00
layout: post
slug: keystore-explorer
title: KeyStore Explorer
wordpress_id: 69
---

So I feel really late to the party, but I have not mucked about with java keystores much. However, when I did, I spent most of that time wincing in virtual pain having to figure out what magical command-line incantations will let me add/remove/modify certificates on the keystore.

Enter the KeyStore Explorer - [http://www.lazgosoftware.com/kse/index.html](http://www.lazgosoftware.com/kse/index.html)

This is a GUI to modify your Java keystores. So if you’re like me and having to work with an app server that has rolling certificates coming in and out, you either

1. automate it

2. simplify it

This aims to meet #2.

For example, I had to update a certificate store for a weblogic server. In particular, one of the certs changed on me and stopped working. I just open up the .jks file, enter the password for it, and

see what’s going on.

[![](http://klauer.files.wordpress.com/2012/04/image001.png)](http://klauer.files.wordpress.com/2012/04/image001.png)

For my fix, I noticed that the certificate serial number didn’t match what the server popped up. You can open a certificate to see the serial number, and other details:

[![](http://klauer.files.wordpress.com/2012/04/image002.png)](http://klauer.files.wordpress.com/2012/04/image002.png)

All in all, it makes examining a keystore easier. Check it out.

Download link - [http://www.lazgosoftware.com/kse/downloads.html](http://www.lazgosoftware.com/kse/downloads.html)
