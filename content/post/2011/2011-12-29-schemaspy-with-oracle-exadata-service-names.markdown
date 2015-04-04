---
author: klauer
comments: true
date: 2011-12-29 22:31:00+00:00
layout: post
slug: schemaspy-with-oracle-exadata-service-names
title: SchemaSpy with Oracle Exadata Service Names
wordpress_id: 7
---

So [SchemaSpy](http://schemaspy.sourceforge.net/) is pretty neat, albeit not the newest tool out there, and I was going to try it out to analyze one of my production databases.  However, it flopped over assuming an SID connector instead of a service name, which the company I work for uses exclusively nowadays.  Digging around on Google, I found that the maven-schemaspy-plugin had just handled a pull request to add service names as a connection type by way of custom [database type .properties files](http://schemaspy.sourceforge.net/dbtypes.html), and decided to grab it and try it out myself:

 


[![Image001](http://klauer.files.wordpress.com/2011/12/image001.png?w=300)](http://klauer.files.wordpress.com/2011/12/image001.png)


 

Before you can run this, you’ll need to put several things in the same directory:

 


1.      [SchemaSpy.jar](http://sourceforge.net/projects/schemaspy/files/schemaspy/SchemaSpy%205.0.0/)




2.      [Oracle JDBC driver .jar](http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html)




3.      [orathin_servicename.properties](https://github.com/wakaleo/maven-schemaspy-plugin/raw/master/src/main/resources/net/sourceforge/schemaspy/dbTypes/orathin_servicename.properties) file 




4.      [GraphViz](http://www.graphviz.org/) (make sure the dot.exe is in your path, it’s called by SchemaSpy to generate the charts)


 

To run it is pretty simple, though:

java -jar .schemaSpy_5.0.0.jar -t orathin_servicename -u A03182 -p <your_password> -o outputdirectory -dp ojdbc6.jar -host serverhost -db database.world–port 1521 –all

The parameters around this are pretty straightforward:
<table style="border-collapse:collapse;border:none;" border="1" class="MsoTableGrid" >
<tbody >
<tr >

<td width="47" style="padding:0 5.4pt;" valign="top" >-jar
</td>

<td width="319" style="border-left:none;padding:0 5.4pt;" valign="top" >Schemaspy.jar file
</td>
</tr>
<tr >

<td width="47" style="border-top:none;padding:0 5.4pt;" valign="top" >-t
</td>

<td width="319" style="border-top:none;border-left:none;padding:0 5.4pt;" valign="top" >Property type (orathin_servicename defaults to orathin_servicename.properties located in your local directory)
</td>
</tr>
<tr >

<td width="47" style="border-top:none;padding:0 5.4pt;" valign="top" >-u
</td>

<td width="319" style="border-top:none;border-left:none;padding:0 5.4pt;" valign="top" >Username
</td>
</tr>
<tr >

<td width="47" style="border-top:none;padding:0 5.4pt;" valign="top" >-p
</td>

<td width="319" style="border-top:none;border-left:none;padding:0 5.4pt;" valign="top" >Password
</td>
</tr>
<tr >

<td width="47" style="border-top:none;padding:0 5.4pt;" valign="top" >-o
</td>

<td width="319" style="border-top:none;border-left:none;padding:0 5.4pt;" valign="top" >Output directory
</td>
</tr>
<tr >

<td width="47" style="border-top:none;padding:0 5.4pt;" valign="top" >-dp
</td>

<td width="319" style="border-top:none;border-left:none;padding:0 5.4pt;" valign="top" >JDBC driver (oracle)
</td>
</tr>
<tr >

<td width="47" style="border-top:none;padding:0 5.4pt;" valign="top" >-host
</td>

<td width="319" style="border-top:none;border-left:none;padding:0 5.4pt;" valign="top" >Server name
</td>
</tr>
<tr >

<td width="47" style="border-top:none;padding:0 5.4pt;" valign="top" >-db
</td>

<td width="319" style="border-top:none;border-left:none;padding:0 5.4pt;" valign="top" >Service name
</td>
</tr>
<tr >

<td width="47" style="border-top:none;padding:0 5.4pt;" valign="top" >-port
</td>

<td width="319" style="border-top:none;border-left:none;padding:0 5.4pt;" valign="top" >Port number (not an optional field)
</td>
</tr>
<tr >

<td width="47" style="border-top:none;padding:0 5.4pt;" valign="top" >-all
</td>

<td width="319" style="border-top:none;border-left:none;padding:0 5.4pt;" valign="top" >Create analysts for all schemas and databases that this user can see.  Creates a good view for your username, probably a narrower view for someone like tdcbatch or whatnot
</td>
</tr>
</tbody>
</table>
