[work in progress]

#### Websockets

##### Chromium

Currently **can not** be blocked.

Outstanding [Chromium issue 129353](https://code.google.com/p/chromium/issues/detail?id=129353).

##### Firefox

Requests for connection upgrade to websocket **can** be blocked.

Connection upgrade requests are currently reported into the `other` column.

**TO DO:** uMatrix should specifically check for requests for connection upgrade to websocket, and report this in the logger (just like it currently does for `ping` requests).

##### Test cases

- [Ephemeral Hosting](http://ephemeralp2p.durazo.us2bbbf21959178ef2f935e90fc60e5b6e368d27514fe305ca7dcecc32c0134838> (might not last forever)