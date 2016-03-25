This demo application utilizes RTmessaging, the cutting-edge publish-subscribe messaging engine at the heart of RTPlatform, a platform built by Machine Zone for extreme scale,  performance, and reliability. The RTM Service utilizes the publish-subscribe messaging pattern to connect client applications through the RTM Service WebSocket endpoint.

[TBD: disclaimer legal text about if you can download and use this application]

## About Sky Traffic ##

Sky Traffic is a geo-location web application, designed to showcase the power of the RTmessaging used in conjunction with other external services to develop real-time applications. Created with the RTPlatform JavaScript SDK and the Google Maps API, this application shows the location of every flight in the world on a single map in a browser window.

## How It Works ##

Sky Traffic consumes a real-time data feed that publishes the data for a flight to a single channel on the RTM endpoint. Sky Traffic subscribes to that channel. When the application receives a new message (on average, 10 per second), it updates the map with the received flight data. As a result, you can see every flight, its flight number, and its progress as it is updated in real-time. At the heart of the application, RTmessaging processes the data feed and uses the Google Maps API to display the results.

## The Code ##

The bulk of the application is the Google Maps API drawing and updating the map. The following code samples show how you can harness the power of RTmessaging with only a few lines of code of the JavaScript SDK.

### Connect to RTmessaging ###

