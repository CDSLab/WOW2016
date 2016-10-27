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
<img width="1110" alt="wow-mic" src="https://cloud.githubusercontent.com/assets/7436221/19613048/fc732056-979e-11e6-9c76-3336f374c751.png">
Click "Record Audio" and wait for it to go red before you speak, then click it again to stop recording.  Don't worry about the Node-RED server URL yet; you will use that later in this lab.

The Watson text-to-speech service produces natural-sounding speech from input text with appropriate cadence and intonation and also supports a variety of languages.

Learn more about Watson-powered STT and TTS at these links: http://www.ibm.com/watson/developercloud/speech-to-text.html
https://www.ibm.com/watson/developercloud/text-to-speech.html

#### The Weather Company Data service

The Weather Company Data Service from Bluemix lets you integrate weather data from The Weather Company into your IBM Bluemix application for any specified geolocation.  The service supports real-time as well we forecasts and historical weather data.  The Weather Company was acquired by IBM in 2015 and is the world's largest private weather enterprise, delivering up to 26 billion forecasts daily.  TWC powers top weather apps on all major mobile platforms, so you have likely used it before, "weather" you knew it or not.

#### Alchemy News service

The Alchemy Data News service indexes hundreds of thousands of articles and blogs every day, analyzes the text with machine learning algorithms, and makes those articles searchable across a variety of fields, including concept and sentiment.  API documentation for the Alchemy News service is located here:

http://docs.alchemyapi.com/docs

## Setup Instructions

Now let's build our application!

1. If you haven't already, create a Bluemix account at https://console.ng.bluemix.net/.  You will be asked to select a unique name for your organization and space where you would like to host the application that you will build today.

2. Click on catalog to get various options of boilerplate code. Select Node-RED.
<img width="1180" alt="Landing" src="https://cloud.githubusercontent.com/assets/7436221/19538326/60742c00-9608-11e6-897b-9efd7ba25a22.png">

3. Name the application and click on **Create**.
<img width="1176" alt="select node-RED" src="https://cloud.githubusercontent.com/assets/7436221/19538333/64ce84f8-9608-11e6-9b94-9b3249c8819b.png">

4. Your application will start running. The app will have cloudant database by default to store node red metadata.
<img width="1140" alt="view app" src="https://cloud.githubusercontent.com/assets/7436221/19539588/fdc0d926-960e-11e6-9b97-0ed1d4c4f51a.png">

5. Click on **Overview** tab to see the detailed view of your application.
<img width="1143" alt="overview" src="https://cloud.githubusercontent.com/assets/7436221/19539543/c21fc422-960e-11e6-9cae-0825da0431a8.png">

6. Click on Connections tab to add two more services.
    1. `Weather Company Data`
    2. `Text to Speech`

 <img width="669" alt="screen shot 2016-09-30 at 5 46 53 pm" src="https://cloud.githubusercontent.com/assets/7436221/19010514/3082de1e-8736-11e6-9216-b96b7d2bfae4.png">
 <img width="852" alt="text" src="https://cloud.githubusercontent.com/assets/7436221/19589060/cc4bf5fe-971e-11e6-9bcd-370b5a021011.png">

7. Restage the application after adding each service.
<img width="606" alt="restage" src="https://cloud.githubusercontent.com/assets/7436221/19589090/09c06c94-971f-11e6-85f5-1f901849f9ea.png">

8. Click on the **View App** of your application. You will be taken to **NODE-RED**
<img width="1140" alt="view app" src="https://cloud.githubusercontent.com/assets/7436221/19589130/4acc192c-971f-11e6-8054-b0aee8c278d5.png">

9. Click on this button to go into Node-red editor.
<img width="1145" alt="screen shot 2016-09-30 at 3 22 06 pm" src="https://cloud.githubusercontent.com/assets/7436221/19008682/c2fab772-8721-11e6-9c58-6dd0d8ebde3e.png">
<img width="1147" alt="screen shot 2016-09-30 at 3 23 58 pm" src="https://cloud.githubusercontent.com/assets/7436221/19008712/0cb77328-8722-11e6-8489-6cd007d4ef2f.png">

