#### Scope selector

![b](https://user-images.githubusercontent.com/585534/33210614-f90bb638-d0e8-11e7-8639-8566c3577cd3.png)

The scope selector allows you to pick the scope to visualize which rules are part of, or propagate to that scope, and also from which scope rules will be added/removed when you click on a cell in the matrix.

As per uMatrix rule-propagation logic, rules from a broader scope propagate to narrower scope, unless of course there is an explicit rule on the way.

Given a rule `source destination type action`, the scope selector controls the `source` part of that rule.

#### The "all" cell

![b](https://user-images.githubusercontent.com/585534/33210981-667e08d2-d0ea-11e7-8fb5-dc563916405e.png)

The _all_ cell allows you to set the default rule which will affect all other cells in the matrix for the current scope. 

As per uMatrix rule-propagation logic, all cells for which there is no explicit rules will inherit the state of the _all_ cell.

Given a rule `source destination type action`, the _all_ cell means that `source`, `destination`, and `type` are all `*`.

The "type" cells

![b](https://user-images.githubusercontent.com/585534/33211240-a160542c-d0eb-11e7-99f3-c237113076b8.png)

Given a rule `source destination type action`, a _type_ cell controls the `type` part of that rule.

Currrently, the _type_ cells translates into these network request types internally:

