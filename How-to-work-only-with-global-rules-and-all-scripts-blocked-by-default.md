The motivation for this article is the following argument made at Wilders Security against uMatrix:

>  I like the way NoScrip works. If you think a domain should be untrusted, you untrust it everywhere. If you trust it, and require the domain, then you white list it.

The way you work your ruleset with uMatrix is not dictated by uMatrix. If you want to work strictly with global rules, i.e. rules that apply everywhere, uMatrix allows that.

Using an example page, this is uMatrix with out-of-the-box ruleset:

![a](https://user-images.githubusercontent.com/585534/33240862-77db100a-d28b-11e7-8e51-416ea0e5cafb.png)

From there, we will set up uMatrix to work as follow:

- All rules will be global.
- All script resources will be blocked by default.
- Scripts from a specific domain will be allowed/blocked with a single click on that domain.

First, select _"Global"_ as the default scope in uMatrix's _Settings_:

![a](https://user-images.githubusercontent.com/585534/33240881-f5903c8c-d28b-11e7-85d4-f849abb9d405.png)

From now on, the global scope will always be selected by default when you open the popup panel:

![a](https://user-images.githubusercontent.com/585534/33240893-5c192c48-d28c-11e7-89b4-70fb14318887.png)

