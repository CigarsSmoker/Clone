### Scope selector

![b](https://user-images.githubusercontent.com/585534/33210614-f90bb638-d0e8-11e7-8639-8566c3577cd3.png)

The scope selector allows you to pick the scope to visualize which rules are part of, or propagate to that scope, and also from which scope rules will be added/removed when you click on a cell in the matrix.

As per uMatrix rule-propagation logic, rules from a broader scope propagate to narrower scope, unless of course there is an explicit rule on the way.

Given a rule `source destination type action`, the scope selector controls the `source` part of that rule.

### The "all" cell

![b](https://user-images.githubusercontent.com/585534/33210981-667e08d2-d0ea-11e7-8fb5-dc563916405e.png)

The _all_ cell allows you to set the default rule which will affect all other cells in the matrix for the current scope. 

As per uMatrix rule-propagation logic, all cells for which there is no explicit rules will inherit the state of the _all_ cell.

Given a rule `source destination type action`, the _all_ cell means that `source`, `destination`, and `type` are all `*`.

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
| media         | `media`     | audio,<br>video,<br>plugins |
| script        | `script`    | scripts |
| XHR           | `xhr`       | [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest), [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) |
| frame         | `frame`     | embedded documents (`iframe`, `frame`) |
| other         | `other`     | everything [which does not fit in previous types](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/API/webRequest/ResourceType#):<br>beacons,<br>[CSP reports](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-uri),<br>[ping](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-ping),<br>[Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest),<br> [XBL](https://developer.mozilla.org/en-US/docs/Mozilla/Tech/XBL),<br> [DTD](https://developer.mozilla.org/en-US/docs/Glossary/DTD),<br>[XSLT](https://developer.mozilla.org/en-US/docs/Web/XSLT), and other unspecified types |

