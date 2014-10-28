Rules is used in a broad sense here: let's rather call them "directives". Most directives will be rules, hence I used "Your rules" in the dashboard.

Each line is a directive. Empty lines will be skipped. The `#` can be used for commenting, and for each line, the parser will ignore the first occurrence of `#` and everything following it.

A directive starts with a directive keyword, immediately followed by the `:` which character is used to tell a parser that we are dealing with a directive keyword.

There are currently two directives: `rule:` and `switch:`. However, the `rule:` directive can be omitted, because it is implicit when there is no directive. Since most directives will be rules, it would be inconvenient to be forced to use `rule:` for each rule.

In the documentation below the square brackets (`[]`) are used to denote optional fields. Curly brackets (`{}`) are used to denote what should appear at a specific position.

#### Directive `rules:` syntax

[`rules:`] {white spaces} source hostname {white spaces} destination hostname {white spaces} [request type {white spaces} [action]]

