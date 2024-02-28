# FirePlaceMonitor
Fireplace monitoring app using the ESP8266 Wemos D2 R1 Mini + DS18B20 temp sensor shield - Node.js - Fuzzy Logic - TTS - Web Dashboards
## The Node.js monitoring Dashboard
A webpage connects to the Node.js server and obtains the temperature sensing readings which are sent from the Wemos D1 R2 Mini device. The WebPage connects via webSockets to receive the temperature reading in JSON. These are the main elements of the webpage. 
Chart.js Library: The script tag <script src="https://cdn.jsdelivr.net/npm/chart.js"></script> is used to include the Chart.js library in your webpage. Chart.js is a popular JavaScript library for creating charts. It's loaded from a CDN (Content Delivery Network), which is a network of servers that deliver the library to your webpage.

**WebSocket Connection:** var socket = new WebSocket('ws://192.168.188.142:8081/client'); creates a new WebSocket connection to the server at the specified URL. WebSockets provide real-time, two-way communication between the server and the client.

**Chart Initialization:** The new Chart() constructor is used to create a new chart. It takes two arguments: a context (in this case, the canvas element with the id temperatureChart), and an object that specifies the configuration of the chart. The configuration object includes the type of chart ('line'), the data for the chart (initially an empty array), and options for the chart (such as the scales for the x and y axes).

**WebSocket Message Event:** The socket.onmessage function is an event handler that's called whenever the client receives a message from the server over the WebSocket connection. The message is expected to be a JSON string that contains a 'temperature' property.

**Updating the Chart:** When a message is received from the server, the temperature value is pushed into the temperatureData array, a new label is added to the chart, and the chart is updated with temperatureChart.update(). This causes the new temperature value to be displayed on the chart.

In summary, this webpage creates a real-time temperature chart that updates whenever it receives a new temperature value from the server. The Chart.js library is used to create and update the chart, and the WebSocket API is used to receive the temperature values from the server.
