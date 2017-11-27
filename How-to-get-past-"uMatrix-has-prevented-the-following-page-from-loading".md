When a domain is blacklisted, uMatrix will block all network requests to the remote server, including the network requests for the root documents:

![a](https://user-images.githubusercontent.com/585534/33290912-358e2de2-d392-11e7-8612-0d38631a6fd2.png)

Most of the time it is likely a site blacklisted as a result of subscribing to one of the hosts files in the _Hosts files_ pane.

If you really want to be able to pull web pages from the blacklisted remote server, it's just a matter of modifying your ruleset appropriately.

Open the popup panel:

![a](https://user-images.githubusercontent.com/585534/33290869-103d90f0-d392-11e7-943c-c0666e26a05f.png)

Then just remove the blacklist rule by clicking on it:

![a](https://user-images.githubusercontent.com/585534/33291029-8d830cac-d392-11e7-967d-79f193697531.png)

**Important:** Note that the removing of the rule is done from the local scope, there is no need to remove this rule from the global scope.

Now force a refresh of the page:

![a](https://user-images.githubusercontent.com/585534/33291196-03b673d2-d393-11e7-9033-e9c48ff3b9d5.png)

Result -- the page now loads fine:

![a](https://user-images.githubusercontent.com/585534/33291269-43523378-d393-11e7-97e7-24c31a596954.png)

If you want the bypass of the block rule to be permanent, don't forget to use the padlock to persist the rule. Though in the example above, un-blacklisting `google-analytics.com` merely allowed a redirection to another server to succeed. In such case, you will have to persist your rule from the _My rules_ pane in the dashboard.

## Sidenotes

In the above example, the _block_ rule originates from one of the hosts file. In such case, it is not possible to literally remove the _block_ rule. What occurs internally is that uMatrix created an _inherit_ rule, which tell uMatrix that the cell must inherit it's _block_ or _allow_ status from a higher precedence cell in the **current** scope, rather than in a broader scope. The rule would look like this in your ruleset:

    google-analytics.com google-analytics.com * inherit

