# Introduction

As a developer, I often find myself engrossed in my work, losing track of time and the world around me. This intense focus, while beneficial for my work, has led to a recurring issue in my personal life - managing my wood-burning fireplace!

My home office is located off the gallery of my house, with the fireplace situated in another room, out of sight. I frequently forget to add more wood to the fire, causing it to go out. Also, sometimes I add wood but forget to close the vent, causing the fire to burn too hot and consume the wood quickly.

These recurring issues led me to seek a solution that would allow me to monitor and control the fireplace without needing to constantly check on it physically. As a software developer, I decided to leverage my skills and create a solution that would not only solve my problem but also provide an interesting and challenging project.

Thus, the idea for this fireplace temperature monitoring system was born. The system combines hardware and software to monitor the temperature of the fireplace in real-time, alert me when the temperature reaches certain thresholds, and allow me to control the fireplace remotely. This project has not only provided a practical solution to my problem but also served as a fascinating exploration of the intersection of software development, hardware, and everyday life.

# FirePlaceMonitor App Overview
The fireplace management App, is therefore a project of my passion for blending technology with everyday comfort. I've designed this application using the powerful ESP8266 Wemos D2 R1 Mini and the DS18B20 temperature sensor shield, creating a seamless blend of hardware and software that offers an intuitive user experience.

With the FirePlaceMonitor App, I've made it possible for you to monitor your fireplace's temperature in real-time. The dynamic web dashboard, a feature I'm particularly proud of, updates instantly with every new temperature value received from the server, ensuring you always have the most accurate data at your disposal.

But I didn't stop there! I've integrated Fuzzy Logic into the app, an advanced algorithm that analyzes the temperature data and determines the state of your fireplace. It alerts you when the temperature is too hot, too cold, or changing, taking the guesswork out of maintaining the perfect fire.

And for the finishing touch? I've incorporated Text-to-Speech (TTS) alerts into the app, providing audible notifications based on the fireplace's temperature conditions. You can even customize the TTS messages and temperature thresholds to suit your preferences.

In essence, the FirePlaceMonitor App is more than just a temperature monitoring tool, making it possible to manage your fireplace efficiently and effectively. 

# Functional Specification Document

**Project Overview**

The project is a solution for monitoring the temperature of a wood-burning fireplace. The system is designed to alert the user when the temperature reaches certain thresholds, preventing the fire from going out or becoming too hot. The system uses a Wemos D1 R1 Mini connected to a DS18B20 temperature sensor, a Node.js server, and a web-based dashboard for real-time temperature monitoring.

