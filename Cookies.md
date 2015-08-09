uMatrix "blocks" cookies are somehow different than other cookie blockers. The explaination can be found in the "Delete blocked cookies." help text in the uMatrix-Dashboard:

> Blacklisted cookies are not prevented by uMatrix from entering your browser. However they are prevented from leaving your browser, which is what really matters. Not blocking cookies before they enter your browser gives you the opportunity to be informed that a site tried to use cookies, and furthermore to inspect their contents if you wish.

> Once these blacklisted cookies have been accounted for by uMatrix, they can be removed from your browser if you wish so.

> **Important note:** Extensions can make web requests during the course of their normal operation. These requests can result in cookies being created in the browser. If the hostname from where a cookie originate is not whitelisted, the cookie will be removed from the browser by uMatrix if this option is checked. So be sure that the hostname(s) with which an extension communicate is whitelisted.

So, if you "block" cookies via uMatrix, they are accepted at first (so uMatrix can inform you about the cookies, and you can view the cookies), but uMatrix prevents them from being read. These cookies can be automatically deleted by enabling the option "Delete blocked cookies.". Note that these cookies are currently deleted every ~2 minutes (for performance reasons, so that all cookies can be deleted at once and not every cookie needs to be deleted individually).

Note that this kind of "cookie-read-blocking" can have some side-effects:

- The cookies are not really blocked/rejected, but stored, and you can view them e.g. in your browsers cookie-list.
- If you don't enable "Delete blocked cookies.", these "blocked" cookies may be stored in your browser for a long time.
- 3rd-party-cookies are also stored, if the request (image/script/frame/...) to the 3rd-party-page is allowed (no matter if cookies are blocked or not). 
- If you allow cookies on a site (e.g. example.com), be aware that this site could then also read the example.com-3rd-party-cookies of other sites, no matter if you blocked these 3rd-party-cookies or not.

If you don't want to store 3rd-party-cookies and don't want that websites could read their cookies from 3rd-party-pages, you should disable 3rd-party-cookies in your browsers preferences.

If you want to block cookies, so they are not stored at all (unless allowed), you should use an additional cookie-blocker-addon.

-------
See also: https://github.com/gorhill/uMatrix/issues/252, https://github.com/gorhill/uMatrix/issues/316
