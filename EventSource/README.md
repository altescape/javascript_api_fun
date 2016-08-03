
# EventSource

Running updates.php on a local server will output a stream of data a bit like the following:

```
event: ping
data: {"time": "2016-08-03T15:17:50+0100"}

event: ping
data: {"time": "2016-08-03T15:17:51+0100"}

data: This is a message at time 2016-08-03T15:17:56+0100

...
```

Every second it this script will output an event which is a line of data.
The default event type is 'message' but here we also have another event called 
ping and the data it provides is a JSON object containing the current time.

For ease enter following into a dev console, but you can add it anywhere, the key to it all is the `updates.php` source:

```JavaScript
let pingHandler = function(e) { console.log(e); }
let source = new EventSource('updates.php');
source.addEventListener('ping', pingHandler, false);
```
also provides a method: `onmessage` which listens out for default `message` type...

```JavaScript
source.onmessage = function (event) {
  console.log(event.data);
};
```

You can have more than one event by outputting this:
```
event: ping
data: {"time": "2016-08-03T15:17:51+0100"}

event: pong
data: {"time": "2016-08-03T15:17:51+0100"}
```
You would then add:

```JavaScript
source.addEventListener('pong', pongHandler, false);
```

and the associated function `pongHandler` not show here.


More info at https://www.w3.org/TR/eventsource/
