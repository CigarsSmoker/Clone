# Idea
Instead of starting with a permissive model, start with a _very_ restrictive model and whitelist as necessary.

# Default ruleset
Go to the uMatrix panel and select the global scope. Deselect everything except 1st-party CSS.

# How to work with this
Open a new page. It might look horribly broken, but don't panic! Look at the uMatrix panel for third party CSS resources (anything with a number in it in the CSS column is probably useful). Select the CSS box for those (sub)domains. Reload. Hopefully, the site looks decent now!

The next step is images. Again, toggle specific (sub)domains until the site looks reasonable.

# To save or not to save?

If this is a site you visit fairly often, you should probably save the rules so that you don't have to go through this too often. Otherwise, I wouldn't bother - the fewer the rules, the less the potential for unexpected things to happen.

# Concrete example
[Coming soon]