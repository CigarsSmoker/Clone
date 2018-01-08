It may happen that a page is still broken after force-reloading once you have created all the needed _allow_ rules for it.

Here are some things to consider.

- Did you use [the logger](https://github.com/gorhill/uMatrix/wiki/Logger) to ascertain that really **nothing** is blocked or modified?
    - Using the logger is the **first** step when having trouble to un-break a site.
- Did you verify that one or more per-scope switches are also interfering?
    - Keep in mind that the [per-scope switches](https://github.com/gorhill/uMatrix/wiki/Per-scope-switches) are independent of the matrix filtering switch, so stuff can still be blocked/modified when per-scope switches are enabled.
- Did you try to bypass the browser cache when you forced a reload of the page?
    - Sometimes it may be necessary to tell the browser to bypass its cache.
    - For example, see <https://github.com/gorhill/uMatrix/issues/893>.
    - Firefox-specific: I also found that sometimes opening the broken page in a new tab fix a breakage issue.
- Did you enable matrix filtering in the behind-the-scene scope?
    - If you enable matrix filtering in the behind-the-scene scope, you may suffer more obscure breakage as a result.
    - As mentioned above, using the logger is key.
