User agent strings used for spoofing are not updated automatically, this is your responsibility. Here is a place where you can get the latest ones: <http://techblog.willshouse.com/2012/01/03/most-common-user-agents/>.
And one more: <http://techpatterns.com/downloads/firefox/useragentswitcher.xml>

You should be aware, that if JavaScript is enabled, it is possible to determine the browser and version via feature detection.
https://html5test.com/compare/browser/mybrowser/chrome-43/chrome-42/firefox-38/firefox-37.html

On some sites a user agent strings from a different browser engine can cause problems. Therefore you may prefer browser specific user agent strings.