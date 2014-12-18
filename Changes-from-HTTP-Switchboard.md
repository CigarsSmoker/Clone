µMatrix and [µBlock](https://github.com/gorhill/uBlock) are both spin-off of [HTTP Switchboard](https://github.com/gorhill/httpswitchboard) ("HTTPSB"). They both improve significantly on HTTPSB. Essentially, HTTPSB is the fancy prototype, proof of concept to test many ideas. µMatrix and µBlock are the final products.

µMatrix inherited the task of matrix-based filtering, while µBlock inherited the task of pattern-based filtering.

Main differences of µMatrix vs. HTTPSB explained below.

- [Rules are no longer sandboxed within scopes](#rules-are-no-longer-sandboxed-within-scopes)
- [A new `1st-party` row](#a-new-1st-party-row)
- [No more restriction on effective domain boundaries](#no-more-restriction-on-effective-domain-boundaries)
- [There is no longer "scope" data structures internally](#there-is-no-longer-scope-data-structures-internally)
- ["Strict blocking" is now the only available mode](#strict-blocking-is-now-the-only-available-mode)
- ["Ubiquitous rules" tab replaced by "Hosts files" tab](#ubiquitous-rules-tab-replaced-by-hosts-files-tab)
- ["Scoped rules" tab replaced by "My rules" tab](#scoped-rules-tab-replaced-by-my-rules-tab)
- [Per-scope switches](#per-scope-switches)
- [Preset rulesets are gone for the time being](#ubiquitous-rules-tab-replaced-by-hosts-files-tab)

#### Rules are no longer sandboxed within scopes

Related HTTPSB issue: [#115](https://github.com/gorhill/httpswitchboard/issues/115), [#227](https://github.com/gorhill/httpswitchboard/issues/227).

With HTTPSB, if you created a rule in the global scope to block all from `addthis.com`, narrower scopes would not be aware of that rule: a user would have to re-create the rule in each and every narrower scopes. This is because originally scopes didn't exist in HTTPSB, _scoping_ was slapped on top of the existing infra-structure at some point during development. In µMatrix, the infrastructure has been rewritten from the ground up with scoping as a core feature. So with µMatrix, adding a block rule for `addthis.com` in the global scope will cause `addthis.com` to be blocked everywhere, in all scopes (as usual, unless a more specific rule overrides the broader rule).

So scopes are now fully layered exactly as how [this user expected them to be](https://github.com/gorhill/httpswitchboard/issues/227) in HTTP Switchboard (they were not).

The matrix is now conceptually 3d:
- Z is the source hostname axis (aka "scope"), from narrower scopes to global scope
- X is the request type axis: `*`, `cookie`, `css`, etc.
- Y is the destination hostname axis (`www.example.com`, `example.com`, `com`, `*`)

There is now only one flat data structure to hold all the matrix rules, and all rules are defined as follow:

`source-hostname destination-hostname request-type action`

When a request needs to be evaluated, µMatrix will find out from which web page the request originate. The hostname of the URL address of the web page will be extracted and used as the `source-hostname` component. The hostname of the URL address of the request will be extracted and used as the `destination-hostname` component.

µMatrix will then try to find an explicit rule which matches exactly `source-hostname`, `destination-hostname`, and `request-type`. If no explicit rule is found, µMatrix will derive a broader scope from `source-hostname` and try again to find an explicit rule in that broader scope. Eventually, the broadest scope possible is reached, which is `source-hostname` being `*`: the global scope.

This z-axis evaluation mechanism did not exist in HTTPSB, aside the not very flexible _"ubiquitous rules"_. Given that now all rules in global scope are ubiquitous to all scopes, HTTPSB's _"ubiquitous block rules"_ and _"ubiquitous allow rules"_ are gone, there is no more need for these.

A matrix cell can have one of three _colors_: red (blacklisted), green (whitelisted), or no color (graylisted). Just like before. The difference is that now with µMatrix all the possible scopes are evaluated from narrowest to broadest to find out the _color_ of a cell.

Once the color is found, the matrix functions just the same as in HTTPSB, i.e. the matrix inheritance model is the same (that would be the X and Y part of the evaluation).

##### Concrete examples of how µMatrix's matrix-based filtering differs from HTTPSB's matrix-based filtering 

Any explicit rules created in the global scope will be seen in **all** narrower scopes.

More generally, any explicit rules created in a broader scope will be seen in related narrower scopes. Rules in `example.com` will be seen by the `www.example.com` scope. And so on. This is important to remember when you create rules.

As a result, now creating rules in narrower scopes is the natural way to use µMatrix. Since rules created in the global scope `*` will be seen everywhere, then global rules are useful for some specific cases. 

For example, when using the browser's _"Translate to [Specific language]"_ option in the contextual menu, the browser will send a request to `translate.googleapis.com` to do the job. If you whitelist `xhr` for `translate.googleapis.com` in the global scope, then the feature to translate a page using the contextual menu will work in all scopes (that is, unless a explicit block rule exists in a narrower scope). This was not possible in HTTPSB, because rules in the global scopes were not visible to narrower scopes.

#### A new `1st-party` row

Related HTTPSB issue: [#221](https://github.com/gorhill/httpswitchboard/issues/221).

In HTTPSB, if you wished to auto-whitelist the domain of the web page, you had to enable the setting _"Auto whitelist page domain"_. This setting is now gone, and a `1st-party` row is now used in the matrix to create whatever rules you want for net requests which are 1st-party to a web page.

To auto-whitelist the domain of the web page is simply a matter of whitelisting the `1st-party` cell in the global scope. With just this one rule now all net requests which are 1st-party to a web page will be allowed (unless overriden by a narrower rule as usual). So as opposed to before with HTTPSB, no temporary rules are created to auto-whitelist: your ruleset is kept clean and tidy.

Note that the `1st-party` row will be available in all scopes. The rules for that row are typically set in the global scope, but I chose to make it available in narrower scopes in case a user wants to override 1st-party rules in a narrower scope.

#### No more restriction on effective domain boundaries

Related HTTPSB issue: [#109](https://github.com/gorhill/httpswitchboard/issues/109).

Unlike HTTPSB, µMatrix does not enforce effective domain boundary for rules. Though the matrix UI does enforce effective domain boundary, you can manually create rules which apply to a whole [TLD](http://en.wikipedia.org/wiki/Top-level_domain) for instance, and this will be properly evaluated by the matrix-based filtering engine without any restriction.

For example, the rules...

- `* biz * block`: will block all net requests which are made to a hostname which ends with `.biz`.
- `org * * allow`: will allow everything whenever the scope ends with `.org` (just an example, that would not be a recommended thing to do).

In short, with µMatrix, do whatever you want.

#### There is no longer "scope" data structures internally

In HTTPSB, scopes were mapped to discrete data structures internally, which were used to sandbox rules -- and as a consequence preventing scopes to inherit rules from broader scopes. There was a resource cost when creating a scope, and when evaluating a net request.

There is no more concrete data structure for scopes in µMatrix: all scopes virtually exist at all time, so in µMatrix there is no longer a resource cost associated with scope creation -- because there is no scope creation. This also eliminate the need for settings such as:

- _"Auto create temporary [domain | site]-level scope"_
- _"Copy all rules from global scope into newly created local scopes"_
- _"Auto delete unused temporary scopes"_

Al these settings are now gone.

The scope selector in the matrix popup is simply used to select where a rule should be created. As a convenience, µMatrix will remember the scope level you last selected and select it automatically next time you open the matrix popup.

#### "Strict blocking" is now the only available mode

There was not much real use for disabling ["strict blocking"](https://github.com/gorhill/httpswitchboard/wiki/%22Strict-blocking%22-illustrated), except for when a user wanted to fully auto-whitelist 1st-party requests when `frame` (or whatever request type) was globally blacklisted (blacklisting 3rd-party `frame` is a good habit security-wise).

Now with the `1st-party` row, it's just a matter of whitelisting `* 1st-party frame`, which will override the global blacklisting of the `frame` type, and thus it has become possible to fully whitelist a domain despite the presence of blacklisted request types.

So _"Enable strict blocking"_ is now gone, and strict blocking is how the matrix naturally works.

#### "Ubiquitous rules" tab replaced by "Hosts files" tab

Because this is essentially what the tab has become with pattern-based filtering removed. The code to manage external lists has been imported from µBlock, so the tab functions pretty much the same now.

All hostnames in selected hosts files are interpreted as blacklisted hostnames in the global scope, so they propagate to narrower scopes just like in HTTPSB.

Just as with µBlock, you can specify URLs to external hosts file-compliant resources.

#### "Scoped rules" tab replaced by "My rules" tab

Since now scopes are gone, the over-complicated _"Scoped rules"_ tab has been replaced by the simpler _"My rules"_ tab, which will allow you to plainly edit/add/remove rules, manually if you wish.

Further reading: [Rules-syntax](https://github.com/gorhill/uMatrix/wiki/Rules-syntax).

#### Per-scope switches

Ability to enable/disable user agent-spoofing and referrer spoofing on a per-scope basis. These settings applied only globally in HTTP Switchboard. They still apply globally, but they can now be overridden on a per-scope basis.

#### Preset rulesets are gone for the time being

The preset rulesets are gone for the time being, due to re-factoring. Given how rules have been redesigned with µMatrix, it will be easier to design preset rulesets to unbreak web pages or portion of web pages (i.e. Disqus, etc.)

I just want to get it right for long-term, and think all this through carefully. The writing of preset rulesets was over-complicated in HTTPSB, and also there was no mechanism to integrate external preset rulesets.

Specific regions may have their own useful preset rulesets etc. So the goal will be to make it very simple for the community to create their own preset rulesets, and for µMatrix to make it easy for a user to subscribe to any external preset rulesets.