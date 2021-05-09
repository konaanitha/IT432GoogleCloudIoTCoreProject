# Google Cloud IoT core Project
# Streaming Heartrate into Google Cloud Using IoT Core.

## Introduction
&emsp; &emsp; Internet of Things(IoT) refers to a system that are connected and can transmit data over the wireless network (internet), without user involvement. IoT devices include wireless sensors, software and devices. This is expanding rapidly in the present years.

&emsp; &emsp; Google Cloud Platform is an Infrastructure as a Service (ISAS), in which the cloud maintains all the core infrastructure, hardware, software and servers in the cloud on behalf of the user. All services used in the Google Cloud are reliable and scalable.

##  Overview
&emsp; &emsp; Here Raspberry PI, an Iot device captures the heartrate, with the IoT Core securely publish the data to Pub/Sub topic, which is a message queue, where the data will be transferred into a data warehouse with the help of a data pipeline created by the components of Google Cloud. The result data can be visualized using data visualization tools such as Excell or google sheets, etc.,.

##  Hardware Requirements
1. Raspberry Pi, SD card
2. Mouse
3. Keyboard
4. Monitor
5. HDMI cable
6. Heart Rate sensor

## Software
1. Raspeberry OS
2. Putty for Windows/Terminal for Mac
3. Excell or Google sheets

## Getting Started:
&emsp; &emsp; We need to have a google account, to use Google Cloud Platform. If you don't have a google account, you must create one. Sign-in to the Google Cloud Console.

* **Environment Setup.**

 &emsp; &emsp; You can use default project ("My First Project") or create a new Google Cloud project on the project selector page. Through the project, you can have access to all the resources of Google Cloud Platform. Create a Project with the name 'IoT-heartrate’, The project ID is unique name across the Google Cloud.

* **Enable APIs.**

   &emsp; &emsp; Next, enabling the APIs of the Pub/Sub, IoT Core, Dataflow, Compute Engine, which are used in this project. To enable APIs, select and click on APIs & Services from Cloud Console menu. Search for the <b> Cloud Pub/Sub API </b> and click on the result and <b>Enable API</b>. Follow the same steps for the other above mentioned APIs.

