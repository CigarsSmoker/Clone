The extension icon in the toolbar gives an overview of how uMatrix affected a page:

![a](https://user-images.githubusercontent.com/585534/37707788-bbb0ff66-2cda-11e8-9b1d-f366a26d9b68.png)

The red and green areas provide a rough overview of how many resources were blocked (reddish) versus how many resources were not blocked (greenish).<sup>[1]</sup>

The badge number tells the number of resources which were blocked/modified. This number will typically match what is reported in uMatrix's logger.

You can turn off the badge number in the _Settings_ pane in uMatrix's dashboard.

***

<sub>[1] Keep in mind that "resources blocked" is a generic expression which includes removal/modifcation of response and request headers.</sub>