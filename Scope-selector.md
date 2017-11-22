Every rule you create in uMatrix applies to a specific scope. The scope tells uMatrix where a rule should be enforced. For example, you may want to block all network requests to `facebook.com` everywhere by default (`* facebook.com * block`), except when visiting web pages from `facebook.com` (`facebook.com facebook.com * allow`)

 The matrix UI in the popup panel allows you to easily select the scope from which to visualize/create/remove rules, the top-left cell is the scope selector:

![a](https://user-images.githubusercontent.com/585534/33131928-17587830-cf66-11e7-8a69-30902ac4ac87.png)

It is advised that you create rules which apply only for a specific scope, but of course it's convenient that some rules are created in the global scope (`*`) such that you do not have to constantly create the same rules for many sites. For most it's convenient to create `allow` rules in the global scope for domains which use are widespread, and which you trust.

A concrete example. Disqus is a commenting platform which use is quite widespread, so it's a good idea to keep `disqus.com` blocked everywhere by default (which is the case if you keep uMatrix's default settings). However, there might be times where you want to view the comments or use the Disqus commenting widget on a given site. In such case, you would create `allow` rules for that site, as seen below (`lareviewofbooks.org disqus.com * allow`, `lareviewofbooks.org disqus.com frame allow`):

![a](https://user-images.githubusercontent.com/585534/33133068-9c2f35aa-cf69-11e7-9d0b-edd09d36b5bf.png)<br><sup>Sidenote: notice that network requests to `referrer.disqus.com`, `glitter.services.disqus.com`, and `realtime.services.disqus.com` are still blocked despite allowing `disqus.com`. These block rules are loaded from the HOSTS files. This also demonstrates that narrower rules can't be overriden by broader ones.</sup>

However this won't be sufficient to unbreak the Disqus comment widget, because after you allowed 3rd-party `disqus.com`, the Disqus widget is still broken, and now the matrix shows network requests to `disquscdn.com` were blocked.

You could just create one more local `allow` rule for `disquscdn.com` to enable Disqus on the page (`lareviewofbooks.org disquscdn * allow`).

Another approach is to create an `allow` rule for `disquscdn.com` in the global scope (`* disquscdn.com * allow`), such that next time you want to allow Disqus on any given site, the Disqus widget will work immediately after you locally allow `disqus.com` (notice the global scope is selected below):

![b](https://user-images.githubusercontent.com/585534/33133245-2e421de0-cf6a-11e7-9542-0dbb98e023aa.png)

Rules from a broader scope always propagate to narrower scopes, so rules from the global scope always propagate to all scopes, unless of course a narrower scope override a specific rule. Back to the `lareviewofbooks.org` scope, we see the global rule for `disquscdn.com` has propagated to the local scope:

![c](https://user-images.githubusercontent.com/585534/33133562-30a7f900-cf6b-11e7-93b1-934e80090cd4.png)

If you would rather have Disqus commenting widget not be broken at all on all sites by default, then you can just create the `disqus.com` rules above in the global scope: `* disqus.com * allow`, `* disqus.com frame allow` -- i.e., _your choice_ (I personally wouldn't do this given how widespread is Disqus).

Anyway, this is the purpose of the scope selector, to easily switch back and forth between scopes. When you switch to a given scope, the matrix will reflect the rules in effects for that scope, i.e. what would happen if the network requests had been made in the selected scope, and the rules you create/remove will be created/removed from the selected scope.