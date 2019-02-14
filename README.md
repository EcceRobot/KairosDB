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
##
Check if Java is already installed:
> java -version

If Java is not currently installed, you'll see the following output:
> -bash: java: command not found

Execute the following command to install OpenJDK:
> sudo apt install default-jre
##
Then you can set KairosDB service is launched at startup:
> systemctl enable kairosdb

The service will start up on **port** 8080 at the server **IPaddress**
In addition, if you go to http://IPaddress:port/ you will find a KairosDB **Web interface**.

## NB: Changing Datastore

KairosDB can be configured to use one of several backends for storing data. By default KairosDB is configured to use an in memory H2 database to store datapoints. To change the datastore that is used change the kairosdb.service.datastore property in the kairosdb.properties file.


## HTTP Rest API

You can use http GET and POST 

for the GET you can copy and paste this messages as URL on the browser and it will show the responses.

Otherwise, you cancURL from terminal

### Health
> curl **-X GET** http://192.168.43.67:8080/api/v1/**health/check**

> curl **-X GET** http://192.168.43.67:8080/api/v1/**health/status**

### List Metric Names
> curl **-X GET** http://192.168.43.67:8080/api/v1/**metricnames**



For the POST you will need a client for attaching data to the POST request, where _-d_ stands for attached **data**.

### Add Data Points

Single point on single metric
> curl **-X POST** http://192.168.43.67:8080/api/v1/**datapoints** **-d** '[{"name": "new_metric","timestamp":1359786400000,"value":123456,"tags": {"client": "client_1"}}]'

Multiple points on multiple metrics
> curl **-X POST** http://192.168.43.67:8080/api/v1/**datapoints** **-d** '[{"name": "archive_file_tracked","datapoints": [[1359788400000, 123], [1359788300000, 13.2], [1359788410000, 23.1]],"tags": {"host": "server1","data_center": "DC1"},"ttl": 300},{"name": "impedance","type": "complex-number","datapoints": [[1359788400000,{"real": 2.3,"imaginary": 3.4}],[1359788300000,{"real": 1.1,"imaginary": 5}]],"tags": {"host": "server1","data_center": "DC1"}},{"name": "archive_file_search","timestamp": 1359786400000,"value": 321,"tags": {"host": "server2"}}]

### Query Metrics

 > curl **-X POST** http://192.168.43.67:8080/api/v1/**datapoints/query** **-d** '{"start_absolute": 1357023600000,"end_relative": {"value": "5","unit": "days"},"time_zone": "Asia/Kabul","metrics": [{"tags": {"host": ["foo", "foo2"],"customer": ["bar"]},"name": "abc.123","limit": 10000,"aggregators": [{"name": "sum","sampling": {"value": 10,"unit": "minutes"}}]},{"tags": {"host": ["foo", "foo2"],"customer": ["bar"]},"name": "xyz.123","aggregators": [{"name": "avg","sampling": {"value": 10,"unit": "minutes"}}]}]}'

## 
