uMatrix version 0.9.0.0 comes with a completely new logger.

[blah blah blah]

##### Filter expressions

You can filter entries in the logger using filter expressions. Log entries which do not match _all_ filter expression will be hidden from view. Syntax for a filter expression:

- Enter `foo` to only show entries which have a string `foo`.
- Enter `|foo` to only show entries which have a field starting with `foo`.
    - Tip: use `|--` to show only entries which were blocked.
- Enter `foo|` to only show entries which have a field ending with `foo`.
- Enter `|foo|` to only show entries which have exactly a field with `foo`.
- Prefix any expression with `!` to reverse the meaning of the expression.
    - `!foo` means display only entries which do not have the string `foo` in it.
    - `!|--` means display only entries which were **not** blocked.
- When more than one filter expression appear, a logical _and_ between the expressions is implied.
