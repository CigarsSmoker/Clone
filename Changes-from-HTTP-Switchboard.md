µMatrix and [µBlock](https://github.com/gorhill/uBlock) are both spin-off of [HTTP Switchboard](https://github.com/gorhill/httpswitchboard).

µMatrix inherited the task of matrix-filtering, while µBlock inherited the task of pattern-based filtering.

Main differences of µMatrix vs. HTTP Switchboard explained below.

#### Rules are no longer sandboxed within scopes

Related HTTP Switchboard issue: [#227](https://github.com/gorhill/httpswitchboard/issues/227).

The matrix is now conceptually 3d:
- Z is the source hostname axis (aka "scope"), from narrower scopes to global scope
- X is the request type axis: `*`, `cookie`, `css`, etc.
- Y is the destination hostname axis (`www.example.com`, `example.com`, `com`, `*`)

There is now only one flat data structure to hold all the matrix rules, and all rules are defined as follow:

`source hostname`, `destination hostname`, `request type`, `action`

When a request needs to be evaluated, µMatrix will find out from which web page the request originate. The hostname of the URL address of the web page will be extracted and used as the `source hostname` component. The hostname of the URL address of the request will be extracted and used as the `destination hostname` component.

µMatrix will then try to find an explicit rule which match exactly `source hostname, destination hostname, request type`. If no explicit rule is found, µMatrix will derive a broader scope from `source hostname` and try again to find an explicit rule in that broader scope. Eventually, the broadest scope possible is reached, which is `source hostname` being `*`: the global scope.

A matrix cell can have one of three _colors_: red (blacklisted), green (whitelisted), or transparent (graylisted). Just like before. The difference is that now with µMatrix all the possible scope are evaluated from narrowest to broadest to find out the _color_ of a cell.

Once the color is found, the matrix functions just the same as in HTTP Switchboard, i.e. the matrix inheritance model is the same (that would be the X and Y part of the evaluation).

##### Concrete examples of how µMatrix's matrix-filtering differs from HTTP Switchboard's matrix-filtering 

Any explicit rules created in the global scope will be seen in **all** narrower scopes.

More generally, any explicit rules created in a broader scope will be seen in related narrower scopes. Rules in `example.com` will be seen by the `www.example.com` scope. And so on. This is important to remember when you create rules.

As a result, now creating rules in narrower scopes is the natural way to use µMatrix. Since rules created in the global scope `*` will be seen everywhere, then global rules are useful for some specific cases. 

For example, when using the browser's _"Translate to [Specific language]"_ option in the contextual menu, the browser will send a request to `translate.googleapis.com` to do the job. If you whitelist `translate.googleapis.com` in the global scope, then the feature to translate a page using the contextual menu will work in all scopes (that is, unless a explicit block rule exists in a narrower scope).

