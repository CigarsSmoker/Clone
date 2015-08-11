uMatrix mainly blocks outgoing connections/outgoing data; it does not block incoming data. It's important to understand this concept to understand uMatrix cookie-handling:

- All incoming cookies are accepted and stored (no matter if they are allowed or blocked by uMatrix).

  So, you can see all received cookies in your browsers cookie-list. This also makes it possible for uMatrix to show which site wanted to set cookies and how many it wanted to set (which wouldn't be possible if uMatrix would "reject" all cookies).
- But uMatrix prevents these cookies from leaving the browser.

  So, if you block cookies by uMatrix, a server which has set a cookie cannot read the cookie again -- and so, the cookie is blocked.

- You can tell uMatrix to automatically delete "blocked" cookies (option "Delete blocked cookies"). Then, uMatrix will periodically (~every 2 minutes) delete all blocked cookies from the browser.

  If you don't enable this option, "blocked" cookies may be stored in your browser for a long time.

An explaination can also be found in the "Delete blocked cookies." help text in the uMatrix-Dashboard:

> Blacklisted cookies are not prevented by uMatrix from entering your browser. However they are prevented from leaving your browser, which is what really matters. Not blocking cookies before they enter your browser gives you the opportunity to be informed that a site tried to use cookies, and furthermore to inspect their contents if you wish.

> Once these blacklisted cookies have been accounted for by uMatrix, they can be removed from your browser if you wish so.

> **Important note:** Extensions can make web requests during the course of their normal operation. These requests can result in cookies being created in the browser. If the hostname from where a cookie originate is not whitelisted, the cookie will be removed from the browser by uMatrix if this option is checked. So be sure that the hostname(s) with which an extension communicate is whitelisted.

----

Note that this kind of "cookie-blocking" can have some side-effects on 3rd-party-cookies:

- If you allow requests to 3rd-party-pages (e.g. allow 3rd-party-images, -scripts, -frames etc.), these sites can also send you cookies which are then stored in the browser (no matter if cookies are allowed or blocked by uMatrix). So, you'll also see these 3rd-party-cookies in your browsers cookie-list.

  But of course, uMatrix blocks these cookies from being sent back to the server (unless you allowed it).

- If you allow cookies for a site, the server of this site may also read it's own 3rd-party-cookies, which were set on other sites -- even if they were blocked.

  Since this is tricky to understand, here's an example:

  - Assuming, you have blocked all cookies with uMatrix, and allowed images from 3rd-party-pages.
  - Now, you visit somepage.example, which includes an image from socialnetwork.example.
  - socialnetwork.example sends the image to your browser, and adds a cookie.
    This (3rd-party-)cookie is stored in your browser, but not sent back to any server (since uMatrix blocks this).
  - Then, you go to socialnetwork.example, and allow cookies (e.g. because you want to log in).
  - socialnetwork.example can now read the (blocked 3rd-party-)cookie, which was set on somepage.example.

If you don't like this behaviour, it's probably best to disable 3rd-party-cookies in you browser preferences.

----

See also: https://github.com/gorhill/uMatrix/issues/252, https://github.com/gorhill/uMatrix/issues/316
