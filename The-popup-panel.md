![a](https://user-images.githubusercontent.com/585534/33213085-ff74afd8-d0f3-11e7-8232-4c204925d274.png)

### Scope selector

![b](https://user-images.githubusercontent.com/585534/33210614-f90bb638-d0e8-11e7-8639-8566c3577cd3.png)

The scope selector allows you to pick the scope to visualize which rules are part of, or propagate to that scope, and also from which scope rules will be added/removed when you click on a cell in the matrix.

As per uMatrix rule-propagation logic, rules from a broader scope propagate to narrower scopes, unless of course there is an explicit rule on the way.

Given a rule `source destination type action`, the scope selector controls the `source` part of that rule.

***

## The matrix cells

![b](https://user-images.githubusercontent.com/585534/33214668-e5e3fa68-d0fa-11e7-8c73-d703988b5855.png)

The matrix is made of cells, and the color of a cell tells whether the cell will result in a _block_ or _allow_ action:
- Dark red: the cell is affected by a _block_ rule.
- Pale red: the cell inherit a _block_ rule by virtue of uMatrix's rule-propagation logic.
- Dark green: the cell is affected by an _allow_ rule.
- Pale green: the cell inherit an _allow_ rule by virtue of uMatrix's rule-propagation logic.

The matrix is a view on the current state of the temporary ruleset. The temporary ruleset is always what uMatrix uses to decide whether a network request must be blocked or allowed.

The matrix will however also show you the permanent rule assigned to a cell, if any: the little triangle in the top left corner of a cell when present represent a permanent rule that exists for that cell.

***

### The "all" cell

![b](https://user-images.githubusercontent.com/585534/33210981-667e08d2-d0ea-11e7-8fb5-dc563916405e.png)

The _all_ cell allows you to set the default rule which will affect all other cells in the matrix for the current scope, and related narrower scopes as per rule-propagation logic.

As per uMatrix rule-propagation logic, all cells for which there is no explicit rules will inherit the state of the _all_ cell.

Given a rule `source destination type action`, the _all_ cell means that `source`, `destination`, and `type` are all `*`.

***

### The "type" cells

![b](https://user-images.githubusercontent.com/585534/33211240-a160542c-d0eb-11e7-99f3-c237113076b8.png)

Given a rule `source destination type action`, a _type_ cell controls the `type` part of that rule.

Currently, the _type_ cells translates into these network request types internally:

| matrix header | rule type   | browser resources  |
| ------------- |:----------- |:------------------ |
| (invisible)   | `doc`       | root document      |
| cookie        | `cookie`    | cookies,<br>local storages (as browser API allows) |
| css           | `css`       | stylesheets,<br>fonts |
| image         | `image`     | images |
| media         | `media`     | audio (`<audio>`),<br>video (`<video>`),<br>plugins (`<object>`, `<embed>`) |
| script        | `script`    | scripts |
| XHR           | `xhr`       | [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest), [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) |
| frame         | `frame`     | embedded documents (`iframe`, `frame`) |
| other         | `other`     | everything [which does not fit in previous types](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/API/webRequest/ResourceType#):<br>beacons,<br>[CSP reports](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-uri),<br>[ping](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-ping),<br>[Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest),<br> [XBL](https://developer.mozilla.org/en-US/docs/Mozilla/Tech/XBL),<br> [DTD](https://developer.mozilla.org/en-US/docs/Glossary/DTD),<br>[XSLT](https://developer.mozilla.org/en-US/docs/Web/XSLT), and other unspecified types |

***

### The "destination" cells

The _destination_ cells allow to easily set allow/block rules to allow/block all types of resources from a specific destination.

![b](https://user-images.githubusercontent.com/585534/33212262-36b6cc32-d0f0-11e7-833c-ea316995a9a4.png)

When a network request is made to a specific destination, uMatrix will report the hostname at which the network request was made, and all the intermediate subdomains (if any) up to the base domain.

Rules on a base domain or subdomains propagate to all descendant subdomains. Generally, if you trust a base domain, it is convenient to set an _allow_ rule to it, so that all subdomains are also allowed as per rule-propagation logic.

Again, keep in mind that rules from broader scopes propagate to narrower scopes, so for some it might be convenient to set an _allow_ rule in the global scope for a base domain they completely trust, for example this is convenient for content delivery network ("CDN") which use is widespread: `* jquery.com * allow` (but really this is a matter of opinion, many will argue that it is not good to wholly allow even such popular CDN: in the end, it's your choice).

The _1st-party_ cell and associated cell types is a special row used to assign default rules to whatever is 1st-party to the current site (what is reported in the scope selector). Typically the rules for 1st-party are set in the global scope -- it's a bit weird to set a _1st-party_ rule in a narrower scope, but it is possible after all.

All hostnames which are explicitly blocked are sent at the bottom of the matrix, so as to reduce visual noise for destinations which are of little interest since they have already been blacklisted. You can collapse/expand that section of the matrix. Typically all the blocked rules created as a result of loading hosts files are reported in that section. Keep in mind you can override these built-in block rules as you wish with either a _noop_ rule or an _allow_ rule (you can click the cell to add/remove rules just as with any other cell).

Given a rule `source destination type action`, the _destination_ cell controls the `destination` part of that rule, and the `type` is set to `*` -- meaning "all resources" from that destination will be affected by the rule.

***

## The "destination & type" cells

![b](https://user-images.githubusercontent.com/585534/33214229-068bc20c-d0f9-11e7-8efa-d12d5d443d20.png)

These cells serve to visualize what resource for what destination are allowed/blocked in the current scope. They can also be used to add/remove rules for specific destination and type of resources.

The count reported in these cells represent the number of _distinct_ URLs which were used to connect (or attempted connection) to the remote server.

Typically, it is inconvenient to strictly work at such granularity, one will usually assign rules to whole domains or whole types, but the _destination & type_ are very useful in case overriding an inherited rule from a lower scope or lower precedence cell.

But as usual, it's up to you to make use of this ability to go more granular when you craft your ruleset.

Given a rule `source destination type action`, a _destination & type_ cell controls the `destination` and `type` part of that rule.
