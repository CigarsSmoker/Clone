The motivation for this article is the following argument made at Wilders Security against uMatrix:

>  I like the way NoScrip works. If you think a domain should be untrusted, you untrust it everywhere. If you trust it, and require the domain, then you white list it.

The way you work your ruleset with uMatrix is not dictated by uMatrix. If you want to work strictly with global rules, i.e. rules that apply everywhere, uMatrix allows that.

Using an example page, this is uMatrix with out-of-the-box ruleset -- by default uMatrix is set up to work with per-base domain rules:

![a](https://user-images.githubusercontent.com/585534/33240862-77db100a-d28b-11e7-8e51-416ea0e5cafb.png)

From there, we will set up uMatrix to work as follow:

- All rules will be global.
- All script and frame resources will be blocked by default.
- Scripts and frames from a specific domain will be whitelisted/blacklisted with a single click on that domain.

First, select _"Global"_ as the default scope in uMatrix's _Settings_:

![a](https://user-images.githubusercontent.com/585534/33240881-f5903c8c-d28b-11e7-85d4-f849abb9d405.png)

From now on, the global scope will always be selected by default when you open the popup panel:

![a](https://user-images.githubusercontent.com/585534/33240893-5c192c48-d28c-11e7-89b4-70fb14318887.png)

Now we will change the out-of-the-box ruleset to achieve our goal of working only with global rules and to only block/allow scripts and frames, i.e. everything else will be allowed by default. All these modifications to the default ruleset can be done from the popup panel:

![a](https://user-images.githubusercontent.com/585534/33240946-eaab32d0-d28c-11e7-87bb-297d68d78b2c.png)

As seen in the picture above:

- The global scope is now always selected by default.
- The _cookie_, _media_, _XHR_, and _other_ cells were whitelisted.
- The _frame_ cell was un-blacklisted.
- The _1st-party_ cell was un-whitelisted.
- The _1st-party_/_frame_ cell was un-whitelisted.

Now persist these changes by clicking the padlock icon (which should report that 7 rules were changed):

![a](https://user-images.githubusercontent.com/585534/33241002-c12b7ffe-d28d-11e7-9af3-b9e78891aa70.png)

This is it.

Scripts and frames are now blocked everywhere, and simply creating an allow rule directly on whatever domain will enable scripts and frames to be loaded for that domain. If you persist such rule by clicking on the padlock, they become permanently part of your ruleset, and applies everywhere since they are created in the global scope.

For example: create _allow_ rules for `googlevideo.com`, `youtube.com`, and `ytimg.com` in the global scope (which is now always selected by default) and persist them with the padlock. You can now have embedded Youtube videos properly play on all sites:

![a](https://user-images.githubusercontent.com/585534/33243521-10796aee-d2b6-11e7-9a44-ab77142f9cc7.png)

If you care to deal with base domains only, then just collapse base domain sections by default:


![b](https://user-images.githubusercontent.com/585534/33243544-55dbe30a-d2b6-11e7-9418-46148d3ca41b.png)

You can expand specific base domain sections independently of the others if ever you want to set more granular subdomain-level rules.