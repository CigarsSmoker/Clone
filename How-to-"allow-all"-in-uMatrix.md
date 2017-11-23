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