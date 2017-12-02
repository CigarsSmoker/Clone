Sometimes it may happen that you need to access the popup panel of uMatrix for a popup browser window.

Unfortunately, it is often the case that some popup browser windows won't have a toolbar, and this means it is not possible for you to access you extensions' toolbar icon and their popup panel.

In the case of uMatrix, this can be crippling given that you might need to set rules to un-break a site loaded in a popup browser window.

There is a workaround for this situation though, but you need to find a way to launch uMatrix's logger -- this can be done from any browser window for which the toolbar is visible:

![a](https://user-images.githubusercontent.com/585534/33516598-7172ce30-d743-11e7-8240-35d6dbec43fd.png)

Once you have the logger opened, force a refresh of the content of your toolbar-less popup window (<kbd>F5</kbd> should do the job). This will cause the logger to be filled with entries which are related to the content of the popup window.

Next, find any entry related to the popup window (you can use the dropdown list at the top of the logger to see only entries for a specific web page), and click the second cell of any row:

![a](https://user-images.githubusercontent.com/585534/33516619-db581a26-d743-11e7-920b-a5f91ac41552.png)

This will bring up a fully functioning embedded popup panel for the web page associated with the entry you clicked (there is currently a regression -- the popup panel does not resizing properly, fixed in current dev build):

![a](https://user-images.githubusercontent.com/585534/33516656-707e44c2-d744-11e7-83ec-7d8761265f01.png)

From there you can add/remove rules to un-break the web page loaded in the popup browser window. Once you have unbroken whatever was loaded in that popup browser window, you might want to commit all your changes so that next time you do not need to go through all these steps.