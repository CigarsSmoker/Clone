Just a quick guide to show how to create rules which apply everywhere. This is convenient for domains which use is widespread and which you trust. First an example page -- notice the embedded Youtube video in it (a common occurrence), which is being blocked by uMatrix:

![a](https://user-images.githubusercontent.com/585534/33275036-c29e1c98-d35f-11e7-9194-55c8e3012f9c.png)

The popup panel shows what you get when using uMatrix with out-of-the-box ruleset (**correction:** the cookie _block_ rule is not part of the out-of-the-box ruleset, it's my own rule I forgot to remove):

![a](https://user-images.githubusercontent.com/585534/33275092-f3c368a0-d35f-11e7-8f0b-b869b96bb6db.png)

From there, we will create global rules which will allow embedded Youtube videos to work everywhere, on all web sites.

Select the global scope:

![a](https://user-images.githubusercontent.com/585534/33275167-26939dcc-d360-11e7-87e4-1177df4a7579.png)

Once the global scope is selected, whitelist everything from `youtube.com`, and also whitelist _frame_ for `youtube.com` (a necessary step since 3rd-party frames are blocked with default ruleset):

![a](https://user-images.githubusercontent.com/585534/33275270-67c695d8-d360-11e7-872e-4dfc7ece1e75.png)

Force a reload of the page to see the effect of these new rules:

![a](https://user-images.githubusercontent.com/585534/33275316-83496d30-d360-11e7-962e-d9467c467c5c.png)

Now let's find out if the video plays properly. Nope, it does not work:

![a](https://user-images.githubusercontent.com/585534/33275335-9327161c-d360-11e7-879d-102e7a61d9b6.png)

Apparently we need to whitelist more stuff. Now the matrix shows a new entry, `googlevideo.com`, this must be it:

![a](https://user-images.githubusercontent.com/585534/33275396-c7defe2e-d360-11e7-8ead-a74bd098f4fe.png)

Again, select the global scope:

![a](https://user-images.githubusercontent.com/585534/33275476-f8710a14-d360-11e7-855c-ebca590054a4.png)

Whitelist everything from `googlevideo.com`:

![a](https://user-images.githubusercontent.com/585534/33275524-1833f8fc-d361-11e7-9d4c-bcf5d58a5e00.png)

Force a reload of the page:

![a](https://user-images.githubusercontent.com/585534/33275575-302f1f4a-d361-11e7-8bae-7981988c3ba2.png)

Let's find out if this fixes the embedded Youtube video. It does, the Youtube video plays fine now:

![a](https://user-images.githubusercontent.com/585534/33275638-4b268450-d361-11e7-8540-b369665496e6.png)

Since these global rules proved to work fine to unbreak embedded Youtube videos, it's a good idea to make them permanent by clicking the padlock (rules are all temporary by default in uMatrix):

![a](https://user-images.githubusercontent.com/585534/33275690-6a76b76c-d361-11e7-91af-e6a20622bad3.png)

Now you have created three global rules which will un-break embedded Youtube videos on all sites. In this other site the embedded Youtube video plays just fine without having to fiddle with uMatrix:

![a](https://user-images.githubusercontent.com/585534/33276255-0ba79fe2-d363-11e7-8982-5fbfebc02eb9.png)

As seen in the matrix, the global rules created above are propagating to the narrower domain scope:

![a](https://user-images.githubusercontent.com/585534/33276326-475c828c-d363-11e7-97aa-ab2c82a2e3c1.png)

## Sidenotes

For reference, the three rules created in the current tutorial were:

    * youtube.com * allow
    * youtube.com frame allow
    * googlevideo.com * allow

If you know beforehand which domains you want to trust everywhere, you can enter the rules directly in the _My rules_ pane in the dashboard. A rule which applies on all sites would look like this:

    * ajax.googleapis.com * allow

Just replace `ajax.googleapis.com` with whatever is in your list of trusted domain names.

Always keep in mind that all rules you create are temporary, so you have to explicitly persist them using the padlock to make them permanent.

The badge count on the padlock shows you how many temporary rules have not been saved in the current context. It won't show you temporary rules from other contexts however. You may go to _My rules_ pane in the dashboard to see all the current temporary rules.