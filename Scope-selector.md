Every rule you create in uMatrix applies to a specific scope. The scope tells uMatrix where a rule should be enforced. For example, you may want to block all network requests to `facebook.com` everywhere by default (`* facebook.com * block`), except when visiting web pages from `facebook.com` (`facebook.com facebook.com * allow`)

 The matrix UI in the popup panel allows you to easily select the scope from which to visualize/create/remove rules, the top-left cell is the scope selector:

![a](https://user-images.githubusercontent.com/585534/33131928-17587830-cf66-11e7-8a69-30902ac4ac87.png)

It is of course advised that you create rules which apply only for a specific scope, but of course it's convenient that some rules are created in the global scope (`*`) such that you do not have to constantly create the same rules for many sites. For most it's convenient to create `allow` rules in the global scope for domains which use is widespread, and which you trust.

For example, although you could keep blocking `frame` everywhere to keep blocking embedded Youtube videos on various web sites, you may want to create global `youtube.com` rules in order to be able to play embedded Youtube videos easily everywhere by simply allowing `frame` on any given web sites (you could also allow `frame` for `youtube.com` everywhere if you wish, your choice.)

Anyway, this is the purpose of the scope selector, to easily switch back and forth between scopes. When you switch to a given scope, the matrix will reflect the rules in effects for that scope, i.e. what would happen if the network requests had been made in the selected scope.