10. Copy flows from this github repository and import in your Node-red editor like below.
    1. Import [Main Flow](https://github.com/CDSLab/WOW2016/blob/master/main.json)
    2. Import [Weather Flow](https://github.com/CDSLab/WOW2016/blob/master/weather.json)
    3. Import [News Flow](https://github.com/CDSLab/WOW2016/blob/master/news.json)

<img width="533" alt="screen shot 2016-09-30 at 5 31 54 pm" src="https://cloud.githubusercontent.com/assets/7436221/19010403/425c31fa-8734-11e6-9442-69010121a7d2.png">

#### Nodes in Node-RED Editor
11. Click on the "text to speech" node and select "US English" on language dropdown.
![](https://cloud.githubusercontent.com/assets/8397737/19015255/ab039ce4-87b5-11e6-865b-7a7c26b3c2eb.png)
<img width="494" alt="screen shot 2016-09-30 at 6 17 16 pm" src="https://cloud.githubusercontent.com/assets/8397737/19015276/0a02475e-87b6-11e6-866d-8892ab17b39d.png">

12. The "name" field can be left blank. Finally, click on the each link node on the main tab.
<img width="174" alt="screen shot 2016-10-01 at 8 57 21 am" src="https://cloud.githubusercontent.com/assets/8397737/19015290/3f16b920-87b6-11e6-96d5-1412e6451f75.png">

13. Connect to the proper receive node.
    1. `Outgoing weather should connect to Incoming weather and`
    2. `Outgoing news should connect to Incoming news`
<img width="500" alt="screen shot 2016-10-01 at 9 06 17 am" src="https://cloud.githubusercontent.com/assets/8397737/19015294/57df73e8-87b6-11e6-91bc-0e5a41068ffa.png">

14. Click on **Deploy**.
<img width="241" alt="deploy" src="https://cloud.githubusercontent.com/assets/7436221/19590618/aba19a12-9727-11e6-83bf-498b85583ab6.png">

## Speech to text Microphone application
- We are using another Bluemix application to record our message and send it to our node-red app. Check the link below.
```
https://wow-mic.mybluemix.net/
```

- Note that if you have time / interest, you can also clone this code yourself and host it on Bluemix (you will also need to create and connect the Watson "speech to text" service to it):
https://github.com/CDSLab/WOW-mic

To use the microphone client app, simply enter your Node-RED application link in the text box shown, as:
<--host name-->.mybluemix.net
<img width="622" alt="server url" src="https://cloud.githubusercontent.com/assets/7436221/19613077/2c8388b2-979f-11e6-9a3d-0a5d3ead6eff.png">

Example: watsonkg.mybluemix.net
Click on **Record Audio** to record your message eg.

```
What is the current weather in Chicago.
```
Stop recording and upload it to **Node-RED** by clicking on the "Upload to Node-RED" button.

If the URL you entered is wrong, an error message will pop up like below:
<img width="418" alt="error" src="https://cloud.githubusercontent.com/assets/7436221/19613241/2f0d1584-97a0-11e6-91d4-d7a30512369a.png">

If everything works, you will receive a voice response (turn up your speakers).

Questions currently supported are:

- What is the [current] weather in (location) ?
- What is the weather forecast for (location) ?
- Give me [ positive | negative ] news about (topic for title search)

## Application Flow Details

Now we will study each flow a little further to understand more fully how this application works.

#### Main Application Flow
<img width="1059" alt="flow" src="https://cloud.githubusercontent.com/assets/7436221/19576366/9ae31918-96c7-11e6-8d7d-4c14e2857df1.png">

**Explanation**: Text is passed in via a REST endpoint.  Then we feed that into a function node which calls decodeURIComponent to remove the URL format of the text.  That text is then fed into a switch statement which routes traffic to the news or weather flows based on if the input text contains "news" or "weather" keyword.  If the text contains "read it", then the flow grabs the last requested news article from Cloudant and flows that into the text-to-speech node.  If the text does not contain any recognized keywords, then pin 4 goes to a "format speech" node which formulates a catch-all response, "I don't understand what you meant".

#### Weather Application flow
<img width="1004" alt="weather" src="https://cloud.githubusercontent.com/assets/7436221/19588839/3b145226-971d-11e6-945e-869228e131bd.png">

**Explanation**: This flow is triggered when the user asks for the weather.  The first thing that needs to be determined is the precise location that is being requested.  The first node in this flow, "Construct URL", is a function node that gets ready to call the Google maps API.  Open it up (double-click) and you will see some javascript that first parses the incoming text and scrapes the word(s) after "in" or "for" - this is assumed to be the location requested.  A string URL is created and passed as msg.url that will ask Google for more information about that location, including the latitude and longitude coordinates.  That URL is then fed into the http request node which returns the response from google.  The response is a string manifestation of JSON, so the next node will convert that string into parseable JSON.  

Next we have some error checking.  The "Error check google API results" checks if zero results are returned from Google -- if so, a response is generated for the assistant to say that the location is not recognized.  But if results are returned, then a function node parses the JSON to extract the latitude and longitude coordinates.  Then the text transcription is parsed further to determine if "current" or "forecast" is requested, and that goes to the appropriate weather node which is pre-configured to return either the current weather or the forecast.  The JSON response from the weather node (which calls the weather service) is then parsed and wrapped inside an English response which then goes to the "text to speech" node which returns a wav in the payload.  Finally an audio html tag is added to the response and sent back with the wav as the http response, which allows the browser client to play the audio.

#### News Application flow
<img width="796" alt="news" src="https://cloud.githubusercontent.com/assets/7436221/19588840/40e036f2-971d-11e6-8784-dbcc8d861a69.png">

**Explanation**: This flow gets triggered when the user asks for news. In "construct msg.query", incoming text is parsed to build a query to pass to the Alchemy News service via the News node.  Anything after "about" is set as the title search field, and if you want news articles with "positive" or "negative" sentiment, that is configured as well.  

More options passed to the News node include: `start=now-1d&end=now` which requests news articles from the last 24 hours and `rank=high` which requests popular articles from reputable sources.  Debug nodes are placed before and after the call to the News node so you can see the input and outputs to the News service in the Debug panel.

The response received from the News node is parsed and formatted and sent to the text-to-speech node and then returned as audio in the http response.

You will also notice another wire flowing out of the News node and going to Cloudant.  That flow writes the text from the news article and persists it to a Cloudant database incase the says "Read it!".

If you so wish, you can try to modify the query parameters passed into the news node, for example, you could change `start=node-1d` to `start=node-1h` for fresher news updates.  Or you could play with the sentiment thresholds.  Or there are many other options you could use to filter and search for articles, the API documentation is located at this link:

http://docs.alchemyapi.com/docs

### I got everything working, now what ?

This is your application to modify and extend as you wish!  We recommend that you experiment and start with small changes.  For example, toggle the voice from male to female, or modify the text responses that are returned.  Later maybe you could add a whole new category of question with a new flow and even hook it up to other Bluemix services.  Your imagination is the limit!