## Create a BigQuery Table
&emsp;&emsp;BigQuery is a serverless, low-cost enterprise data warehouse. In this, we create schema for the table  and the data is stored in the tables.

 &ensp;To Create a table that hold all of the IoT heartrate data:
 1. From the **Cloud Console** --> select **BigQuery.**
 2. Click on three dots next to the project ID --> select **Create Dataset.**
 3. Enter 'heartRateData’ for the Dataset and select the location where it will be stored. 
 4. Click on the three dots next to the Dataset just created, which opens the editor  to create a new  table.
 5. For **Source Data** select create empty table. For Destination table name ,enter the table name as 'heartRateDataTable'.
 6. Under **Schema**, click on the **Add field** to add the fields for the table and select the appropriate datatype for each field. Click on the **Create Table** button.
 
 * [Create Table.png](https://github.com/konaanitha/IT432GoogleCloudIoTCoreProject/blob/main/Images/create%20table.png) {target= "_blank"}
 <a href='https://github.com/konaanitha/IT432GoogleCloudIoTCoreProject/blob/main/Images/create%20table.png' target= "_blank"> Create table.png </a>

## Create a Pub/Sub Topic and Subscription
&emsp;&emsp;Pub/Sub is a real time messaging service  used for ingesting data. It is perfect for handling incoming IoT messages and then allowing downstream systems to process them.Subscription allow other Google Cloud services to access these messages.
1. From the **Cloud Console --> Select Pub/Sub-->  Topics.**
2. If  you see Enable API prompt, click the **Enable API button.**
3. Select **Create Topic** and enter 'heartratedata' as topic name  and click **Create.**
4. Create a Subscription for the topic by clicking on the three dots to create a new subscription-->**Create Subscription.** 
5. Enter the Subscription name 'heartratedata'.
 
We have now The Pub/Sub subscription to pull Iot messages from.

## Use a Dataflow Template
&emsp;&emsp;Dataflow is cloud based data processing service used for batch and real time data.A Dataflow template will be used to create a process that monitors a Pub/Sub topic for incoming messages and then moves them to BigQuery. The data from the Dataflow will be stored in temporary file,and the location will be provided in Cloud Storage.

 **To Create a file in Cloud Storage:**
* From the Cloud Console Menu Select **Storage-->Browser -->click on Create Bucket.**
* Enter the **Name** of the bucket . The Bucket name is unique across the Google Cloud.
* Select the region where your project resides and click **Create Bucket** button.

 **To Create a Dataflow Job:**
* From the Cloud Console Select Dataflow -->Jobs.
*  Click on on **Create Job from Template.**
*  Enter 'heart-streaming'as Job name.
*  Select the region make sure it matches the region where the project resides.
*  Select the dataflow template as **'Pub/sub Subscription to Big Query’.**
*  Enter the details in the other fields ,making sure they align with the name of the Pub/Sub subscription,BigQuery dataset and tablename and Cloud Storage file.
*  Click on **RUN JOB.**

The Dataflow job has started and it made a connection between Pub/Sub and BigQuery.

## Create IoT Core Registry
&emsp;&emsp; Google cloud Iot core is a fully managed service which is used for securely connecting and management of IoT devices. It is a gateway to Google Cloud Platform.
* From the **Cloud Console --> IoT Core.**
* If you see Enable prompt ,click Enable API button.
* Create a Registry for the IoT device. 
* Enter 'heartrate' for the RegistryID.
* Select Region ,disable HTTP in Protocol section.
* Select the Pub/Sub topic which is created in Pub/Sub topic earlier and click on **Create** button.

The Registry is now ready for the devices to be added.

## Adding device to Registry
&emsp;&emsp;From the Cloud Console , Select IoT Core
* Click on the **Devices** tab and Click **Create A Device**.
* Enter 'raspberryHeartRate' as DeviceID.
* For Public key Format select **ES256.**
* We can choose either manual,copy and paste the value of the key or upload the public key file.

 The following commands are used to generate ES 256 key pair in Google CLoud Shell
 
 > openssl ecparam -genkey -name prime256v1 -noout -out ec_private.pem
 > 
 > openssl ec -in ec_private.pem -pubout -out ec_public.pem
  
  Once the Keys are generated, open the editor, copy the public key and add to the authentication section of the device.
  
  ## Configure the Raspberry PI:
  &emsp;&emsp; The following are the steps followed in configuring the Pi
  1. Connect the monitor,keyboard,mouse, heartrate Sensor and finally power adapter.
  2. After the Pi boots up,select the Raspian operating system .Select the desired language and install it.
  3. Click on the WI-FI icon --> select a network and enter the password for the network. 
  4.  Click on the Raspberry Icon-->Preferences-->Raspberry Pi Configuration.
  5.  Select **Interface** tab and enable **SSH**.
  6.  From the Localization tab, set the Locale and TimeZone.
  7.  Allow the Pi to Reboot.
  8.  Make sure all of the software on the Pi is upto date.
  9.  Open the terminal and type 'Ifconfig' command, which gives the IP address of the Pi.
  10.  Install Putty in your local machine and make a connection to Raspberry Pi wireless by typing the IPaddress of Pi in the host name or Ip address.
  
  ## Start the Data
  ### Getting Streaming data from a Raspberry Pi
  &emsp;&emsp; After establishing the connection of Pi from the local machine using Putty enter Username and password.
  * First, move to the home directory of Raspberry pi with the following:		
  
     > cd /home/pi/iotcore-heartrate 
     > 
   * Run the following script by changing to which match the project.  
   
   >
   > **python checkHeartRate.py --project_id=myproject --registry_id=myregistry --device_id=mydevice**
   > 

 * After sucessful execution, a terminal window with the heart rate data results will be seen every 10 seconds.

  ## Check the Data is Flowing
  &emsp;&emsp;We need to make sure that the data is flowing into BigQuery Table.
  * From the Cloud Console Menu -->Select BigQuery .
  * Click on the arrow next to Project name, click on the Dataset, then on the table.
  * Click on the **Query Table** button.
  * Run an SQL statement , that selects all the data from the BigQuery table.
  *  Click **RUN QUERY** button.

 If you see the results then the data is flowing.
 
  ## Visualize the data
   &emsp;&emsp;The Query results ,which  are retrieved from RUN Query can be saved in either EXcel file or Google sheets by clicking 'SAVE RESULTS'.
   * Highlight the two columns that cointain the time collected and heartrate. 
   * Select Insert and select chart 'Clustered Column Chart'.
   * The chart should now display a visualization of heart over time.

 ## Summary:
 &emsp;&emsp; In this, I have used Google IOt core , a fully managed device to secure IoT devices , the messages which are streamed form the IoT device are published in Pub/Sub topic . I created a Dataflow job from Template , that creates a Pipeline stream which reads the messages from the Pub/Sub and writes into BigQuery Table.The Query results from the BigQuery  table are saved into Excel or Google sheets for quick data visualisation.


   



  








