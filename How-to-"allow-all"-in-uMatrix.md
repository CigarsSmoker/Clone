I see often users asking how to "allow all" in NoScript. So I will address the same question here but for uMatrix.

There are four ways to "allow all" in uMatrix. I will present them in order of gentleness, from the less scary way of allowing all to the most scary way of allowing all.

## Local soft allow-all

Create a local _allow_ rule for the _all_ cell:

![a](https://user-images.githubusercontent.com/585534/33175914-39b16cb4-d02b-11e7-96e9-1750e31774c4.png)

This way the _allow_ rule applies only in the local scope, nowhere else. Assigning an _allow_ rule to the _all_ cell is a soft allow-all, because no narrower block rules will be overriden as a result, i.e. all the block rules imported from the hosts file will still be enforced.

Note that due to the propagation logic of rules in uMatrix, an _allow_ rule on the _all_ cell propagate to all non-blacklisted cells in the matrix, so that if you reload the page, the _allow_ rule will also propagate to newly seen network requests for which there is no explicit block rule.

## Local hard allow-all

A local hard allow-all will completely disable matrix filtering, but only for the local scope:

![b](https://user-images.githubusercontent.com/585534/33176267-7fdf41c4-d02c-11e7-926b-16276b2bf3a2.png)

Note that in such case, this will also disable all the block rules imported from the hosts file, which is the equivalent of almost completely disabling uMatrix, but at least only for the current scope.

Important: keep in mind that the per-scope switches are independent of the matrix filtering switch, you may also need/want to turn them off.

## Global soft allow-all

Create a global _allow_ rule for the _all_ cell (notice the global scope is selected in the picture):

![a](https://user-images.githubusercontent.com/585534/33176486-350de8de-d02d-11e7-8b78-cd60fe16fadf.png)

Same behavior as "local allow-all", except that now it applies to all scopes, i.e. web pages loaded from wherever will all be in soft allow-all mode.

Keep in mind though that all narrower block rules will not be overridden, as per uMatrix rule propagation logic, so all block rules from hosts files will still be enforced everywhere, and also all your block rules will still be enforced.

## Global hard allow-all

Disable matrix filtering while in the global scope (notice the global scope is selected in the picture):

![b](https://user-images.githubusercontent.com/585534/33176919-c85212f4-d02e-11e7-833f-458bf02e2b89.png)

The matrix filtering switch is just like any other rule, its state propagates to narrower scopes. So disabling matrix filtering in the global scope is almost equivalent to disabling completely uMatrix on all sites.

## Reminders

A reminder that all rules (matrix or switches) are temporary by default. So in the examples above, one would simply click of the _"Revert all temporary changes"_ button in the popup panel to remove all these allow-all rules and put back uMatrix in its original state.

Also, I want to remind and emphasize that all rules (matrix or switches) in uMatrix propagate to narrower scopes, unless a more explicit rule is encountered on the way down to narrower scopes.

This means that it's entirely possible for uMatrix to work in "reverse mode", in which uMatrix does not filter anything by default, and one would enable uMatrix only for specific site. Of course I do not expect power users to ever work this way, but this is just to again emphasize the rule propagation logic inherent to uMatrix.