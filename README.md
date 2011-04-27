Porthole is a small library for secure cross-domain iFrame communication.

## Usage
Include the javascript.

	<script type="text/javascript" src="porthole.js"></script>

Create your content iFrame. This is where the guest content lives. Make sure to give it a name.
	<iframe id="guestFrame" name="guestFrame" src="http://other-domain.com/"></iframe>

Define an event handler if you want to receive messages.

	function onMessage(messageEvent) {  
		/*
			messageEvent.origin: Protocol and domain origin of the message
			messageEvent.data: Message itself
			messageEvent.source: Window proxy object, usefull to post a response 
		*/
	}

Create a window proxy object.

	var windowProxy;
	window.onload=function(){ 
		// Create a proxy window to send to and receive message from the guest iframe
		windowProxy = new Porthole.WindowProxy('http://other-domain.com/proxy.html', 'guestFrame');

		// Register an event handler to receive messages;
		windowProxy.addEventListener(onMessage);
	};

Create a window proxy object in the iFrame.

	var windowProxy;
	window.onload=function(){ 
		// Create a proxy window to send to and receive message from the parent
		windowProxy = new Porthole.WindowProxy('http://parent-domain.com/proxy.html');

		// Register an event handler to receive messages;
		windowProxy.addEventListener(function(event) { 
			// handle event
		});
	};

Send a message.

	windowProxy.postMessage('supersizeme');	

## Unit Tests
	rake jasmine

## Demo
<http://sandbox.ternarylabs.com/porthole/>

## Documentation
<http://ternarylabs.github.com/porthole/>