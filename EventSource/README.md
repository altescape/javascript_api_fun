
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

The event is ping and the data is a JSON object containing current time.

For ease enter this into the console, but you can add it anywhere, the key to it all is the `updates.php` source:

```JavaScript
let pingHandler = function(e) { console.log(e); }
let source = new EventSource('updates.php');
source.addEventListener('ping', pingHandler, false);
```
