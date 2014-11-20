Per-scope switches, introduced in version 0.8.1.0, allow a user to customize various settings for a specific scope.

![Per scope switches](https://raw.githubusercontent.com/gorhill/uMatrix/master/doc/img/per-scope-switches.png)

The state of a per-scope switch in a broad scope will be inherited by narrower scopes, unless a more specific rule override the broader rule.

For example, setting the per-scope switch _"User agent spoofing"_ in the global (`*`) scope will cause the user agent information to be spoofed everywhere. However, user agent spoofing could cause a site to not work properly ([example: crowdin.com](https://github.com/gorhill/uMatrix/issues/36)), and it is thus possible to override the global state of the _"User agent spoofing"_ switch by disabling the switch just for the scope where it causes problem.

The per-scope switches layer just like matrix rules layer.

### The per-scope switches

Following is a list of the currently existing per-scope switches.

#### Strict HTTPS

When the _"Strict HTTPS"_ switch is turned on, mixed content will be forbidden.

To witness _"Strict HTTPS"_ at work, visit the encrypted version of Wired's [Threat Post](https://threatpost.com/), which suffers (at time of writing, 2014-11) from mixed content:

![Mixed content foiled](https://raw.githubusercontent.com/gorhill/uMatrix/master/doc/img/strict-https-at-work.png)

When _"Strict HTTPS"_ is turned on, you can see the browser refusing to process all non-HTTPS connections.

#### User agent spoofing


#### Referrer spoofing
