Per-scope switches, introduced in version 0.8.1.0, allow a user to customize various settings for a specific scope.

![Per scope switches](https://raw.githubusercontent.com/gorhill/uMatrix/master/doc/img/per-scope-switches.png)

The state of a per-scope switch in a broad scope will be inherited by narrower scopes, unless a more specific rule override the broader rule.

For example, setting the per-scope switch _"User agent spoofing"_ in the global (`*`) scope will cause the user agent information to be spoofed everywhere. However, user agent spoofing could cause a site to not work properly ([example: crowdin.com](https://github.com/gorhill/uMatrix/issues/36)), and it is thus possible to override the global state of the _"User agent spoofing"_ switch by disabling the switch just for the scope where it causes problem.

The per-scope switches layer just like matrix rules layer.

**Important:** The per-scope switches are independent from the matrix filtering switch, meaning that if you toggle off matrix filtering, the per-site switches which are toggled on will still apply. For example, one could turn off matrix filtering while keeping the ability to enforce strict HTTPS.

### The per-scope switches

- [User agent spoofing](#user-agent-spoofing)
- [Referrer spoofing](#referrer-spoofing)
- [Strict HTTPS](#strict-https)

***

### User agent spoofing

User agent spoofing has been transformed from a global setting into a per-scope setting, so that you can now disable/enable it specifically on a per-scope basis.

The setting in the _Privacy_ tab is still there, and its purpose is to control user agent spoofing for the global scope (`*`). Since narrower scopes will inherit the switch state from a broader scope, this means the global scope switch still act as a global setting, difference being that now the switch state can be overridden in a narrower scope.

***

### Referrer spoofing

Similarly, referrer spoofing has been transformed from a global setting into a per-scope setting, so that you can now disable/enable it specifically on a per-scope basis.

The setting in the _Privacy_ tab is still there, and its purpose is to control referrer spoofing for the global scope (`*`). Since narrower scopes will inherit the switch state from a broader scope, this means the global scope switch still act as a global setting, difference being that now the switch state can be overridden in a narrower scope.

The logic behind referrer spoofing is simpler now: it's whether the switch referrer spoofing is turned on, and whether the domain of the referrer URL is third-party to the domain of the request URL. Whether the domain of the URL of a request is whitelisted is now irrelevant.

Also, notice that now I use the term "spoofing". Whereas before the referrer string was blanked, the referrer information will now be foiled using the root URL derived from the URL of the request. For example, if the URL of a request is `http://www.example.com/blahblahblah/boring.html` and the referrer is `http://google.com`, the referrer will be spoofed using the `http://www.example.com/` string.

***

### Strict HTTPS

First, if you are not familiar with what is "mixed content", here are some places to learn more about it:

- [Mozilla Developer Network: Mixed Content](https://developer.mozilla.org/en-US/docs/Security/MixedContent)
- [Qualys Blog: HTTPS Mixed Content: Still the Easiest Way to Break SSL](https://community.qualys.com/blogs/securitylabs/2014/03/19/https-mixed-content-still-the-easiest-way-to-break-ssl)
- [W3C: Mixed Content](https://w3c.github.io/webappsec/specs/mixedcontent/)

When the _"Strict HTTPS"_ switch is turned on, mixed content will be forbidden.

_"Strict HTTPS"_ is more then to just protect MITM attack. Without _"Strict HTTPS"_, data-mining by 3rd-parties can still occur, as evil ISPs like Verizon et al. could still inject tagging information in the HTTP headers of outgoing net requests which are not done through encrypted connections.

Chromium/Firefox forbid **some** mixed content by default. When there is mixed content on a web page, a little shield icon will appear in the address bar, and a user may click on it to load the content which was forbidden from loading natively by the browser. However, as [investigated by a user](https://github.com/gorhill/uMatrix/issues/67), this [does not apply to image, video and audio resources](https://www.bennish.net/mixed-content.html).

With uMatrix 0.9.0.0, unsecure network requests are blocked directly by uMatrix, rather than by the browser through a CSP directive. This means if a page is mixed content, your browser will notify you about the mixed content on that page, though the connections were blocked by uMatrix (use the logger to see for yourself).