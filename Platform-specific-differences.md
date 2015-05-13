[work in progress]

#### Websockets

Chromium: currently **can not** be blocked.
- Outstanding [Chromium issue 129353](https://code.google.com/p/chromium/issues/detail?id=129353).

Firefox: Upgrade header to websocket **can** be blocked.
- Upgrade requests are reported into the `other` column.
- TO DO: uMatrix should specifically check for requests for connection upgrade to websocket, and report this in the logger.
