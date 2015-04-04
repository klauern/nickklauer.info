---
author: klauer
comments: true
date: 2012-03-01 03:22:44+00:00
layout: post
slug: logback-logging
title: Logback Logging
wordpress_id: 39
---

So logging is just not an attractive feature in most Java applications, so I can understand why alot of people just disregard this choice when writing a Java application.  However, when it comes to picking logging as a feature, it's best to pick one that's



	
  1. simple to set up

	
  2. grows with your app

	
  3. sane defaults

	
  4. configurable when it doesn't fit the bill


Logback is one of those choices that I'd recommend you just pick for your Java apps and worry about it later.

Logback is the successor to the popular Log4J library written by the same developer.  That should tell you where the developer's spending his time.

So why should you pick it?  Well, to cherry-pick some bullet-points from the developer's page on [why you should switch](logback.qos.ch/reasonsToSwitch.html) (highly suggest reading that over):



	
  1. Faster than log4J for some cases (10X faster)

	
  2. interops easily with SLF4J

	
  3. Documentation is very thorough (otherwise I'd not be writing this post)

	
  4. XML or Groovy config file

	
  5. reloads config file without a restart

	
  6. automatic file rolling, zipping, and deletion


Anyways, it's about as feature-packed as you could honestly want with log files.  So let's get to configuring it out.

I won't bore you with the large architecture and setup options for getting started, so let's assume a couple things to make this easy to follow:

	
  * You're using Maven to build your app

	
  * You'll use two appenders:

	
    * one for debugging to **STDOUT**

	
    * one for logging to a file in production




	
  * We'll roll these logs daily, keeping only **30 days** of saved off log files.




Configuring your Logback with defaults.




Let's assume that you're just starting out, and wnat to put the logger in some of your code.  This is pretty easy:


[sourcecode language="java"]
package klauer.softwarethings;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class LoggerThingy {
  public static void main(String[] args) {

    Logger logger = LoggerFactory.getLogger("klauer.softwarethings.LoggerThingy");
    // The simple case is just that--simple.
    logger.debug("Hello world.");

    String some_val = "why not";
    String some_other_val = "another one?";
    // Instead of using String + String or some convoluted StringBuffer.append(), we can use {}'s for two or less values.
    logger.debug("Hello World,  I have these additional fields: {} {}", some_val, some_other_val);

    String third_val = "we'll keep going";
    // What do we do for three or more?  Easy:
    Object[] params = { some_val, some_other_val, third_val };
    logger.debug("All of these values are here, {} {} {}", params);
  }
}
[/sourcecode]

So as you might guess, it's not terribly difficult to spruce up your code with loggers.  Note that the `LoggerFactory` is taking a String from which I put in my class name, but you have the flexibility to take any structure of logging you want. Logback includes a hierarchical representation of loggers, so `klauer.softwarethings` is a specific level, such that a class logger of `klauer.softwarethings.ANeatoClass` would have a logger at the same level as this logger, and a class at `klauer.MainClass` is at a higher level. This kind of representation can matter to you if you're building a very rich set of loggers for your app/s and want a consistent style, but for maintainability, it would be best to stick with classes. Much of this can be configured in your `logback.xml` or `logback.groovy` files, which are covered **deeply** in the [documentation](http://logback.qos.ch/manual/architecture.html).  I'll leave it to you to dig in and find what works best, but I've found that simply specifying each logger by the class that it's being invoked from is enough for me to know the flow of the code and helps with log parsers like Splunk or Loggly in finding trends or hot zones.

As I had mentioned above, you can choose either an **`XML`** or **`groovy`** configuration file format. In addition to that, you can have a separate `logback-test.xml/groovy` file that will be used for debugging purposes only. What makes this especially useful is that if you use it with Maven, you can just put your `logback-test` file in `src/test/resources` and it will only be used for your testing and regular build-cycle process. This way you aren't creating log files for testing, for instance, or sending email alerts on `Logger.error()` calls. The `logback.xml/groovy` that sits in your `src/main/resources` will get bundled up into your deployed application.

For the given example below, I've decided to use XML, but there is a nice [`logback.xml-to-groovy`](http://logback.qos.ch/translator/asGroovy.html) converter, which should make light work of the example code below. Let's take a look at a sample logback configuration file:

[sourcecode language="xml" gutter="false"]
<configuration>
  <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
    <file>logFile.log</file>
    <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
      <!-- daily rollover -->
      <fileNamePattern>logFile.%d{yyyy-MM-dd}.log</fileNamePattern>

      <!-- keep 30 days' worth of history -->
      <maxHistory>30</maxHistory>
    </rollingPolicy>

    <encoder>
      <pattern>%-4relative [%thread] %-5level %logger{35} - %msg%n</pattern>
    </encoder>
  </appender> 

  <root level="DEBUG">
    <appender-ref ref="FILE" />
  </root>
</configuration>
[/sourcecode]

What do we have here?



	
  * `appender class` simply defines the type of appender. In this case, we're using a `RollingFileAppender`, but there are a number of other options, such as a `ConsoleAppender`, `SMTP` appender, etc. etc.. It's all laid out in the [Appenders](http://logback.qos.ch/manual/appenders.html) chapter of the documentation.

	
  * `rollingPolicy` dictates how to best roll the logs out. In this case, we're using a simple `[TimeBasedRollingPolicy](http://logback.qos.ch/manual/appenders.html#TimeBasedRollingPolicy)` as it lets us specify the filename of the log and the number of days to keep. Another option that could be used is file size-based

	
  * `fileNamePattern` can be pretty easy to understand, but the part that matters is the level of granularity you specify in your logs. For instance, a date format of `%d{yyyy-MM}` will roll monthly, thus changing how `maxHistory` is interpreted.

	
  * The `encoder` pattern is laid out in the appenders documentation as well, but in this case, the `RollingFileAppender` uses a [OutputStreamAppender](http://logback.qos.ch/manual/appenders.html#OutputStreamAppender) which has it's own semantics. You can see that we're teasing out the thread that it's running under, the log level, name of the logger, and the message, but there are as always a number of good options if those don't satisfy your need that much. What works great about this is that you can use this exact format in a Splunk configuration to let Splunk know just how to parse log files generated by your application.

	
  * The `root level` tells us at what level of the logger we want to capture, and the `appender-ref` tells us which appender to use for this level. Much of this is covered in the [Configuration](http://logback.qos.ch/manual/configuration.html) chapter of the documentation, which also goes over the Log Levels, log hierarchy and parent/child relationships. For our purposes, we just want to capture any logging events Debug or Higher. In production, you could probably see this being "INFO" or higher, or separate it out to have a separate logger that sends emails on "ERROR" or higher.


I've only scratched the surface for this, but hopefully you can see that logging doesn't have to be so simple as to be just `System.out.println` everywhere. It can be useful, functional, and not alot of work. As you can see above, the `logback.xml` file is really all you need to configure to make it work the way you want to, and I've found that the defaults for things such as `RollingFileAppender` is pretty simple to set up. Logback is smart enough to roll your logs over daily, zip them up, and delete out the old ones, so it should make keeping logs a simple matter with little maintenance to it.



# More information:




## Logback - [http://logback.qos.ch/](http://logback.qos.ch)




## Maven:


[sourcecode language="xml"]
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-core</artifactId>
    <version>1.0.0</version>
</dependency>
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.0.0</version>
</dependency>
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-api</artifactId>
    <version>1.6.4</version>
</dependency>
[/sourcecode]
