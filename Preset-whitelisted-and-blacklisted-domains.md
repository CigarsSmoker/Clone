## Preset whitelist rules

There are no preset whitelist rules for specific domains in uMatrix: whether a domain should be trusted or not is entirely your choice.

uMatrix will never come with out of the box whitelist rules for specific domains. There are millions of web sites out there, and uMatrix won't make a stand for any of them by packaging preset whitelist rules for specific web sites.

The only specific whitelist rules in uMatrix are the ones you create yourself.

However, hopefully I will one day be able to bring back the library of presets from where you can pick ready-to-use set of rules for specific purpose. See [issue #30](https://github.com/gorhill/uMatrix/issues/30).

## Preset blacklist rules

uMatrix comes with preset blacklist rules: these are derived from the hosts files (all selected by default).

Each hostname in a selected hosts file is converted into a blacklist rule as follow:

    * hostname * block

You may choose to un-select all hosts files so that no blacklist rules are imported as a result.

Even when working in default-deny mode, it is always a good thing to benefit from these preset blacklist rules:

- CSS and images are allowed by default in uMatrix. But since a global _block_ rule for a specific hostname has a higher precedence than a global _allow_ rule for a specific type, this means no CSS or image resources will be pulled from a blacklisted hostname -- the _block_ rule override the _allow_ rule.
- It may happen you want to allow all for a specific web site to quickly un-break a web page, by setting a [local _allow_ rule on the _all_ cell](https://github.com/gorhill/uMatrix/wiki/How-to-%22allow-all%22-in-uMatrix). A global _block_ rule on a specific hostname has a higher precedence than a local _allow_ rule on the _all_ cell, and as a result all connections to these blacklist hostnames will still be forbidden with a local _allow_ rule on the _all_ cell.