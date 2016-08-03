
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

Every second it will output a segment of data.

The event is ping and the data is a JSON object containing current time.

For ease enter this into the console, but you can add it anywhere, the key to it all is the `updates.php` source:

```JavaScript
let pingHandler = function(e) { console.log(e); }
let source = new EventSource('updates.php');
source.addEventListener('ping', pingHandler, false);
```
also provides a method: `onmessage`...

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

and the associated function `pongHandler` obbiously.


More info at https://www.w3.org/TR/eventsource/
