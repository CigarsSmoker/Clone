uMatrix requires the following permissions to work properly:

    "permissions": [
        "browsingData",
        "contentSettings",
        "cookies",
        "privacy",
        "storage",
        "tabs",
        "unlimitedStorage",
        "webNavigation",
        "webRequest",
        "webRequestBlocking",
        "http://*/*",
        "https://*/*"
    ],

* [**browsingData**](https://developer.chrome.com/extensions/browsingData): to allow [clearing the browser cache](http://developer.chrome.com/extensions/browsingData#method-removeCache).
* [**contentSettings**](https://developer.chrome.com/extensions/contentSettings.html): to [enable javascript](http://developer.chrome.com/extensions/contentSettings#property-javascript) for all web pages so that uMatrix can fully control execution of javascript using the `Content-Security-Policy: script-src 'none'` header directive.
* [**cookies**](https://developer.chrome.com/extensions/cookies): to allow the removal of blocked cookies.
* [**privacy**](https://developer.chrome.com/extensions/privacy): for uMatrix to be able to disable the setting _"Prefetch resources to load pages more quickly"_. This is to ensure your IP address do not leak to the remote servers of blocked network requests.
* [**storage**](https://developer.chrome.com/extensions/storage): to store your own whitelist/blacklist domains/objects and all other settings.
* [**tabs**](https://developer.chrome.com/extensions/tabs): to enable forcing a reload of the content of a tab (when the content of the whitelist/blacklist change).
* [**unlimitedStorage**](https://developers.google.com/chrome/whitepapers/storage#unlimited): to allow a user to update various assets used by uMatrix (like preset blacklists, preset recipes, etc.) by fetching the latest versions from Github and saving them locally.
* [**webNavigation**](http://developer.chrome.com/extensions/webNavigation): to listen to [onBeforeNavigate](http://developer.chrome.com/extensions/webNavigation.html#event-onBeforeNavigate) events in order to set up HTTPSB's internal data structure for a specific web page.
* [**webRequest**](http://developer.chrome.com/extensions/webRequest): to allow intercepting all requests in order to inspect them.
* [**webRequestBlocking**](http://developer.chrome.com/extensions/webRequest#manifest): to be able to block a request if the object of the request is blacklisted.
* `http://*/*` & `https://*/*`: to be able to inspect HTTP net requests for all URLs (necessary in order to decide whether a block directive should be enforced).