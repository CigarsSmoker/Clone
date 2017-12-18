Per-scope switches allow a user to customize various settings for a specific scope.

![Per scope switches](https://user-images.githubusercontent.com/585534/34109064-6eda7828-e3d0-11e7-922c-99047a298c6e.png)

The state of a per-scope switch in a broad scope will be inherited by narrower scopes, unless a more specific rule override the broader rule.

For example, setting the per-scope switch _"Spoof `Referer` header"_ in the global (`*`) scope will cause the referrer header information to be spoofed everywhere. However, spoofing could cause a site to not work properly, and it is thus possible to override the global state of the _"Spoof `Referer` header"_ switch by disabling the switch just for the scope where it causes problem.

**Important:** The per-scope switches are independent from the matrix filtering switch, meaning that if you toggle off matrix filtering, the per-scope switches which are toggled on will still apply. For example, one could turn off matrix filtering while keeping the ability to forbid mixed content.

### The per-scope switches

- [Forbid mixed content](#forbid-mixed-content)
- [Spoof `Referer` header](#spoof-referer-header)
- [Spoof `noscript` tags](#spoof-noscript-tags)

***

### Forbid mixed content

First, if you are not familiar with what "mixed content" is, here are some places to learn more about it:

- [Mozilla Developer Network: Mixed Content](https://developer.mozilla.org/docs/Security/MixedContent)
- [Qualys Blog: HTTPS Mixed Content: Still the Easiest Way to Break SSL](https://community.qualys.com/blogs/securitylabs/2014/03/19/https-mixed-content-still-the-easiest-way-to-break-ssl)
- [W3C: Mixed Content](https://w3c.github.io/webappsec/specs/mixedcontent/)

When the _"Forbid mixed content"_ switch is turned on, mixed content will be forbidden.

_"Forbid mixed content"_ is more than to just protect MITM attacks. Without _"Forbid mixed content"_, data-mining by 3rd-parties can still occur, as unscrupulous ISPs like [Verizon](https://www.eff.org/deeplinks/2014/11/verizon-x-uidh) et al. could still inject tagging information in the HTTP headers of outgoing network requests which are not done through encrypted connections.

Chromium/Firefox forbid **some** mixed content by default. When there is mixed content on a web page, a little shield icon will appear in the address bar, and a user may click on it to load the content which was forbidden from loading natively by the browser. However, as [investigated by a user](https://github.com/gorhill/uMatrix/issues/67), this [does not apply to image, video and audio resources](https://www.bennish.net/mixed-content.html).

Since uMatrix 0.9.0.0, unsecure network requests are blocked directly by uMatrix, rather than by the browser through a CSP directive. This means if a page has mixed content, your browser will notify you about the mixed content on that page, though the connections were blocked by uMatrix (use the logger to see for yourself).

***

### Spoof `Referer` header

Referer spoofing has been transformed from a global setting into a per-scope setting, so that you can now disable/enable it specifically on a per-scope basis.

The setting in the _Settings_ tab is still there, and its purpose is to control referer spoofing for the global scope (`*`). Since narrower scopes will inherit the switch state from a broader scope, this means the global scope switch still act as a global setting, difference being that now the switch state can be overridden in a narrower scope.

The logic behind referer spoofing is simpler now: it's whether the switch referer spoofing is turned on, and whether the domain of the referer URL is third-party to the domain of the request URL. Whether the domain of the URL of a request is whitelisted is now irrelevant.

Also, notice that now I use the term "spoofing". Whereas before the referer string was blanked, the referer information will now be foiled using the root URL derived from the URL of the request. For example, if the URL of a request is `http://www.example.com/blahblahblah/boring.html` and the referer is `http://google.com`, the referer will be spoofed using the `http://www.example.com/` string.

***

### Spoof `<noscript>` tags

 With uMatrix 1.1.14, user agent spoofing has been [removed](https://github.com/gorhill/uMatrix/releases/tag/1.1.14) and a new switch, spoof `<noscript>` tags has been added, which is on by default.

Since spoofing `<noscript>` is not necessarily _always_ desirable, the global setting can be overridden on a per-scope basis with the _"Spoof `<noscript>` tags"_ switch.

This feature is most useful to users who [block 1st-party scripts by default.](https://github.com/gorhill/uMatrix/wiki/How-to-block-1st-party-scripts-everywhere-by-default)

Note that this might be the long term approach used for enabling `<noscript>` tags: the [approach planned by Firefox](https://bugzilla.mozilla.org/show_bug.cgi?id=1392090) is not really suitable to uMatrix, as this would require to completely disable javascript for a site (causing the matrix ruleset to be disregarded), while with the current approach, one can still enable 3rd-party scripts and yet have the `<noscript>` tags spoofed.