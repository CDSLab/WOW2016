# World of Watson 2016, Lab 3200

### Overview

##### Simplify Your Life with Your Own IBM Watson Personal Assistant
We all lead busy lives, so it can be a challenge to find timely and relevant information. But what if you had a personal assistant to deliver this for you? In this lab, you will build your own cognitive cloud app powered by IBM Watson to deliver news and weather customized for your preferences and location. You will build your own Node.js application deployed to IBM Bluemix and use services from the Watson Alchemy News and the Weather Company. News articles are analyzed for category and sentiment and a real-time weather forecast is delivered for your location. You will interact with your assistant using Watson speech-to-text and text-to-speech services.  In the process of doing all this, you will also learn more about Node-RED, Node.js and Bluemix, as well as some of the services that Bluemix has to offer.

### Technology Overview
![codecamp16](https://cloud.githubusercontent.com/assets/12015008/19007253/c430234c-8718-11e6-8ff9-a328229e018a.png)

#### Node-RED

Node-RED is an open-source visual tool, originated at IBM and now owned by the JS Foundation, that allows you to wire together IoT devices, API's and online services in interesting ways to build applications.  A payload of data in JSON format flows from left to right and travels through a series of nodes that are connected by wires.  Something triggers the flow -- could be an IoT device, or a twitter stream, for example, and then the nodes after it can analyze the data and decide on an action and finally an output node will send data somewhere (for example, to a database, or an alerting system).  This is an overview of how Node-RED works -- You can learn more about Node-RED at [nodered.org](http://www.nodered.org/).

For the application you will be building today, your Node-RED flow will be triggered by a REST call issued by a microphone application that uses Watson to record and translate your voice to text.  That text is then sent to your Node-RED instance via REST call.  Your Node-RED instance will be a hosted application on Bluemix, IBM's PaaS.  We will provide the microphone application, which acts like a client, and you will use Node-RED to build the backend that services the incoming text request and returns a voice response, which will then be played by the client application on your laptop's speaker.  Your application will utilize news, weather and Watson text-to-speech services to create the response.  

While Node-RED can run on many different hardware, including Raspberry Pi, in this lab, you will be working with a special version of Node-RED that is hosted on the cloud with Bluemix and has special nodes that can interface with Bluemix services including Watson services.  If you are interested in learning more about how to build Node-RED applications that interface with Bluemix Watson services, this link has a variety of interesting starter-pack applications.

#### Bluemix

Bluemix is a cloud PaaS (Platform as a Service), which allows you to host your application online and bind it to a variety of SaaS service offerings from IBM including Watson analytic services.  Learn more at http://www.ibm.com/bluemix and if you are new to Bluemix, you can create a trial account at http://www.bluemix.net/ (click "Sign Up").  

#### Watson speech-to-text and text-to-speech services

Watson speech-to-text service converts the human voice into the written word using machine intelligence to analyze the grammar and language structure to generate an accurate transcription in real time.  The transcription of the incoming audio is sent back continuously and corrected as more speech is heard.  In our demo app, you will see confidence scores from Watson assigned to each word along with alternative words that it was considering.

You can try it out in your favorite language at this link -- please use the Chrome browser:

https://wow-mic.mybluemix.net/

Click "Record Audio" and wait for it to go red before you speak, then click it again to stop recording.  Don't worry about the Node-RED server URL yet; you will use that later in this lab.

The Watson text-to-speech service produces natural-sounding speech from input text with appropriate cadence and intonation and also supports a variety of languages.

Learn more about Watson-powered STT and TTS at these links: http://www.ibm.com/watson/developercloud/speech-to-text.html
https://www.ibm.com/watson/developercloud/text-to-speech.html

#### The Weather Company Data service

The Weather Company Data Service from Bluemix lets you integrate weather data from The Weather Company into your IBM Bluemix application for any specified geolocation.  The service supports real-time as well we forecasts and historical weather data.  The Weather Company was acquired by IBM in 2015 and is the world's largest private weather enterprise, delivering up to 26 billion forecasts daily.  TWC powers top weather apps on all major mobile platforms, so you have likely used it before, "weather" you knew it or not.

#### Alchemy News service



### Main Application Flow
<img width="1059" alt="flow" src="https://cloud.githubusercontent.com/assets/7436221/19576366/9ae31918-96c7-11e6-8d7d-4c14e2857df1.png">

### Weather Application flow
<img width="1004" alt="weather" src="https://cloud.githubusercontent.com/assets/7436221/19588839/3b145226-971d-11e6-945e-869228e131bd.png">

### News Application flows
<img width="796" alt="news" src="https://cloud.githubusercontent.com/assets/7436221/19588840/40e036f2-971d-11e6-8784-dbcc8d861a69.png">


## Setup Instructions

1. If you haven't already, create a bluemix account at https://console.ng.bluemix.net/.  You will be asked to select a unique name for your organization and space where you would like to host the application that you will build today.

2. Click on catalog to get various options of boilerplate code. Select Node-RED.

<img width="1180" alt="Landing" src="https://cloud.githubusercontent.com/assets/7436221/19538326/60742c00-9608-11e6-897b-9efd7ba25a22.png">

..Name the app.
..Select a **web** application.

<img width="1176" alt="select node-RED" src="https://cloud.githubusercontent.com/assets/7436221/19538333/64ce84f8-9608-11e6-9b94-9b3249c8819b.png">

- Your application will start staging and will start. The app will have cloudant database by default to store node red metadata.

<img width="1140" alt="view app" src="https://cloud.githubusercontent.com/assets/7436221/19539588/fdc0d926-960e-11e6-9b97-0ed1d4c4f51a.png">








- Select **Overview** tab on the left to see the detailed view of your application.


<img width="1143" alt="overview" src="https://cloud.githubusercontent.com/assets/7436221/19539543/c21fc422-960e-11e6-9cae-0825da0431a8.png">

As we are going to make our own assistance. We can enable it to notify us the temperature/weather of any place on the earth.
For that we need to add a service to this app, which is called "Weather Company Data". So we select Add a service or API button.

 <img width="669" alt="screen shot 2016-09-30 at 5 46 53 pm" src="https://cloud.githubusercontent.com/assets/7436221/19010514/3082de1e-8736-11e6-9216-b96b7d2bfae4.png">

It will create in few minutes and link itself to the existing app.
Now your App has to be **Restaged** to reflect the updation.

- Go back to overview of your App and add another service called "Text to Speech" and restage the application.

- Click on the link of your application. You will be taken to **NODE-RED**
..Here, you can enter into Node-RED Editor to start making flows.
Creating flows makes life easier with just dragging and dropping the functional nodes having code or API calls.
It helps in debugging at each level as well so you know where the bug is located.

<img width="1145" alt="screen shot 2016-09-30 at 3 22 06 pm" src="https://cloud.githubusercontent.com/assets/7436221/19008682/c2fab772-8721-11e6-9c58-6dd0d8ebde3e.png">

Left panel gives a vast range of nodes to drag and connect. This helps to perform functions and make an application running in minutes.


<img width="1147" alt="screen shot 2016-09-30 at 3 23 58 pm" src="https://cloud.githubusercontent.com/assets/7436221/19008712/0cb77328-8722-11e6-8489-6cd007d4ef2f.png">

Three files are added into this github repository. Create three flows.
- Import [Main Flow](main.json)
- Import [Weather Flow](weather.json)
- Import [News Flow](news.json)

<img width="533" alt="screen shot 2016-09-30 at 5 31 54 pm" src="https://cloud.githubusercontent.com/assets/7436221/19010403/425c31fa-8734-11e6-9442-69010121a7d2.png">

Copy each flow from the github file to create flows on you node-red and paste here.

A couple more steps are required to get the application up and running. First click on the "text to speech" node and select "US English"

![](https://cloud.githubusercontent.com/assets/8397737/19015255/ab039ce4-87b5-11e6-865b-7a7c26b3c2eb.png)

<img width="494" alt="screen shot 2016-09-30 at 6 17 16 pm" src="https://cloud.githubusercontent.com/assets/8397737/19015276/0a02475e-87b6-11e6-866d-8892ab17b39d.png">

The "name" field can be left blank. Finnally, click on the each link node on the main tab:


<img width="174" alt="screen shot 2016-10-01 at 8 57 21 am" src="https://cloud.githubusercontent.com/assets/8397737/19015290/3f16b920-87b6-11e6-96d5-1412e6451f75.png">

and connect to the proper receive node:

<img width="500" alt="screen shot 2016-10-01 at 9 06 17 am" src="https://cloud.githubusercontent.com/assets/8397737/19015294/57df73e8-87b6-11e6-91bc-0e5a41068ffa.png">

"Outgoing weather" should connect to "Incoming weather" and "Outgoing news" should connect to "Incoming news"

## Speech to text Microphone application
- We are using another Bluemix application to record our message and send it to our node-red app. Check the link below.
```
https://wow-mic.mybluemix.net/
```

Enter your application link in the text box shown.
<--host name-->.mybluemix.net

And record your message like
```
**What is the current weather in Chicago.**
```
Upload your message and it makes a call to your Node-RED backend application and speaks out the result.
