# Idea
Instead of starting with a permissive model, start with a _very_ restrictive model and whitelist as necessary.

# Default ruleset
Go to the uMatrix panel and select the global scope. Deselect everything except 1st-party CSS.

# How to work with this
Open a new page. It might look horribly broken, but don't panic! Look at the uMatrix panel for third party CSS resources (anything with a number in it in the CSS column is probably useful). Select the CSS box for those (sub)domains. Reload. Hopefully, the site looks decent now!

The next step is images. Again, toggle specific (sub)domains until the site looks reasonable.

# To save or not to save?

If this is a site you visit fairly often, you should probably save the rules so that you don't have to go through this too often. Otherwise, I wouldn't bother - the fewer the rules, the less the potential for unexpected things to happen.

# Concrete example
Let's take facebook.com as an example. We'll walk through how to figure out what the site needs and how.

First, we visit Facebook. I will be using a vanilla Firefox profile with only uMatrix installed.

1. Facebook is utterly broken. We click on the uMatrix panel and note that `static.xx.fbcdn.net` has a `7` in the CSS box. We toggle that and reload.

2. It already looks a lot better! Now we fix the images. We see that the `facebook.com`, `www.facebook.com`, `scontent-ort2-2.xx.fbcdn.net`, and `static.xx.fbcdn.net` entries have multiple images, so we toggle the image box for `facebook.com` and the last two (`www.facebook.com` is automatically whitelisted as you can see in the screenshot). We reload.

3. We now see that Facebook complains that Javascript is disabled in the browser, so we go ahead and toggle the script box for `facebook.com` and reload.

4. We now try logging in. When we click "Login", we get an error that cookies are not enabled, so we go ahead and toggle the cookie box for `facebook.com` and try logging in again.

5. This is enough to get us logged in! However, Facebook itself doesn't work! The screen is blank. The only resource that shows as blocked (currently) is the script box of `static.xx.fbcdn.net`, so let's toggle that and try again.

6. That worked! We're able to see stuff in the Newsfeed now. However, clicking on Notifications doesn't seem to work. When we click on it, we see the XHR box in `www.facebook.com` tick up, so let's try toggling that.

7. Cool! Now we can see notifications (and click on them). However, images aren't loading (the ones in the newsfeed will load, but try clicking on one of them). We see that the image box of `scontent.xx.fbcdn.net` is blocking something, so we'll try toggling that.

8. This seems to just bring up a new domain (`external-ort2-2.xx.fbcdn.net`)! Let's toggle its image box as well.

9. That worked! We can now view images both inline and in theatre mode. Now try scrolling down. Uh oh. Facebook refuses to load new things! If you look at the console, you'll see that it's trying to pull new content from `1-edge-chat.facebook.com`. Anticipating what is going on, we can go ahead and whitelist XHR for 1st-party. Let's try reloading now.

10. Huh, it still doesn't work. Perhaps whitelisting the frames in `staticxx.facebook.com` and `www.facebook.com` would help? 

11. Cool! It works! Now let's try to find an embedded video to see if it will play (Hint: it won't). We get a loading circle which almost immediately stops. We see a `video-ort2-2.xx.fbcdn.com`, so let's whitelist its XHR (it needs to fetch the video after all!).

12. And it works! You can now view posts, images, and videos while only whitelisting the specific things Facebook needs for those purposes.