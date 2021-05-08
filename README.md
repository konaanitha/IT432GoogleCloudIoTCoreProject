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

### 1. Select/Create a project.
&emsp; &emsp; You can use default project ("My First Project") or create a new Google Cloud project on the project selector page. Through the project, you can have access to all the resources of Google Cloud Platform. Create a Project with the name 'IoT-heartrate’, The project ID is unique name across the Google Cloud.

&emsp; &emsp; Next, enabling the APIs of the Pub/Sub, IoT Core, Dataflow, Compute Engine, which are used in this project. To enable APIs, select and click on APIs & Services from Cloud Console menu. Search for the <b> Cloud Pub/Sub API </b> and click on the result and <b>Enable API</b>. Follow the same steps for the other above mentioned APIs.