# System Components

 ![FirePlaceMonitor Model ](https://github.com/thebacons/FirePlaceMonitor/blob/main/Slide2.JPG)
 
## Wemos D1 R1 Mini and DS18B20 Temperature Sensor

The Wemos D1 R1 Mini is a WiFi capable microcontroller. It is connected to a DS18B20 temperature sensor, which measures the temperature of the fireplace. The microcontroller sends the temperature data to the Node.js server over WiFi.

## Node.js Server

The Node.js server receives temperature data from the microcontroller. It uses a fuzzy logic algorithm to analyze the temperature data and determine the state of the fireplace. The server can trigger Text-to-Speech (TTS) messages based on the following conditions:

-   The temperature is too hot
-   The temperature is too cold
-   The temperature is increasing
-   The temperature is decreasing

The server also provides a web interface for controlling the LED on the microcontroller and setting custom TTS messages and temperature thresholds.


## Web Dashboard and Node.js Server Interaction

The web dashboard is a crucial component of the system, providing a user-friendly interface for real-time temperature monitoring and control. It is implemented using HTML, CSS, and JavaScript, with D3.js library used for creating the dynamic temperature chart.

The dashboard is served by the Node.js server and communicates with it using WebSockets, a protocol that provides full-duplex communication channels over a single TCP connection. This allows for real-time, bidirectional communication between the server and the client.

The interaction between the web dashboard and the Node.js server via WebSockets is a key aspect of the system. It allows for real-time temperature monitoring and control, providing a responsive, user-friendly interface for the user. The use of D3.js for the temperature chart enables dynamic, data-driven visualization of the temperature data.

A node.js web dashboard provides a real-time visualization of the temperature data. It displays a line chart of temperature over time, with the x-axis representing time and the y-axis representing temperature. The chart includes minor and major subdivisions on the axes, and it updates in real-time as new temperature data is received. The dashboard also displays the current temperature and a placeholder message when waiting for the first temperature reading.

A webpage connects to the Node.js server and obtains the temperature sensing readings from node.js server, which were relayed from the Wemos D1 R2 Mini device that is connected to the DS18B20 temperature sensor shield. 

The WebPage connects via webSockets to receive the temperature reading in JSON. These are the main elements of the webpage. 

### WebSocket Connection

When the web dashboard is loaded in a browser, it establishes a WebSocket connection to the Node.js server. This connection is initiated by the client (the web dashboard) using the WebSocket API:

``var  socket  =  new  WebSocket('ws://192.168.188.142:8081/client');``

The server listens for incoming WebSocket connections and handles them using the  `ws`  library. When a connection is established, the server can send data to the client, and the client can send data to the server over the same connection.

### Real-Time Data Communication

The Node.js server continuously receives temperature data from the microcontroller. When new data is received, the server sends it to the web dashboard over the WebSocket connection:

``socket.send(JSON.stringify({temperature:  data.temperature}));``

On the client side, the web dashboard listens for incoming messages from the server. When a message is received, it updates the current temperature display and the temperature chart:

``socket.onmessage  =  function(event)  { var  data  =  JSON.parse(event.data);``

### Dynamic Chart Update

The temperature chart is implemented using D3.js, a powerful library for creating data-driven documents. The chart is updated in real-time as new temperature data is received from the server.

When a new data point is received, it is added to the temperature data array, and the chart is redrawn to include the new data point. D3.js handles the creation, update, and removal of elements based on the data, allowing for efficient, dynamic updates of the chart.

### Dashboard Overview

The interaction between the web dashboard and the Node.js server via WebSockets is a key aspect of the system. It allows for real-time temperature monitoring and control, providing a responsive, user-friendly interface for the user. The use of D3.js for the temperature chart enables dynamic, data-driven visualization of the temperature data.

A node.js web dashboard provides a real-time visualization of the temperature data. It displays a line chart of temperature over time, with the x-axis representing time and the y-axis representing temperature. The chart includes minor and major subdivisions on the axes, and it updates in real-time as new temperature data is received. The dashboard also displays the current temperature and a placeholder message when waiting for the first temperature reading.

A webpage connects to the Node.js server and obtains the temperature sensing readings from node.js server, which were relayed from the Wemos D1 R2 Mini device that is connected to the DS18B20 temperature sensor shield. 

The WebPage connects via webSockets to receive the temperature reading in JSON. These are the main elements of the webpage. 

Chart.js Library: The script tag ```<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>``` is used to include the Chart.js library in your webpage. Chart.js is a popular JavaScript library for creating charts. It's loaded from a CDN (Content Delivery Network), which is a network of servers that deliver the library to your webpage.

### User Interaction

The user interacts with the system through the web dashboard. They can view the current temperature and the temperature history on the chart. They can also control the LED on the microcontroller and set custom TTS messages and temperature thresholds through the web interface provided by the Node.js server.

When the temperature reaches certain thresholds, the server triggers TTS messages to alert the user. This allows the user to take appropriate action, such as adding more wood to the fire or closing the vent, to maintain the desired temperature.

## EdgeTTS Configuration
The TTS functionality provides audible alerts based on the temperature conditions of the fireplace, enhancing the user experience and usability of the system. The use of the EdgeTTS library and the Microsoft Edge Text-to-Speech API provides high-quality TTS with a variety of voices and languages, and the ability to customize the TTS to suit the user's preferences.

The EdgeTTS instance is configured with various options that control the voice, language, output format, and other aspects of the TTS functionality:

``const  tts  =  new  EdgeTTS({voice:  'en-GB-RyanNeural', lang:  'en-GB', outputFormat:  'audio-24khz-96kbitrate-mono-mp3', saveSubtitles:  true,});``

-   `voice`: This option specifies the voice to be used for the TTS. In this case, 'en-GB-RyanNeural' is used, which is a British English voice provided by Microsoft.
-   `lang`: This option specifies the language to be used for the TTS. In this case, 'en-GB' is used, which stands for British English.
-   `outputFormat`: This option specifies the format of the audio output. In this case, 'audio-24khz-96kbitrate-mono-mp3' is used, which is a high-quality mono MP3 format.
-   `saveSubtitles`: This option, when set to true, enables the saving of subtitles for the spoken text.

These options can be changed to configure the TTS to use different voices, languages, and output formats, providing flexibility and customization for the TTS functionality.

## Conclusion

This system provides a comprehensive solution for monitoring and controlling the temperature of a wood-burning fireplace. It combines hardware, software, and web technologies to provide real-time temperature monitoring, alerts, and control capabilities.


