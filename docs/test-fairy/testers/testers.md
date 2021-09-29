---
id: testers
title: Testers
sidebar_label: Testers
---
## Managing Testers
To see all the testers you have for your app, invite new testers or import/export a list of testers, click on the **TESTERS** tab.

![ alt upload](../../img/app/invite-testers.png)

### Inviting Testers by Email

To invite testers by email click on the `Add Testers` Button.
In the list box add tester emails  - one for each row.

You can also select a Group for the testers in the list or just leave it blank (see **Managing tester groups** below).
After you finished press the `Add Testers` button below the list to complete the process.

You can add testers manually or [import lists of testers](https://app.testfairy.com/testers/import/) in csv format.

______        
###### **Note for iOS only**
  If you are **not** using an [iOS Enterprise certificate](https://developer.apple.com/programs/ios/enterprise/), you  will need to get the UDID's of your testers' devices before sending them your app.   
         When you invite new testers by email, your testers will get an email asking them to register their device. Once they click on the registration link, you will get an email with their UDID and their device details will be added to your [testers page](https://app.testfairy.com/testers).  
         For more information about how to add UDIDs to provisioning profiles please read [this guide](http://docs.testfairy.com/iOS_SDK/Adding_UDIDs_to_iOS_development_profile.html).
______

![ alt upload](../../img/app/invite-testers2.png)

<a id="managing-testers"></a>


### <a name="managing-tester-groups"></a> Managing tester groups

You can also divide testers to **groups** to add more structure and organise your testing efforts.
In order to create a group click in the GROUPS text-box and then on `Create new group...`
Choose a group name and pree OK. The tester you clicked in his group will be assigned the group you just created.

![alt tester group](../../img/app/tester-groups-1.png)

Tester groups help you manage the invitation process to your apps. If you want to invite a number of testers that are all under the same group simply filter the list of testers according to that group and then select all and invite them.

![alt invite group](/img/app/tester-group-2.png)

In order to delete a group you will first have to delete all its mentions in the GROUPS field. Delete the group by pressing the x next to its name. Once you have delete all its occurrences it will be deleted. Refresh the page to make sure it was deleted.

![ alt delete group](../../img/app/delete-group.png)


**What you should read next:** [How To Analyze Test Results](How_To_Analyze_Test_Results.html).

## Registering Your iOS Device UDID Number
<!---iframe width="854" height="480" src="https://www.youtube.com/embed/YqhiGrh7vjc" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe--->

<iframe width="800" height="600" frameborder="0" allowfullscreen="true" style="box-sizing: border-box; margin-bottom:5px; max-width: 100%; border: 1px solid rgba(0,0,0,1); background-color: rgba(255,255,255,0); box-shadow: 0px 2px 4px rgba(0,0,0,0.1);" src="https://testfairy.fleeq.io/l/0drh0k8ux8-f0t37mznbz"></iframe>


### Registering your device

In order to start testing with TestFairy, you need to be invited by an app developer.
Once you receive an invitation via email or landing page, download or register your device, if you are requested to do so.
This is a very quick and simple process, which you will only have to do once.
Some apps won't require you to register your device. In this case, simply click on the download link and follow the instructions on screen.

### When asked to register your device

1. Open the invitation email and follow the link to //**register your mobile device in TestFairy**//.
2. Make sure you open the link with the **Safari** browser.
3. The link will open your tester dashboard at [my.testfairy.com](https://my.testfairy.com) and display the `Register device` button. Click it to initiate the download.
4. You will be prompted to download the TestFairy configuration profile. Click the **Allow** button to download it.
5. Once the profile was downloaded go to the **settings app** and  go to the **General** --> **Profiles** menu.
6. On the right side you will see a list of profiles with a section of **Downloaded Profiles**. Press the **TestFairy** profile that is located there.
7. The profile installer will open. Click on **Install**.
8. Your device is now registered in TestFairy. Please wait for the developer to send you a download link.


### Downloading apps

First, make sure you receive an email from the app developer, which [invites you](/App_Distribution/Distributing_Your_Apps.html) to test an application build.

1. Click the “DOWNLOAD APP” link in the email.
2. Click the “Download App" button in your Safari browser.
3. You will be prompted to install the application. Click “Install”.
4. The app icon should now appear on your device desktop.


### Troubleshooting installation

<iframe width="800" height="600" frameborder="0" allowfullscreen="true" style="box-sizing: border-box; margin-bottom:5px; max-width: 100%; border: 1px solid rgba(0,0,0,1); background-color: rgba(255,255,255,0); box-shadow: 0px 2px 4px rgba(0,0,0,0.1);" src="https://testfairy.fleeq.io/l/8kblwik5sc-d1udj9q6hh"></iframe>

If the application does not install on your device, we recommend that you run the troubleshooting tool:

1. Open your TestFairy account via the link [my.testfairy.com](https://my.testfairy.com) on the device you want to test.
2. Click the Tester icon ![](/img/tester/tester-icon-1.png) menu and choose **Troubleshooting**.
3. Click the `START` button to start the troubleshooting process.
4. Click **allow** to let the configuration profile download.
5. Close and go to the **settings app**. Click on the **profile downloaded** menu.
6. Install the configuration profile.
5. After install is complete, you will be directed to review the the troubleshooting results.


## How to test Android apps
<iframe width="854" height="480" src="https://www.youtube.com/embed/65Jz4_o0_Z0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>


### Downloading apps

You should receive an email from the application developer, inviting you to test an application build.

  1. Click the “Download App” link in the email.

  2. Save the application.

  3. Open the application.

  4. You will now be prompted to install the application. Click “Install”.

  5. The application icon should now appear on your device desktop.  

### Creating a tester's account

1. Once you've been invited to test an application via TestFairy, you can create a TestFairy account to see your invitations, open bugs, download applications, and more. Open the invitation you've received for testing a new build, and click the ["tester account"](https://my.testfairy.com/) link.

  <img src="/img/tester/invitation-email.png" width="300"/>

2. Click on ["I am a tester, I do not know my password"](https://my.testfairy.com/forgot-password) and submit your email address.
  You will receive an email with instructions for setting a new password for your tester account.

### Troubleshooting installation

* If the application does not install on your device, please check if you already have the same application installed with the same name, and remove it.

* If you are getting an "Installation blocked" message:

   <img src="/img/tester/60-unknown-sources-msg.png" width="300"/>

    * Go to "Settings" on your device
    * Choose "Security"
    * Look for "Unknown sources"
    * Activate "Allow installation of apps from sources other than the Play Store"
    * Re-install the application

    <img src="/img/tester/61-unknown-sources-android.png" width="300"/>




## Submitting User Feedback
<!-- ## Reporting Bugs -->

### Shake to create Feedback

When the [TestFairy SDK](https://docs.testfairy.com/SDK/Adding_The_SDK_To_Your_App.html) is defined in your app shaking the device will prompt the user to create a feedback issue from within the app.
The issue will appear with an automatically generated screenshot of the app which can be annotated and a feedback form where details like email and description can be added.

<iframe width="854" height="480" src="https://www.youtube.com/embed/lVlXx01jrU8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

It is also possible to automatically integrate [Bug Tracking](https://docs.testfairy.com/Bug_Tracking/Overview.html) systems to your issues so when they are created the issues are passed automatically.  


**What to read next:**
[Build Settings](Build_Settings.html)
