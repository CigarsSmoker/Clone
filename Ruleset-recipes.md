[documentation is currently being fleshed out]

Ruleset recipes ("recipes" thereafter) are community-contributed rulesets suggested to you when you visit a given web site. Recipes are specific, they contain only the necessary rules to un-break a specific web site or behavior.

When one or more recipes are available for a given web site, they will be suggested to you in the popup panel (through the _puzzle_ icon), such that you can inspect the rules and easily import them into your own ruleset if you agree with the rules.

![Example](https://user-images.githubusercontent.com/585534/37831619-9417b488-2e7c-11e8-928a-1eb8e39a732c.png)

Recipes are _never_ automatically imported, they always require that you explicitly import them. You may inspect all the rules by expanding the recipe.

When you import a recipe, the rules are always imported into your temporary ruleset.

Some recipes may contain rules which are not visible from the current matrix, or contain rules which affect multiple scopes. Here is an example of such recipe, already present as a stock one:

    Youtube with account
        youtube.com *
            example.com 1st-party script
            example.com googlevideo.com *
            example.com googlevideo.com xhr
            accounts.google.com 1st-party *
            accounts.google.com 1st-party cookie
            accounts.google.com gstatic.com *
            accounts.google.com gstatic.com script

When you import this recipe (let's say into the `example.com` scope), temporary rules will be created in the current scope, and rules will also be created in the `accounts.google.com` scope (to allow logging in the current case). If you are satisfied that all the rules in the recipe are to be kept permanently, click the padlock icon _aside_ the recipe, this will save all the rules for that specific recipe. If you were to use the popup panel padlock, only the rules which are currently visible in the popup panel would be saved.

## Contributing recipes

Everybody is free to create whatever ruleset they see fit.

Given this, it is impossible to guarantee that any given recipe will un-break a given web site as intended by the recipe author. Hence there are some guidelines about contributing recipes that are likely to work for most users. If a recipe does not work as intended because they are imported into rather restrictive personal ruleset, this will be for the user to work out.

Recipe authors should craft their recipes as if they were to be imported in the following ruleset -- this will be the most restrictive destination ruleset supported by recipe contributors:

    * * * block
    * * script block
    * * frame block
    * first-party * allow
    * first-party frame allow

This is the most restrictive destination ruleset supported: all 3rd-party resources are blocked, all scripts (1st- and 3rd-party) are blocked, and all 3rd-party frames are explicitly blocked.

In order to minimize the amount of rules to be imported, recipes should list the necessary rules from broadest to narrowest -- uMatrix will always discard rules from a recipe which are not necessary given the content of the destination ruleset.

Here is an example using an existing stock recipe:

    Vimeo as 3rd-party
        * player.vimeo.com
            _ player.vimeo.com *
            _ player.vimeo.com script
            _ player.vimeo.com frame
            _ vimeocdn.com *
            _ vimeocdn.com script

The first line is the name of the recipe, to be used in the popup panel. It must make the purpose of the recipe obvious.

The second line is the condition which tells uMatrix when a recipe should be presented to the user in the popup panel. It's made of two parts: the 1st-party hostname and the 3rd-party hostname which must be matched in the current matrix for the recipe to be considered relevant.

In the specific example above, the condition to match is `* player.vimeo.com`, which means: the recipe is relevant for any given scope in which `player.vimeo.com` is a 3rd-party.

The other lines are rules to be imported.

The special underscore symbol `_` is a scope placeholder, it is meant to be replaced by the scope currently selected in the popup panel.

Once a user imports a recipe, uMatrix will evaluate each rule in order of appearance, and determine whether it must be imported according to whether the resources specified in a rule is currently blocked or not. If a resource is not blocked, the rule won't be imported.

For example, if a user imports the above recipe into the default ruleset (the one in effect when you first install uMatrix), the rule `[current scope] player.vimeo.com script allow` won't be imported, because the rule `[current scope] player.vimeo.com * allow` will already have caused the `[current scope] player.vimeo.com script` cell to be allowed, and similarly the rule `[current scope] vimeocdn.com script allow` won't be be needed.

Recipe contributors must never specify globally-scoped rules in their recipes, unless such behavior is made _very clear_  by the recipe name. For example, the following recipe could be crafted to whitelist some popular CDN:

    Globally whitelist jsDelivr CDN
        * cdn.jsdelivr.net
            * cdn.jsdelivr.net *
            * cdn.jsdelivr.net script

Note the use of the word _globally_ in the recipe name, and also note that global scope `*` was used as the scope in the rules rather than the placeholder `_` typically found in non-global recipes.