Assuming that you start with out of the box ruleset.

To copy a specific ruleset below into your own ruleset, go to _"My rules"_ in the dashboard. When you click _Edit_, you will be able to freely edit your rules, so from there it is just a matter of copying any specific ruleset below and pasting at the end of your list of rules, then click _Save_.

#### facebook.* ONLY on Facebook, blocked everywhere else

    * facebook.com * block
    * facebook.net * block
    facebook.com facebook.com * allow
    facebook.com fbstatic-a.akamaihd.net * allow

Probably needs more rules, but I don't have a Facebook account, can't tell. But for those without a Facebook account, this worked good enough to browse Facebook pages.

A more granular version that might be useful is:

    facebook.com 1st-party xhr allow
    facebook.com facebook.com cookie allow
    facebook.com fbcdn.net script allow
    facebook.com fbcdn.net xhr allow
    facebook.com staticxx.facebook.com frame allow
    facebook.com video-ort2-2.xx.fbcdn.net media allow
    facebook.com www.facebook.com frame allow
    facebook.com www.facebook.com media allow
    facebook.com www.facebook.com xhr allow

This works for logging in (including 2-factor auth!) and browsing Facebook, posting comments, viewing images/videos, etc.

#### github.com

    github.com ghconduit.com xhr allow
    github.com githubapp.com * allow
    github.com raw.githubusercontent.com * allow
    github.com render.githubusercontent.com * allow
    github.com render.githubusercontent.com frame allow
    github.com s3.amazonaws.com other allow
    github.com s3.amazonaws.com xhr allow

#### skyscraperlive.com

    skyscraperlive.com brightcove.com plugin allow
    skyscraperlive.com brightcove.com script allow
    skyscraperlive.com c.brightcove.com plugin allow
    skyscraperlive.com connect.facebook.net script allow
    skyscraperlive.com discintlhdflash-f.akamaihd.net plugin allow
    skyscraperlive.com platform.twitter.com script allow
    skyscraperlive.com ustream.tv plugin allow
    skyscraperlive.com ustream.tv script allow
    skyscraperlive.com www.ustream.tv frame allow

#### stackoverflow.com
    stackoverflow.com ajax.googleapis.com script allow
    stackoverflow.com sstatic.net image allow
    stackoverflow.com sstatic.net script allow

#### twitch.tv

    twitch.tv akamaized.net xhr allow
    twitch.tv ttvnw.net xhr allow
    twitch.tv static.twitchcdn.net script allow

#### youtube.com

This worked for me:

    youtube.com apis.google.com * allow
    youtube.com apis.google.com frame allow
    youtube.com googlevideo.com * allow
    youtube.com plus.google.com * allow
    youtube.com plus.google.com frame allow
    youtube.com plus.googleapis.com * allow
    youtube.com plus.googleapis.com frame allow
    youtube.com ytimg.com * allow

Even if you blocked all things Google in the global scope, Youtube will work just fine with these rules.

A more granular ruleset that might be useful is:

    youtube.com clients1.google.com script allow
    youtube.com googlevideo.com media allow
    youtube.com googlevideo.com xhr allow
    youtube.com www.google.com script allow
    youtube.com www.youtube.com other allow
    youtube.com www.youtube.com xhr allow
    youtube.com youtube.com script allow
    youtube.com ytimg.com script allow

This has yet to break anything for me (i.e. I can watch Youtube videos just fine on youtube.com).

#### youtube-nocookie.com

This one is useful when you click on a blocked Youtube embedded in a frame on a 3rd-party page (click the label). It worked for me.

    youtube-nocookie.com googlevideo.com xhr allow
    youtube-nocookie.com ytimg.com * allow

---

#### Third-party rules:
- https://github.com/uMatrix-Rules
- https://github.com/kristerkari/umatrix-recipes