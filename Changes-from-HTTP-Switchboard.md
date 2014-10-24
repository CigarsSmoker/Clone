µMatrix and [µBlock](https://github.com/gorhill/uBlock) are both spin-off of [HTTP Switchboard](https://github.com/gorhill/httpswitchboard) ("HTTPSB").

µMatrix inherited the task of matrix-filtering, while µBlock inherited the task of pattern-based filtering.

Main differences of µMatrix vs. HTTPSB explained below.

#### Rules are no longer sandboxed within scopes

Related HTTPSB issue: [#227](https://github.com/gorhill/httpswitchboard/issues/227).

The matrix is now conceptually 3d:
- Z is the source hostname axis (aka "scope"), from narrower scopes to global scope
- X is the request type axis: `*`, `cookie`, `css`, etc.
- Y is the destination hostname axis (`www.example.com`, `example.com`, `com`, `*`)

There is now only one flat data structure to hold all the matrix rules, and all rules are defined as follow:

`source hostname`, `destination hostname`, `request type`, `action`

When a request needs to be evaluated, µMatrix will find out from which web page the request originate. The hostname of the URL address of the web page will be extracted and used as the `source hostname` component. The hostname of the URL address of the request will be extracted and used as the `destination hostname` component.

µMatrix will then try to find an explicit rule which match exactly `source hostname, destination hostname, request type`. If no explicit rule is found, µMatrix will derive a broader scope from `source hostname` and try again to find an explicit rule in that broader scope. Eventually, the broadest scope possible is reached, which is `source hostname` being `*`: the global scope.

A matrix cell can have one of three _colors_: red (blacklisted), green (whitelisted), or transparent (graylisted). Just like before. The difference is that now with µMatrix all the possible scope are evaluated from narrowest to broadest to find out the _color_ of a cell.

Once the color is found, the matrix functions just the same as in HTTPSB, i.e. the matrix inheritance model is the same (that would be the X and Y part of the evaluation).

##### Concrete examples of how µMatrix's matrix-filtering differs from HTTPSB's matrix-filtering 

Any explicit rules created in the global scope will be seen in **all** narrower scopes.

More generally, any explicit rules created in a broader scope will be seen in related narrower scopes. Rules in `example.com` will be seen by the `www.example.com` scope. And so on. This is important to remember when you create rules.

As a result, now creating rules in narrower scopes is the natural way to use µMatrix. Since rules created in the global scope `*` will be seen everywhere, then global rules are useful for some specific cases. 

For example, when using the browser's _"Translate to [Specific language]"_ option in the contextual menu, the browser will send a request to `translate.googleapis.com` to do the job. If you whitelist `translate.googleapis.com` in the global scope, then the feature to translate a page using the contextual menu will work in all scopes (that is, unless a explicit block rule exists in a narrower scope).

#### There is no longer "scope" data structures internally

In HTTPSB, scopes were mapped to discrete data structures internally, which were used to sandbox rules -- and as a consequence preventing scopes to inherit rules from broader scopes. There was a resource cost when creating a scope, and when evaluating a net request.

There is no more concrete data structure for scopes in µMatrix: all scopes virtually exist, so in µMatrix there is no longer a resource cost associated with scope creation. This also eliminate the need for settings such as:

- _"Auto create temporary [domain | site]-level scope"_
- _"Copy all rules from global scope into newly created local scopes"_
- _"Auto delete unused temporary scopes"_

Al these settings are now gone.

The scope selector in the matrix popup is simply used to select where a rule should be created. As a convenience, µMatrix will remember the scope level you selected and select it automatically next time you open the matrix popup.

#### A new `1st-party` row

In HTTPSB, if you wished to auto-whitelist the domain of the web page, you had to enable the setting _"Auto whitelist page domain"_. This setting is now gone, and a `1st-party` row is now used in the matrix to create whatever rules you want for net requests which are 1st-party to a web page.

To auto-whitelist the domain of the web page is simply a matter of whitelisting the `1st-party` cell in the global scope. With just this one rule now all net requests which are 1st-party to a web page will be allowed (unless overriden by a narrower rule as usual). So as opposed to before with HTTPSB, no temporary rules are created to auto-whitelist: your ruleset is kept clean and tidy.

#### Strict mode is now the only available mode

There was not much real use for disabling "strict mode", except for when a user wanted to fully auto-whitelist 1st-party requests when `frame` (or whatever request type(s)) were globally blacklisted (a good habit).

Now with the `1st-party` row, it's just a matter of whitelisting `*, 1st-party, frame`, which will override the global blacklisting of the `frame` type, and thus it has become possible to fully whitelist a domain despite the presence of blacklisted types.