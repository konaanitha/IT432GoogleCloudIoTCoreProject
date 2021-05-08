# Google Cloud IoT core Project- To Stream Heartrate into Google cloud.

## Introduction:
&emsp; &emsp; Internet of Things(Iot ) refers to a system that are connected and can transmit data over the wireless network (internet), without user involvement. IoT devices include wireless sensors, software and devices. This is expanding rapidly in the present years.

&emsp; &emsp; Google Cloud Platform is an Infrastructure as a Service (ISAS), in which the cloud maintains all the core infrastructure, hardware, software and servers in the cloud on behalf of the user. All services used in the Google Cloud are reliable and scalable.

##  Overview:
&emsp; &emsp; Here Raspberry PI, an Iot device captures the heartrate, with the IoT Core securely publish the data to Pub/Sub topic, which is a message queue, where the data will be transferred into a data warehouse with the help of a data pipeline created by the components of Google Cloud. The result data can be visualized using data visualization tools such as Excell or google sheets, etc.,.

##  Hardware Requirements:
1. Raspberry Pi, SD card
2. Mouse
3. Keyboard
4. Monitor
5. HDMI cable
6. Heart Rate sensor

## Software:
1. Raspeberry OS
2. Putty for Windows/Terminal for Mac
3. Excell or Google sheets

## Getting Started:
&emsp; &emsp; We need to have a google account, to use Google Cloud Platform. If you don't have a google account, you must create one. Sign-in to the Google Cloud Console.

* **Environment Setup.**
 
&emsp; &emsp; You can use default project ("My First Project") or create a new Google Cloud project on the project selector page. Through the project, you can have access to all the resources of Google Cloud Platform. Create a Project with the name 'IoT-heartrate’, The project ID is unique name across the Google Cloud.

* **Enable APIs.**
   
&emsp; &emsp; Next, enabling the APIs of the Pub/Sub, IoT Core, Dataflow, Compute Engine, which are used in this project. To enable APIs, select and click on APIs & Services from Cloud Console menu. Search for the <b> Cloud Pub/Sub API </b> and click on the result and <b>Enable API</b>. Follow the same steps for the other above mentioned APIs.

## Create a BigQuery Table:
&emsp;&emsp;BigQuery is a serverless, low-cost enterprise data warehouse. In this, we create schema for the table  and the data is stored in the tables.

 &ensp;To Create a table that hold all of the IoT heartrate data:
 1. From the **Cloud Console** --> select **BigQuery.**
 2. Click on three dots next to the project ID --> select **Create Dataset.**
 3. Enter 'heartRateData’ for the Dataset and select the location where it will be stored. 
 4. Click on the three dots next to the Dataset just created, which opens the editor  to create a new  table.
 5. For **Source Data** select create empty table. For Destination table name ,enter the table name as 'heartRateDataTable'.
 6. Under **Schema**, click on the **Add field** to add the fields for the table and select the appropriate datatype for each field. Click on the **Create Table** button.

## Create a Pub/Sub Topic and Subscription:
&emsp;&emsp;Pub/Sub is a real time messaging service  used for ingesting data. It is perfect for handling incoming IoT messages and then allowing downstream systems to process them.Subscription allow other Google Cloud services to access these messages.
1. From the **Cloud Console --> Select Pub/Sub-->  Topics.**
2. If  you see Enable API prompt, click the **Enable API button.**
3. Select **Create Topic** and enter 'heartratedata' as topic name  and click **Create.**
4. Create a Subscription for the topic by clicking on the three dots to create a new subscription-->**Create Subscription.** 
5. Enter the Subscription name 'heartratedata'.
 
We have now The Pub/Sub subscription to pull Iot messages from.

## Use a Dataflow Template:
&emsp;&emsp;Dataflow is cloud based data processing service used for batch and real time data.A Dataflow template will be used to create a process that monitors a Pub/Sub topic for incoming messages and then moves them to BigQuery. The data from the Dataflow will be stored in temporary file,and the location will be provided in cloud storage.
