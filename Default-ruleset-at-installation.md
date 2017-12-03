For reference, this is the default ruleset when you first install uMatrix:

    https-strict: behind-the-scene false
    matrix-off: about-scheme true
    matrix-off: behind-the-scene true
    matrix-off: chrome-extension-scheme true
    matrix-off: chrome-scheme true
    matrix-off: localhost true
    matrix-off: moz-extension-scheme true
    matrix-off: opera-scheme true
    matrix-off: wyciwyg-scheme true
    referrer-spoof: behind-the-scene false
    * * * block
    * * css allow
    * * image allow
    * * frame block
    * 1st-party * allow
    * 1st-party frame allow

The rule `matrix-off: wyciwyg-scheme true` was added in [version 1.1.6](https://github.com/gorhill/uMatrix/releases/tag/1.1.6). If you are using Firefox and installed uMatrix before version 1.1.6, I strongly suggest you add this rule manually.

Some of the rules above are important to ensure proper operation of uMatrix and of your browser. Remove them at your own risk.