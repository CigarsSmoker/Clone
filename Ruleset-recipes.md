Ruleset recipes ("recipe(s)" thereafter) are community-contributed rulesets suggested to you when you visit a given web site. Recipes are specific, they contain only the necessary rules to un-break a specific web site or behavior.

When one or more recipes are available for a given web site, they will be suggested to you in the popup panel (through the _puzzle_ icon), such that you can inspect the rules and easily import them into your own ruleset if you agree with the rules. Recipes are _never_ automatically imported, they always require that you explicitly import them.

## Contributing recipes

Everybody is free to create whatever ruleset they see fit.

Given this, it is impossible to guarantee that any given recipe will un-break a given web site as intended by the recipe author. Hence there are some guidelines about contributing recipes that are likely to work for most users. If a recipe does not work as intended because they are imported into rather restrictive personal ruleset, this will be for the user to work out.

Recipe authors should craft their recipes as if they were to be imported in the following ruleset -- this will be the most restrictive destination ruleset supported by recipe contributors:

    * * * block
    * * script block
    * * frame block
    * first-party frame allow

This is the most restrictive destination ruleset supported: all 3rd-party resources are blocked, all scripts (1st- and 3rd-party) are blocked.

In order to minimize the amount of rules to be imported, recipes should list the necessary rules from broadest to narrowest -- uMatrix will always discard rules from a recipe which are not necessary for given the content of the destination ruleset.

Here is an example using an existing stock recipe:

    Vimeo as 3rd-party
        * player.vimeo.com
            _ player.vimeo.com *
            _ player.vimeo.com script
            _ player.vimeo.com frame
            _ vimeocdn.com *
            _ vimeocdn.com script

The first line is the ruleset recipe is the name of the recipe, to be used in the popup panel. It must make the purpose of the recipe obvious.

The second line is the condition which tells uMatrix when a recipe should be presented to the user in the popup panel. It's made of two parts: the 1st-party hostname and the 3rd-party hostname which must be matched in the current matrix for the recipe to be considered relevant.

In the specific example above, the condition to match is `* player.vimeo.com`, which means: the recipe is relevant for any given scope in which `player.vimeo.com` is a 3rd-party.

The other lines are rules to be imported. Once a user imports a recipe, uMatrix will evaluate each rule in order of appearance, and determine whether it must be imported according to whether the resources specified in a rule is currently blocked or not. If a resource is not blocked, the rule won't be imported.

The special underscore symbol `_` is a scope placeholder, it is meant to be replaced by the scope currently selected in the popup panel.