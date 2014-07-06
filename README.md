WMB-SOF
=======

Framework for WMB and IIB


Abstract:
------------
WMB-SOF (WebSphere Message Broker – Service Oriented Framework) is an Add-On for the WebSphere Message Broker to enhance the Brokers functionality with a reusable Framework. 

The Out-of-the-box WebSphere Message Broker does not provide common services like
•	Errorhandling
•	Routing
•	Logging
•	Restarting
•	Notification
Such services have to be developed in nearly every customer engagement. That was the reason for developing a reusable framework, to
•	reuse the components
•	reduce effort and development time
•	let the developer concentrate on the process glow (e.g. mapping, transformation, sequencing, etc.)
 
The Framework provides a set of reusable components and services which can be used in the Message Flows.
It is a service driven Framework and is separated into the following services and components (in brackets)
•	Dispatcher
•	Processing
•	Delivery
•	(Value Mapping)
•	(Errorhandling)
•	(Logging)
•	Notification
•	Restart
•	Maintenance
•	Monitoring
•	Sequencing
•	Toolbox: Flows as templates
•	Configuration Database (key component)
•	Administration GUI 


Within the framework concept, each message goes through three independent Message flows. Only the pure processing flows (process) has to be developed individually. The process flow is responsible for message format transformation and process logic like sequencing, collecting, mapping, etc. Each process step is logged into the Database. 

The first process step is a Dispatcher Service. The Dispatcher Service receives messages from internal and external systems via:

•	WebSphere MQ
•	HTTP/S
•	File (via FTP)
•	SAP Adapter
•	Siebel Adapter
•	SQL
•	JMS
•	SOAP
•	WebSphere TX
•	Extendable 

Key points of the Dispatcher Service tasks:
•	Identify Sender, Message Type, Receiver and determine the overall process.
•	Determine Routing Parameters for further processing.
•	Routing Parameters are saved in the WMBSOF configuration database and are maintained via the Administration GUI. The Dispatcher Service determines the Routing Parameters from the configuration databaseà this is the only Service that accesses the database.
•	Use of Framework Services and components.
•	Logging via the Logging Service.
•	Sends the message to the next process step which is a Process Service.
•	If there is an error, the Errorhandling component is used to process the message, to perform a restart later on (Restart Service).

The second process step is a Process Service. Main key points of the Process Service's task:

•	Transformation of messages and process logic (serialization, collecting, mapping, etc.).
•	These are not elements of the WMB-SOF Framework and are created by the developers.
•	MQ entry point (MQ Input Node).
•	Use of Framework Services and components.
•	Logging via the Logging Service.
•	Sends the message to the next process step which is a Delivery Service.
•	If there is an error, the Errorhandling component is used to process the message, to perform a restart later on (Restart Service).

 
The third process step is one or more Delivery services. The individual Delivery Services are used to deliver messages to external and internal systems. This includes delivery via:

•	WebSphere MQ
•	HTTP/S
•	File (via FTP)
•	SAP Adapter
•	Siebel Adapter
•	SQL
•	SOAP
•	JMS
•	Extendable 

Main key points of the Delivery Service's task:
•	Delivery of the Message.
•	MQ entry point (MQ Input Node).
•	Use of Framework Services and components.
•	Logging via the Logging Service.
•	Sends the message to the external or internal systems.
•	If there is an error, the Errorhandling component is used to process the message, to perform a restart later on (Restart Service).

For Dispatching (receiving of messages - entrance processing) and Delivery (dispatch from message - output processing) pre-defined flow Templates are available, which must be configured via the administration GUI. In individual cases it can become necessary that in the delivery and dispatcher Main flow additional functionality has to be implemented. 


The expiration of the processing chain dispatcher - process - delivery is controlled via Database entries and can be changed at run-time.

The three Main Flows (Dispatcher, Process, Delivery) of the overall-process communicate with each other via WebSphere MQ Series queues.

The configuration of the Routing for the process chain within the WebSphere Message Broker – Service Oriented Framework is carried out via an Administration GUI. The GUI is used to define all information necessary to navigate the received message through the individual Message Flows. Each Message Flow that has been created with Framework components requires special routing information before it can be successfully processed.

All the definitions made for the Administration GUI are stored in a DB2 V9.5 or higher database. The tables in this database create references to each other by using unique IDs. 


Program Requirements:
-------------------------------
-	WebSphere Message Broker 7.0 or higher 
-	WebSphere Message broker Toolkit 7.0 or higher
-	WebSphere MQ 7.0 or higher
-	DB2 9.5 or higher   
-	WebSphere Application Server 7.0.x for the administration GUI or higher


Installation:
----------------
1.	Import the WMBSOF_FLW project into the WebSphere Message Broker Toolkit
2.	Create the Database WMBSOF with the associated tables
3.	Start the administration GUI and define the routing parameter

Usage:
---------
The WMB-SOFramework is a set of WebSphere Message Broker Sub Flows and Main Flows. 

The Main Flows provide the following service:

•	Generate Log Events in the Database based on defined properties
•	Notification
•	Restart
•	Maintenance
•	Monitoring
•	Sequencing

The Sub Flows can be implemented in the customer Flows and provide

•	Dispatching
•	Delivery
•	Value Mapping
•	Errorhandling
•	Logging

 

