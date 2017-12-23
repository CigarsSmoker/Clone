It may happens that a page is still broken after reload after you have created all the needed _allow_ rules for it.

Here are some things to consider.

- Did you verify that one or more per-scope switches are also interfering?
    - Keep in mind that the [per-scope switches](https://github.com/gorhill/uMatrix/wiki/Per-scope-switches) are independent of the matrix filtering switch, so stuff can still be blocked/modified when per-scope switches are enabled.
- Did you force a bypass of the browser cache when you forced a reload of the page?
    - For example, see <https://github.com/gorhill/uMatrix/issues/893>.
- Did you use [the logger](https://github.com/gorhill/uMatrix/wiki/Logger) to ascertain that really nothing is blocked?
    - Using the logger is the first step when having trouble to un-break a site.