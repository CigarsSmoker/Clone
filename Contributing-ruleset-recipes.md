[just randomly throwing stuff in here for now]

The character `_` is placeholder for "current scope".

The strictest ruleset for which recipes must un-break sites is:

- All 3rd-party requests blocked by default (including images/css)
- All scripts blocked by default (including 1st-party scripts)
- All 3rd-party frames are blocked by default

For any given 3rd-party, if only one type of request is needed, then the rule should allow only that one specific type. Example:

    _ someserver.cdn xhr

For any given 3rd-party, if more than one type of request is needed, two cases:

1. If only passive resources are needed, then the rules should be specifically only for these passive resources. Example:

    _ somescdn.com css
    _ someserver.com image

2. If active resources are needed, then a broad rule should appear before the more specific ones. Example:

    _ somecdn.com *
    _ somecdn.com script
    _ somecdn.com frame

***

Using rules for hostnames which are public suffix list or below is frowned upon, though it is something impractical to stick to this rules. When this happens, a convincing argument in favor of the exception should be made.

In the same vein, type-based rules must be avoided. Bad:

    _ * xhr

If ever this happens to be the only sensible solution to some real issue, then again a convincing argument should be made in favor of such broad rule.

[...]