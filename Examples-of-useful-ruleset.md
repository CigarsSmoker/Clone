Assuming that you start with out of the box ruleset.

To copy a specific ruleset below into your own ruleset, go to _"My rules"_ in the dashboard. When you click _Edit_, you will be able to freely edit your rules, so from there it is just a matter of copying any specific ruleset below and pasting at the end of your list of rules, then click _Save_.

#### Youtube

This worked for me:

    youtube.com apis.google.com * allow
    youtube.com apis.google.com frame allow
    youtube.com googlevideo.com * allow
    youtube.com plus.google.com * allow
    youtube.com plus.google.com frame allow
    youtube.com plus.googleapis.com * allow
    youtube.com plus.googleapis.com frame allow
    youtube.com ytimg.com * allow

Even if you blocked all things Google in the global scope, Youtube will work just find with these rules.

#### Twitch TV

    twitch.tv api.swiftype.com script allow
    twitch.tv jtvnw.net * allow
