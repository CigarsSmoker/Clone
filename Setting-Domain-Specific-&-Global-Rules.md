The example below demonstrates how to create rules within uMatrix for either [Domain Specific Rules](https://github.com/gorhill/uMatrix/wiki/Setting-Domain-Specific-&-Global-Rules#setting-domain-specific-rules) or [Global Rules](https://github.com/gorhill/uMatrix/wiki/Setting-Domain-Specific-&-Global-Rules#setting-global-rules) which allows a user to achieve desired site functionality (_e.g._ The user wants to be able to always play embedded youtube videos on a website) 

## Setting Domain Specific Rules
For the steps below we will use an [example website](http://digg.com/video/free-climber-pass) which has a youtube video embedded on the page.

1. **Select the Domain** 

From the uMatrix panel in the top left corner, make sure the selection is a blue domain which should show the website domain you are currently on.

![step01_panel_onedomain](https://cloud.githubusercontent.com/assets/6795795/25504703/eb3f9b18-2b6c-11e7-8659-92d34ff358aa.png)

***

2. **Whitelist Rules**

Select the rules you want to allow from the 3rd party domain. 

![step02_whitelistrules_onedomain](https://cloud.githubusercontent.com/assets/6795795/25504705/eb426ad2-2b6c-11e7-99e1-1dd33bc7f059.png)

_In example above we are allowing scripts and frames to load from 'www.youtube.com' on 'digg.com' **only**._

***

3. **Save the Rules**

Click the unlocked padlock icon from the uMatrix panel to permanently save the new rules you have just allowed.

![step03_saverules_onedomain](https://cloud.githubusercontent.com/assets/6795795/25504711/eb563224-2b6c-11e7-8a14-88622f4f8a17.png)

**Alternative Method**

Open the uMatrix dashboard and click on the 'My rules' tab. Make your temporary rules permanent by committing them by clicking on the 
![step03_commit](https://cloud.githubusercontent.com/assets/6795795/25504706/eb428db4-2b6c-11e7-868d-20be7594e9de.PNG) button.

![step03alt_saverules_onedomain](https://cloud.githubusercontent.com/assets/6795795/25504709/eb53a28e-2b6c-11e7-92b1-c88baa65b889.PNG)

_The above method to make rules permanent is an **alternative** approach to clicking the padlock icon from the uMatrix Panel_ 

***

4. **Refresh the Page**

Click the ![step04_refresh](https://cloud.githubusercontent.com/assets/6795795/25504712/eb584654-2b6c-11e7-87d3-cdea667edf26.png) icon in the uMatrix Panel to refresh the [example website](http://digg.com/video/free-climber-pass) and test if the rules you have set allow the desired site behavior.

***

5. **Repeat Steps 1-4 as Needed**

Repeat **Steps 1-4** until the website functions in the desired manner -- For this example, we want the youtube video to fully load and allow playback in the [example website](http://digg.com/video/free-climber-pass).

![step05_youtube_onedomain](https://cloud.githubusercontent.com/assets/6795795/25504713/eb60db98-2b6c-11e7-8921-18f411e490d6.png)

_Scripts for domains 'www.youtube.com', 'youtubei.youtube.com' & 's.ytimage.com' as well as XHR requests for 'googlevideo.com' & 'www.youtube.com' and frames for 'www.youtube.com' have now been allowed on 'digg.com' **only**._


### Rules you set following the steps above should now only apply to the **selected** website.' (In this example, digg.com) 
***
***


## Setting Global Rules 

For the steps below we will use an [example website](http://digg.com/video/free-climber-pass) which has a youtube video embedded on the page.

1. **Select the Global Domain** 

From the uMatrix panel in the top left corner click the blue domain which should show the website domain you are currently on and select '*' instead of the domain you are currently on.

![step01_panel_global](https://cloud.githubusercontent.com/assets/6795795/25504702/eb3cc6ae-2b6c-11e7-9757-cbc740abeed9.png)

***

2. **Whitelist Rules**

Select the rules you want to allow from the 3rd party domain. 

![step02_whitelistrules_global](https://cloud.githubusercontent.com/assets/6795795/25504704/eb3ff162-2b6c-11e7-94da-062444c1ce65.png)

_In example above we are globally allowing scripts and frames to load from 'www.youtube.com'_

***

3. **Save the Rules**

Click the unlocked padlock icon from the uMatrix panel to permanently save the new rules you have just allowed.

![step03_saverules_global](https://cloud.githubusercontent.com/assets/6795795/25504707/eb46c848-2b6c-11e7-81b6-857cf5c996b0.png)

**Alternative Method**

Open the uMatrix dashboard and click on the 'My rules' tab. Make your temporary rules permanent by committing them by clicking on the 
![step03_commit](https://cloud.githubusercontent.com/assets/6795795/25504706/eb428db4-2b6c-11e7-868d-20be7594e9de.PNG) button.

![step03alt_saverules_global](https://cloud.githubusercontent.com/assets/6795795/25504708/eb50f516-2b6c-11e7-9f78-e3b825a36a2c.PNG)

_The above method to make rules permanent is an **alternative** approach to clicking the padlock icon from the uMatrix Panel_ 

***

4. **Refresh the Page**

Click the ![step04_refresh](https://cloud.githubusercontent.com/assets/6795795/25504712/eb584654-2b6c-11e7-87d3-cdea667edf26.png) icon in the uMatrix Panel to refresh the [example website](http://digg.com/video/free-climber-pass) and test if the rules you have set allow the desired site behavior.

***

5. **Repeat Steps 1-4 as Needed**

Repeat **Steps 1-4** until the website functions in the desired manner -- For this example, we want the youtube video to fully load and allow playback in the [example website](http://digg.com/video/free-climber-pass).

![step05_youtube_global](https://cloud.githubusercontent.com/assets/6795795/25504710/eb54d564-2b6c-11e7-8a2c-48a0613b2ca1.png)

_Scripts for domains 'www.youtube.com', 'youtubei.youtube.com' & 's.ytimage.com' as well as XHR requests for 'googlevideo.com' & 'www.youtube.com' and frames for 'www.youtube.com' have now been **globally** allowed._

***

### Rules you set following the steps above should now be global and **apply to all websites**.
***
***


Please keep in mind that out of the box, uMatrix is a powerful third party script blocker that may impact the full functionality of many websites. Because of this it is designed and intended to be used by **advanced** users. 