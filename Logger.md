uMatrix version 0.9.0.0 comes with a completely new logger.

This new logger is forward-looking, i.e. it will log events only when it is actually opened. This is a more efficient approach than logging everything even when the user does not care about inspecting the network events -- which used to be the case. So now the memory/CPU overhead of logging is incurred if and only if the logger is being used (opened).

Also, the logger is now _unified_:

- All events of interest are being logged, not just network traffic.
- All events from everywhere are logged in one place, no need to select which tab to inspect.
    - This is particularly useful to relate together behind-the-scene event to ongoing network traffic.

##### Special status indicators

The _eye-slash_ indicator means the entry is a behind-the-scene network request.

The _x_ indicator means the entry belongs to a tab which has been closed. You may cleanup such entries from the logger using the _x_ icon in the toolbar.

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
