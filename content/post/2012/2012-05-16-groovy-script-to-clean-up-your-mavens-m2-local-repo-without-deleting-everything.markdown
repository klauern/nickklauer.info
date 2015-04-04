---
author: klauer
comments: true
date: 2012-05-16 16:10:14+00:00
layout: post
slug: groovy-script-to-clean-up-your-mavens-m2-local-repo-without-deleting-everything
title: Groovy script to clean up your maven's ~/.m2/ local repo without deleting everything
wordpress_id: 88
---

When I want to clear out some space, I end up doing **'rm -rf ~/.m2/repository/`** or **'del -Recurse -Force ~/.m2/**repository' but that tends to remove EVERYTHING and makes your builds longer in the future. I thought this little script was pretty useful for dev work as it only clears out old SNAPSHOT versions from your repo, as well as older versions of dependencies (such as outdated JUnit deps or whatnot).

[http://blog.orange11.nl/2011/08/01/cleaning-up-your-maven-repository/](http://blog.orange11.nl/2011/08/01/cleaning-up-your-maven-repository/)

The gist of it is that this is a Groovy script to delete out--per your configuration of the script--X number of days back of SNAPSHOT releases and older versions of libraries where a newer one has existed for Y days.

It's probably best to just read the post above, but if you aren't one of those types to spend time doing that, you can skip the rigmarole and just download the script:

[https://github.com/jettro/small-scripts/blob/master/groovy/CleanDir.groovy](https://github.com/jettro/small-scripts/blob/master/groovy/CleanDir.groovy)

Mind you, you still need to read the script and set your # of days to keep, especially the line that says:

`def dryRun = true`

To say something like **'false'** so it actually does something. ;)

Here’s a run of mine (albeit not my actual ~/.m2 folder, but it shows that it works):

`C:\mydocs\Downloads`

`> **C:\Java\Groovy\groovy-1.8.6\bin\groovy.exe CleanDir.groovy**`

*******************************************************************************

* About the clean a maven repository

* Start cleaning at path: `C:\Documents and Settings\A03182\.m2\repository`

* Remove all snapshots that are older than 60 days

* Remove all versions that are older than 90 days and do have a higher version available

* **We are going to do a dry run**

* We only remove snapshots, no versioned artifacts are deleted

* **Total size cleaned is 35k**

*******************************************************************************

About to remove directory C:\Documents and Settings\A03182\.m2\repository\net\sfalxa\jlatexmath\1.9.1-SNAPSHOT with total size 1878 and 124 days old

About to remove directory C:\Documents and Settings\A03182\.m2\repository\org\clojars\bmabey\congomongo\1.1.2-SNAPSHOT with total size 6089 and 124 days old

About to remove directory C:\Documents and Settings\A03182\.m2\repository\org\clojars\somnium\clojure-db-object\1.1.1-SNAPSHOT with total size 4368 and 124 days old

About to remove directory C:\Documents and Settings\A03182\.m2\repository\org\clojars\somnium\mongo-java-driver\1.1.0-SNAPSHOT with total size 4576 and 124 days old

About to remove directory C:\Documents and Settings\A03182\.m2\repository\org\clojure\clojure\1.2.0-master-SNAPSHOT with total size 1563 and 124 days old

About to remove directory C:\Documents and Settings\A03182\.m2\repository\org\clojure\clojure-contrib\1.2.0-SNAPSHOT with total size 1567 and 124 days old

About to remove directory C:\Documents and Settings\A03182\.m2\repository\org\danlarkin\clojure-json\1.1-SNAPSHOT with total size 4944 and 124 days old

About to remove directory C:\Documents and Settings\A03182\.m2\repository\swank-clojure\swank-clojure\1.3.0-SNAPSHOT with total size 5537 and 124 days old

About to remove directory C:\Documents and Settings\A03182\.m2\repository\swing\repl\swing\repl\1.0.0-SNAPSHOT with total size 5404 and 124 days old

Pretty neat stuff, check it out. I’ve attempted to attach the script, but I wouldn’t be surprised if it gets removed or flagged by the email filter for some reason. I cleaned up about 200MB from my repo, maybe you’ll find it’s useful for you, too.
