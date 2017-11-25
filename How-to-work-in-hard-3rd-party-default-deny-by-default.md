Out of the box, uMatrix's ruleset is "soft" 3rd-party default-deny.

"Soft" here means that passive 3rd-party resources are not blocked by default, so as to minimize the likelihood of web sites not rendering properly. Passive resources are stylesheets and images.

With a few clicks, you can modify the ruleset so that uMatrix works in "hard" 3rd-party default-deny everywhere.

"Hard" here means that even 3rd-party passive resources will be forbidden by uMatrix. This quite increases the likelihood of web sites not rendering properly visually, but for some the benefits are worth it because this prevents **all** 3rd-party network requests when loading web pages.

First, this is a web page with uMatrix's out-of-the-box ruleset at work:

![a](https://user-images.githubusercontent.com/585534/33232100-08274da4-d1ce-11e7-997c-63b35fd8ec23.png)

From there, select the global scope:

![a](https://user-images.githubusercontent.com/585534/33232106-32a84538-d1ce-11e7-8688-86962052efea.png)

Then remove both _allow_ rules for _css_ and _image_ (this removes `* * css allow` and `* * image allow` from your ruleset):

![a](https://user-images.githubusercontent.com/585534/33232118-4b6f3842-d1ce-11e7-8673-0b16183aac7f.png)

Don't forget the persist your changes if you plan to keep that "hard" 3rd-party default-deny for good:

![a](https://user-images.githubusercontent.com/585534/33232126-702013c8-d1ce-11e7-8bbf-832386778088.png)

The result -- all 3rd-party requests are now blocked (the article in the page could still be read fine in the current example):

![a](https://user-images.githubusercontent.com/585534/33232132-8599f502-d1ce-11e7-8659-34bac9a39bce.png)

You will probably have to work a bit more to un-break your sites, but for many it's worth it in order to completely forbid 3rd-party network requests.