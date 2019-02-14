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


Then you can set KairosDB service is launched at startup:
> systemctl enable kairosdb

The service will start up on **port** 8080 at the server **IP Address**


## HTTP REST API

You can use http GET and POST 

for the GET you can copy and paste this messages as URL on the browser:


> curl -X GET http://192.168.43.67:8080/api/v1/health/check

> curl -X GET http://192.168.43.67:8080/api/v1/health/status

List Metric Names
> curl -X GET http://192.168.43.67:8080/api/v1/metricnames

for the POST you will need a client for attaching data to the POST request:
You can use cURL from terminal:

> curl -X POST http://192.168.43.67:8080/api/v1/datapoints -d '[{"name": "new_metric","timestamp":1359786400000,"value": 123456,"tags": {"client": "client_1"}}]'



## 
