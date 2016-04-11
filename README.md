# test
```
_initPresenceChannel(store) {
    this.rtm.subscribe("presence", {}, (data) => store.dispatch(data));

    setInterval(() => {
	    if (loggedIn(store)) {
		    let user = store.getState().me.toJS();
			this.rtm.publish("presence", updatePresence(user));
		}
	}, PRESENCE_INTERVAL);
}
// [app/actions/rtm.js lines 105-112]
```

## Authentication and Private Channels

### Authentication works by the following process:

* Client uses Google Sign-In to authenticate with Google via the Google API Client Library through the CAS and obtain a token (click *Sign in with Google*, click *Allow* and, if necessary, enter Google email and password). 
The RTM Service uses the token to authorize publishing and subscribing to the private channel.
* Client attempts to subscribe to its private channel *private.<email>*.
* RTM Service sends the token to the CAS and requests permission to publish and subscribe to the private channel.
* CAS authorizes access to the private channel using the email from the token.

*Note:* If the CAS is not available, authentication with Google fails but you can use all other application features. CAS-specific code is at CAS code is at `cas/src/main/java/com/machinezone/mzchat/CASService.java`.

The following code shows the part of the authentication process:

```
	this._authenticate(me).then(() => {
		let rtmChannelName = this.privateChannelName(currentUserEmail);
		let ondata = (data) => store.dispatch(data);
		return this.rtm.subscribe(rtmChannelName, CHANNEL_OPTS, ondata);
	})
	.then(() => store.dispatch(authenticate()))
	.catch((err) => {
		console.log("User is not authenticated in rtm");
		console.log(err);
	});

// [app/actions/rtm.js lines 129-138]
```

