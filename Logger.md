uMatrix version 0.9.0.0 comes with a completely new logger.

This new logger is forward-looking, i.e. it will log events only when it is actually opened.

This is a more efficient approach than logging everything even when the user does not care about inspecting the network events -- which used to be the case. So now the memory/CPU overhead of logging is incurred if and only if the logger is being used (opened).

Also, the logger is now _unified_:

- All events of interest are being logged, not just network traffic.
- All events from everywhere are logged in one place, no need to select which tab to inspect.
    - This is particularly useful to relate together behind-the-scene events to ongoing network traffic.

#### Advantages of a unified logger

No events lost: all events from all origins are logged in one place, so they all get logged. Previously you had to select the tab which to inspect, which means all events from other tabs -- including from behind-the-scene origin -- were lost.

Since no events is lost, one can now easily spot what add-ons are doing behind-the-scene. If an add-on constantly phone home while you surf the net, you will be able to see this easily.

This also allows to easily relate events from different origins. For example, when surfing GitHub, I can see behind-the-scene network requests being made while surfing GitHub. Though uMatrix/uBlock can't tell the behind-the-scene events are related to GitHub, a user can tell.

This allows to see fully chains of redirects. The network requests for root document will just appear one after another in the logger.

This allows to easily see the URL of popup windows, and from there one can create custom filters using the information in the logged entries.

#### Special status indicators

The _eye-slash_ indicator means the entry is a behind-the-scene network request.

The _x_ indicator means the entry belongs to a tab which has been closed. You may cleanup such entries from the logger using the _x_ icon in the toolbar.

It is possible to click on the status indicator area to open the matrix for the associated tab (if any). The matrix will open in _sticky_ mode, i.e. you can keep it opened permanently. The opened matrix will reflect the state of a specific tab in the browser, so log entries which are not related to that tab will be dimmed.

#### Filter expressions

You can filter entries in the logger using filter expressions. Log entries which do not match _all_ filter expressions will be hidden from view. Syntax for a filter expression:

- Enter `foo` to only show entries which have a string `foo`.
- Enter `|foo` to only show entries which have a field starting with `foo`.
    - Tip: use `|--` to show only entries which were blocked.
- Enter `foo|` to only show entries which have a field ending with `foo`.
- Enter `|foo|` to only show entries which have exactly a field with `foo`.
- Prefix any expression with `!` to reverse the meaning of the expression.
    - `!foo` means display only entries which do not have the string `foo` in it.
    - `!|--` means display only entries which were **not** blocked.
- When more than one filter expression appear, a logical _and_ between the expressions is implied.

Examples:

- `!|-- facebook`: show only non-blocked entries with the string `facebook` in it.
- `|xhr google`: show only entries of type `XMLHttpRequest` with the work `google` in it.
- `!|image !|css`: show only entries which are not of type `image`, neither `css`.