# KairosDB

## Set up a database server running KairosDB
Referring to:
https://kairosdb.github.io/docs/build/html/GettingStarted.html
Go to
https://github.com/kairosdb/kairosdb/releases
and download the latest .deb package
> kairosdb_1.2.2-1_all.deb 

Then install with **dpkg**
> $ sudo dpkg -i kairosdb_1.2.2-1_all.deb

You need **Java** 1.8 running also on the system

Check if Java is already installed:
> java -version

If Java is not currently installed, you'll see the following output:
> -bash: java: command not found

Execute the following command to install OpenJDK:
> sudo apt install default-jre

## HTTP REST API 

## 
