By default, uMatrix does not prevent root documents from loading -- unless the domain itself is blacklisted. It would be quite impractical to block all root documents by default.

There is a built-in _allow_ rule (`* * doc allow`) in uMatrix such that root documents are properly loaded even when there is a _block_ rule on the _all_ cell, and even if the current domain is not whitelisted (this will happen if you remove the `* 1st-party * allow` rule from your ruleset):

![a](https://user-images.githubusercontent.com/585534/33379786-01b0c5ba-d4e7-11e7-8b30-6c50c287c235.png)<br><sup>`* 1st-party * allow` was removed, root document still loaded fine.</sup>

If you want even root document to inherit the state of lower precedence block rules, you will need to override the built-in _allow_ rule for root document. To do so, you will have to add the following rule into your ruleset by manually editing through _My rules_ pane in the dashboard:

    * * doc inherit
 
If additionally you remove the `* 1st-party * allow` rule from your ruleset, then all root documents will become blocked by default (assuming the lower precedence _all_ cell is blacklisted):

![a](https://user-images.githubusercontent.com/585534/33379162-50cdf37c-d4e5-11e7-8ef9-4fdb349fcaa8.png)

And you will have to explicitly create an _allow_ rule for the root document to load:

![a](https://user-images.githubusercontent.com/585534/33379307-bf915fa6-d4e5-11e7-8d32-ff5885c47263.png)

I do not expect many users to work this way, but I document it here so that it hopefully answers questions about how root documents are handled in uMatrix.

Note that the built-in rule `* * doc allow` never appears in _My rules_, because of a history of users blanket removing all rules and then opening an issue about uMatrix now blocking too much. The rule is now built-in and must be overridden with an explicit `* * doc inherit` in order for root documents to inherit their block/allow status from the _all_ cell.