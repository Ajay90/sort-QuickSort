# sky-profiler
SKY Profiler does real time monitoring of your webMethods Integration Server service invocations.

## Description
SKY Profiler does real time analytics of profiled data from the production instances of webMethods Integration Server to identify potential bottlenecks and help operational teams avoid any downtimes.
**Note: All examples below are specific to Microsoft Windows File System. The service summary table shows only the latest data from the SKYProfiler server start. If there were services executed before server start those will be not be shown. However the report will show all the data.”**

## Set-up

### Pre-requisite
**Note: Currently SKY Profiler Runtime works only with webMethods Integration Server installed on Linux box.
		The User Interface is tested on Google Chrome.
		The service summary table shows only the latest data from the SKYProfiler server start. If there were services executed before server start those will be not be shown. However the report will show all the data.**

The project needs below software as a pre-requisite to get started.
* Apache Ant
* Apache Maven
* MongoDB
* Zookeeper
* Apache Kafka

Download SKY Profiler by
```
git clone https://github.com/SoftwareAG/sky-profiler
```
 Note: sky-profiler home
 
Update maven path in build.properties.
Create a data directory **"data"** for MongoDB. _(E.g., C:\Program Files\MongoDB\data)_
Edit zookeeper.properties in Apache Kafka to update the Data Directory location to **"C:/zookeeper-3.4.9/temp"**
Edit server.properties in Apache Kafka to update the Log Directory location to **"C:/kafka_2.11-0.10.1.1/kafka-logs"**. Add **"auto.create.topics.enable=true"** property at the end of the server.properties.
Copy **"wm-isclient.jar"** and **"wm-isserver.jar"** from webMethods Integration Server installation to "{sky-profiler_home}/lib" which are required for SKY Profiler Runtime component.

### Build
```
ant all
```

The above command will build SKYProfiler.zip (webMethods Integration Server package) and skyprofiler-1.0-RELEASE.jar inside "{sky-profiler_home}/dist" directory. 

## How it works

Install the SKYProfiler package in the Integration Server which needs to be monitored.

### SKY Profiler Server requires the following services to be running to start-up
* MongoDB
```
Start MongoDB like mongod.exe --dbpath="C:\Program Files\MongoDB\data"
```

* Zookeeper
```
Start Zookeeper like zkServer.cmd
```

* Apache Kafka
```
Start Kafka like kafka-server-start.bat ..\..\config\server.properties
```

SKY Profiler Server
```
java -jar skyprofiler-1.0-RELEASE.jar
```

Once the service is up, you could access the application on http://localhost:8080.
Default crednetials: admin/password1234


## Basic Usage
	* Add a webMethods Integration Server which needs to be monitored and click on the server added
	* Navigate to Options->Configuration
	* Select the Package which needs to be monitored
	* Fill-in other details and Save
	* Click on Start to start monitoring
	* Any service execution that belongs to the selected will get displayed in the Service Monitoring table
		
### To get more details:
	* Click on the service name to expand the collapsible bar
	* A Response Time graph will be shown (Only the latest service execution reponse time will be displayed)
	* Click on one of the data point in the graph for further details. This will display Service Call Tree
	* Service call tree displays service hierarchy
	* This will show you which service is taking more time to execute
	* You could then click on the Graph icon corresponding to that service, which then opens up a window containing graphs like CPU, Response time, Threat Level CPU, etc
	* Click on the data point in one of the graphs to highlight the correlation line across all the graphs 
	* These graphs help you map the spiked response time with other performance parameters to decide which resource parameter could have caused the spike
		
### Report generation:
After all the profiling is completed you could generate a report as follows:
		
	* Navigate to home screen
	* Click on Options-> Report
	* An HTML report is generated

Contact us at [TECHcommunity](mailto:technologycommunity@softwareag.com?subject=Github/SoftwareAG) if you have any questions.
