uMatrix requires the following permissions to work properly:

    "permissions": [
        "browsingData",
        "cookies",
        "privacy",
        "storage",
        "tabs",
        "unlimitedStorage",
        "webNavigation",
        "webRequest",
        "webRequestBlocking",
        "<all_urls>"
    ],

* [**browsingData**](https://developer.chrome.com/extensions/browsingData): to allow [clearing the browser cache](http://developer.chrome.com/extensions/browsingData#method-removeCache).
* [**cookies**](https://developer.chrome.com/extensions/cookies): to allow the report and removed blocked cookies.
* [**privacy**](https://developer.chrome.com/extensions/privacy) ([introduced in 0.9.1.2](https://github.com/gorhill/uMatrix/commit/bbfef4f6cfa6ffe3697fc40ba39fd1b19d54eb01)): for uMatrix to be able to disable the setting _"Prefetch resources to load pages more quickly"_. This is to ensure your IP address do not leak to the remote servers of blocked network requests.
* [**storage**](https://developer.chrome.com/extensions/storage): to store your own whitelist/blacklist domains/objects and all other settings.
* [**tabs**](https://developer.chrome.com/extensions/tabs): to enable forcing a reload of the content of a tab (when the content of the whitelist/blacklist change).
* [**unlimitedStorage**](https://developers.google.com/chrome/whitepapers/storage#unlimited): to allow a user to update various assets used by uMatrix (like preset blacklists, preset recipes, etc.) by fetching the latest versions from Github and saving them locally.
* [**webNavigation**](http://developer.chrome.com/extensions/webNavigation): to listen to [onBeforeNavigate](http://developer.chrome.com/extensions/webNavigation.html#event-onBeforeNavigate) events in order to set up HTTPSB's internal data structure for a specific web page.
* [**webRequest**](http://developer.chrome.com/extensions/webRequest): to allow intercepting all requests in order to inspect them.
* [**webRequestBlocking**](http://developer.chrome.com/extensions/webRequest#manifest): to be able to block a request if the object of the request is blacklisted.
* `<all_urls>`: to be able to inspect network requests for all URLs (`http:`, `https:`, `ws:`, `wss:`, `data:`, etc.) -- necessary in order to decide whether a block directive should be enforced)