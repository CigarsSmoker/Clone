I see often users asking how to "allow all" in NoScript. So I will address the same question here but for uMatrix.

There are four ways to "allow all" in uMatrix. I will present then in order of gentleness, from the less scary way of allowing all to the most scary way of allowing all.

## Gentle "allow all"

Create a local _allow_ rule for the _all_ cell:

![a](https://user-images.githubusercontent.com/585534/33175914-39b16cb4-d02b-11e7-96e9-1750e31774c4.png)

This way the _allow_ rule applies only in the local scope, nowhere else. Assigning an _allow_ rule to the _all_ cell is a soft "allow all", because no narrower block rules will be overriden as a result, i.e. all the block rules imported from the hosts file will still be enforced.

Note that due to the propagation logic of rules in uMatrix, an _allow_ rule on the _all_ cell propagate to all non-blacklisted cells in the matrix, so that if you reload the page, the _allow_ rule will also propagate to newly seen network requests for which there is no explicit block rule.

