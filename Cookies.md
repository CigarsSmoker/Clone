Blacklisted cookies are not prevented by uMatrix from entering your browser. However they are prevented from **leaving your browser**<sup>[1]</sup>, which is what really matters. Not blocking cookies before they enter your browser gives you the opportunity to be informed that a site tried to use cookies, and furthermore to inspect their contents if you wish.

Once these blacklisted cookies have been accounted for by uMatrix, you can ask uMatrix to remove them from your browser if you wish so: just check the setting "Delete blocked cookies" in the _Privacy_ tab.

***

[1] This is about standard [HTTP Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cookie) header. Cookies can still be "stolen", and send to remote server by rogue javascript in other data structures (POST request for example). This can be counteracted by blocking such rogue scripts in uMatrix and using specialized cookie-blocking extensions ([#7](https://github.com/uBlockOrigin/uMatrix-issues/issues/7))