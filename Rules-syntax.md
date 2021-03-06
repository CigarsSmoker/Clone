Rules are used in a broad sense here: let's rather call them "directives". Most directives will be rules, hence I used _"My rules"_ in the dashboard.

Each line is a directive. Empty lines will be skipped.

The `#` character can be used for commenting, and for each line, the parser will ignore the first occurrence of `#` and everything following it.

A directive starts with a directive keyword, immediately followed by the `:` which character is used to tell a parser that we are dealing with a directive keyword.

There are currently two directives: `rule:` and `matrix:`. However, the `rule:` directive can be omitted, because it is implicit when there is no directive. Since most directives will be rules, it would be inconvenient to be forced to use `rule:` for each rule.

In the documentation below the square brackets (`[]`) are used to denote optional fields. Curly brackets (`{}`) are used to denote what should appear at a specific position.

#### Directive `rule:` syntax

> _source hostname_ {white spaces} _destination hostname_ {white spaces} [_request type_ {white spaces} [_action_]]

`rule:` is implicit, you don't have to use it (actually, currently the parser will not work if you use it...)

White spaces can be any number of space character or tab character.

**source hostname** is the context from which a net request is made, also known as the "scope". `*` can be used to denote "any context", aka the _global scope_.

**destination hostname** is where the net request is destined. `*` can be used to denote "any destination".

**request type** is the type of the net request. If omitted, the `*` type is assumed and means "any type".

**action** is what to do when a net request matches _source hostname_, _destination hostname_ and _request type_. Currently, the actions supported are:
- `block`: the request will be prevented (often referred as "blacklisted")
- `allow`: the request will be allowed (often referred as "whitelisted")
- `inherit`: the action will be inherited from another cell in the matrix, as per cell inheritance logic. It's what is often referred as "graylisted".

If _action_ is omitted, `allow` is used -- because uMatrix is naturally deny-default mode at heart.

For both source and destination, matching is hierarchical: a rule for a domain will be matched by all subdomains (except if another rule match for the subdomain).

##### Order of precedence

General principle: more specific rule overrides less specific rule. Precedence is defined in `evaluateCellZXY` method (see [matrix.js](https://github.com/gorhill/uMatrix/blob/master/src/js/matrix.js)).

Priority order is following: matrix-off > srcHostname > desHostname > type

The order of rules doesn't matter. It is undefined what the rule will have effect among the rules with the same priority.


##### Examples of rules

Forbid all requests to `facebook.net`, but allow all net requests of any type to `facebook.net` only when they are made from within `facebook.com` context:

`* facebook.net * block`<br>
`facebook.com facebook.net * allow`<br>

or

`* facebook.net * block`<br>
`facebook.com facebook.net *`<br>

or

`* facebook.net * block`<br>
`facebook.com facebook.net`

The above rules all accomplish the same thing, as per default values.

Subdomains will also match, so `www.facebook.net` will also be filtered except from any subdomain of `facebook.com`.

#### Directive `matrix-off:` syntax

Disable or enable matrix filtering for a specific scope. Syntax:

> `matrix-off:` {white spaces} _source hostname_ {white spaces} _state_

**source hostname** is the context for which matrix filtering needs to be toggled on or off.

**state** can be one of `true` or `false` keyword.

Reminder: narrower scopes inherit the matrix-filtering switch state from broader scopes. So if you disable matrix-filtering in the global scope (`*`), then matrix-filtering will be turned off for all scopes, unless a scope has an explicit override of the matrix-filtering switch.