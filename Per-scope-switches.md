Per-scope switches, introduced in version 0.8.1.0, allow a user to customize various settings for a specific scope.

![Per scope switches](https://raw.githubusercontent.com/gorhill/uMatrix/master/doc/img/per-scope-switches.png)

The state of a per-scope switch in a broad scope will be inherited by narrower scopes, unless a more specific rule override the broader rule.

For example, setting the per-scope switch _"User agent spoofing"_ in the global (`*`) scope will cause the user agent information to be spoofed everywhere. However, user agent spoofing could cause a site to not work properly ([example: crowdin.com](https://github.com/gorhill/uMatrix/issues/36)), and it is thus possible to override the global state of the _"User agent spoofing"_ switch by disabling the switch just for the scope where it causes problem.

The per-scope switches layer just like matrix rules layer.

### The per-scope switches

Following is a list of the currently existing per-scope switches.

***

### Strict HTTPS

First, if you are not familiar with what is "mixed content", here are some places to learn more about it:

- [Mozilla Developer Network: Mixed Content](https://developer.mozilla.org/en-US/docs/Security/MixedContent)
- [Qualys Blog: HTTPS Mixed Content: Still the Easiest Way to Break SSL](https://community.qualys.com/blogs/securitylabs/2014/03/19/https-mixed-content-still-the-easiest-way-to-break-ssl)
- [W3C: Mixed Content](https://w3c.github.io/webappsec/specs/mixedcontent/)

When the _"Strict HTTPS"_ switch is turned on, mixed content will be forbidden.

To witness _"Strict HTTPS"_ at work, visit the encrypted version of Wired's [Threat Post](https://threatpost.com/), which suffers (at time of writing, 2014-11) from mixed content:

![Mixed content foiled](https://raw.githubusercontent.com/gorhill/uMatrix/master/doc/img/strict-https-at-work.png)

When _"Strict HTTPS"_ is turned on, you can see in the above example the browser refusing to process all non-HTTPS connections -- to `kasperskyhub.staging.wpengine.com` in the above case.

Since the unencrypted connection is not even attempted by the browser, this prevents µMatrix to account for these aborted connection, and thus they won't be reported in the matrix. But you can see them using the developer console.

***

### User agent spoofing


***

### Referrer spoofing
