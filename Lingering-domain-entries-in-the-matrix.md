When you load a web page, uMatrix will collate all the hostnames seen in the network traffic (through its [webRequest](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/API/webRequest) listener).

From these hostnames, uMatrix will extract base domain names, and all of these and intermediate subdomains will be reported in the matrix UI.

Now the following is very important to keep in mind: **uMatrix does not clean the slate when a new page is loaded from the same site.**

The reason for this is that uMatrix wants to be sure everything is reported to the user, to ensure the user will be properly informed should there be a rare network request made to some strange 3rd party server, which could otherwise more than likely go unseen or unnoticed if uMatrix was to clean the slate between each page loads from the same site.

For any given site, the slate is cleaned when you navigate to a new site (i.e. the hostname in the URL address changes), or when you close the tab -- i.e. loading the same site in a new tab will cause that the tab to start with a clean slate.