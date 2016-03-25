This demo application utilizes RTmessaging, the cutting-edge publish-subscribe messaging engine at the heart of RTPlatform, a platform built by Machine Zone for extreme scale,  performance, and reliability. The RTM Service utilizes the publish-subscribe messaging pattern to connect client applications through the RTM Service WebSocket endpoint.

[TBD: disclaimer legal text about if you can download and use this application]

## About Sky Traffic ##

Sky Traffic is a logistical geolocation and geomapping web application, designed to showcase the power of the RTmessaging used in conjunction with other external services to develop real-time applications. Created with the RTPlatform JavaScript SDK and the Google Maps API, this application shows the location of every flight in the world on a single map in a browser window.

## How It Works ##

Sky Traffic consumes a real-time data feed that publishes the data for a flight to a single channel on the RTM endpoint. Sky Traffic subscribes to that channel. When the application receives a new message (on average, 10 per second), it updates the map with the received flight data. As a result, you can see every flight, its flight number, and its progress as it is updated in real-time. At the heart of the application, RTmessaging processes the data feed and uses the Google Maps API to display the results.

## The Code ##

The bulk of the application is the Google Maps API drawing and updating the map. The following code samples show how you can harness the power of RTmessaging with only a few lines of code of the JavaScript SDK.

### Connect to RTmessaging ###
```javascript
this.client = MZ.RTM.create(appKey);
// [SkyTraffic.js, line 11]
```
### Process Message Data and Draw Plane ###
```javascript
// create a channel
this.channel = this.client.createChannel(channelName);
// define callback
this.channel.on('data', ::this.handleChannelData);
...
handleChannelData(pdu) {
	pdu.body.messages.forEach(data => {
		data['updatedAt'] = Date.now();
		// draw the plane
		this.planes.set(data.aircraft, data);
    });
	this.invalidate();
}
// [SkyTraffic.js, lines 17-18, 56-62]
```
### Subscribe and Get History ###
```javascript
this.channel.subscribe({history: {max_age: 3600}});
// [SkyTraffic.js, line xx]
```

## More Demo Applications ##
<a href="#">Chat App</a><br/>
<a href="#">Social, Collaborative App</a><br/>
<a href="#">Government</a><br/>
<a href="#">Dashboards</a>


## Documentation
<a href="#">RTPlatform Overview</a><br/>
<a href="#">Client SDKs</a>



