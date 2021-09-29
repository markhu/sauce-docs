---
id: uploading-app
title: Uploading an App
sidebar_label: Uploading an App
---

To upload an app via the TestFairy UI:



We recommend using our <a href="https://docs.testfairy.com/API/Upload_API.html">Upload API</a> to enable our <a href="https://wiki.jenkins-ci.org/display/JENKINS/TestFairy+Plugin">Jenkins plugin</a>, <a href="#">Gradle plugin</a>, or <a href="https://github.com/testfairy/command-line-uploader" target="_blank">Command line uploader</       a>.

The code of our command line uploader, Jenkins and Gradle plugins is open source, so you can feel free to change and improve on it.

## Manual upload process.

### Supported Plaforms

  * **Android**: TestFairy supports uploading and distributing Android Applications. In order to distribute Android apps with TestFairy  apps must be packaged as a `.apk` file.
  * **iOS**: TestFairy supports uploading and distributing iOS Applications. iOS apps can be signed with either __AdHoc__, __Development__ and __Enterprise__ certificates. In order to distribute iOS apps with TestFairy, apps must be packaged as an `.ipa` file.
  * **MacOS**: TestFairy supports uploading and distributing iOS Applications. iOS apps can be signed with either __AdHoc__, __Development__ and __Enterprise__ certificates. MacOS apps are bundled as `.app` files, however, In order to distribute MacOS apps with TestFairy, those `.app` files must be zipped into a `.zip` file.

### Choose your build file
In the first stage you need to choose the file you want to upload. it can be an **.ipa** (for iOS), **.apk** (for Android) or **.zip** (for MacOS)file.
![choose file](/img/getting-started/upload/upload-app-android-1.png)

### Selecting Your Project Settings

You can define your build settings right in the upload process:

-- **In-app reporting** - Check this box to enable/disable the "shake to report" feature in your app. When enabled, users can simply shake their device to send out a feedback report, along with a video recording, screenshots, logs and metrics of their testing session.

-- **Auto-Update** - When auto update is enabled, users using previous versions of this app will get a notification about the new version next time they open up the app. The new version will be downloaded automatically, so the user doesn't have to actively download it. Please note that in this case no email notification will be sent to the testers.

-- **Custom Comments** - Use this section to add release notes, describe the updated/changes and write about anything else you would like your testers to be aware of.

Please note: these settings are relevant only if you added our SDK to your app.

![ alt testfairy-upload](../../img/app/upload-settings.png)

More build settings available in the [Account_Settings](Account_Settings.html) page.


### <a id="Uploading"></a> Updating an app

If you wish to update a build you already loaded, all you have to do is simply upload the same file again - the same build with the same version.

The new build file will override the old build **without** creating a new app version.

### <a id="Uploading"></a> Uploading a new version

If you wish to upload a new build - which is a new version of the same app, all you have to do is upload the new version in the exact same way you've uploaded the old version. Our service will identify that both apps have the same package name (bundle identifier) and group them together in the same project (app).


**What you should read next:** [Build Settings](https://docs.testfairy.com/Getting_Started/App_Build_Settings.html).

## App Build Settings
<iframe width="800" height="600" frameborder="0" allowfullscreen="true" style="box-sizing: border-box; margin-bottom:5px; max-width: 100%; border: 1px solid rgba(0,0,0,1); background-color: rgba(255,255,255,0); box-shadow: 0px 2px 4px rgba(0,0,0,0.1);" src="https://testfairy.fleeq.io/l/aftiqrzoh4-b55x03f9fv"></iframe>

<!-- ![ alt build-settings-btn](../../img/app/build-settings-btn.png) -->

In order to configure your build settings, click on the **Settings** button of the build menu, right next to the app name and version.

Every build has its own settings, however, some of the definitions are shared by all builds of an app.


<img src="../../img/getting-started/build-settings/build-settings-btn.png" width="800"/>


### App distribution

<img src="../../img/getting-started/build-settings/build-settings-2.png" width="800"/>

* **App Distribution:** Enabled or Disabled. When disabled the app cannot be installed and pending invitations will expire.

* **[Auto-Update](https://docs.testfairy.com/App_Distribution/Auto_Update.html)** - when auto-update is enabled, all the previous installations of this app will be automatically upgraded to this version. The next time a user with an old version opens his app, he will get an 'updating' message and the app will be installed automatically. No email will be sent regarding this update.

* **[Release Notes](https://docs.testfairy.com/App_Distribution/Releas_Notes.html)** These release notes will appear in email invitations, landing pages and in the tester dashboard at my.testfairy.com. Release Notes can be set via upload api, manually on upload or in this page.

* **[Tags]()** Tags can be added to each build. They are comma separated text and can contain spaces.

* **[Metadata]()** Metadata are details received from __Continuous integration (CI)__ systems that upload the build to the TestFairy Dashboard. They can not be edited.

* **[Landing Page](https://docs.testfairy.com/App_Distribution/Landing_Pages.html)** - link to the landing page. Click the  `Configure` button to change the landing page for this build.

### Insights


<img src="../../img/getting-started/build-settings/build-settings-insights.png" width="800"/>

* __Recording:__ Choose whether recording of sessions is `enabled`, `disabled` or `enabled only when WiFi is on`. This is global and overrides all other settings.

* __Session__: this option defines the maximum length of session recorded.

* __Video__ - Changing video settings can be useful if you wish to decrease network overload:
    * Enable / Disable video recording     
* __Metrics__:
   * Application logcat - collect the app logs from the device.


### Bug reporting


<img src="../../img/getting-started/build-settings/build-settings-bugs.png" width="800"/>

* __[In-App Bug Reporting]__(https://docs.testfairy.com/Testers/Submitting_User_Feedback.html)** - When in-app reporting is enabled tester will be able to shake their device in order to open a bug report.

* __[Bug System](https://docs.testfairy.com/Bug_Tracking/Overview.html)__ - indicated which JIRA project is connected to this app. The general configuration of bug tracking systems is doen via the [Bug systems](https://app.testfairy.com/settings/bug-system/) menu item in  __Account preferences__.

### Symbolication

See [here](https://docs.testfairy.com/iOS_SDK/Uploading_dSyms_to_TestFairy.html).

### More

In iOS you will see the details of the build as detected by our service. You can see the certificate type you used to sign the app, as well as more details.

![ios more](../../img/getting-started/app-build-settings-6.png)

In android you will see build details and the hash of the signing certificate at the bottom.

![android more](../../img/getting-started/build-settings/build-settings-more.png)

**What to read next:** [Distributing apps](Distributing_Your_Apps.html)

## Adding and Managing Users
Use the Team area to manage your team members:

![team menu](/img/app/team/team-menu.png)

There are 4 types of users in the system:
1. **Account Owner** - the owner of the account. This user cannot be changed and has full control on the account. The owner  can add Admins, make them Managers and add Testers.
2. **Account Manager** - an admin account that in addition to admin actions can add and delete other admin users(not managers). Managers can not add account manages and can not remove the account owner.
3. **Admin** - a developer that can upload builds, delete builds and view and delete sessions.
4. **Tester** - can download builds of apps. See [here](https://docs.testfairy.com/Getting_Started/How_To_Invite_Testers.html).

You can define an admin as a manager by selecting the account from the list and selecting the `Set as manager` action from the **more actions** menu under the list (you need to be an `owner` or `manager` to perform this action):

![make manager](/img/app/team/make-manager-1.png)


To add more admins to your account add their email address to the **Add new admins** field and specify the access level in the **Permissions** field. You can add more than one at a time by adding several emails to the list, one email in each line.


![ alt add-admins](/img/app/add-admins.png)

- The default access level given to **admin** accounts is `All Projects (rw)` . **rw** mean full access - **read** and **write** to the project specified, or all projects. **r** means **read only** access.

     * **rw** and **r** Permissions are created automatically for each application that is loaded to the system.
     * In addition, there is the `All projects` permission which is for **all applications** that are loaded to the system.

- If you want a different set of permissions for a team member you can select them from the combinations in the permission windows by clicking on the desired set for each project. delete the permission by clicking the `x` on the permission.

## Account Preferences
<iframe width="800" height="600" frameborder="0" allowfullscreen="true" style="box-sizing: border-box; margin-bottom:5px; max-width: 100%; border: 1px solid rgba(0,0,0,1); background-color: rgba(255,255,255,0); box-shadow: 0px 2px 4px rgba(0,0,0,0.1);" src="https://testfairy.fleeq.io/l/0ijyr11qum-2z57bu31bz"></iframe>


Global definitions for your account are done in the Preferences menu.

<img src="../../img/app/preferences-link.png"/>

The first 2 menu items are your SDK and API app tokens.

### SDK token
![ alt app-token](../../img/app/app-token.png)

Your App Token is used to initializing the [TestFairy SDK](https://docs.testfairy.com/SDK/Adding_The_Testfairy_SDK_To_Your_App.html).


### API key
![ alt api-key](../../img/app/api-key.png)

You can use the TestFairy API to directly upload builds and invite testers. For more information please read the [Upload API](https://docs.testfairy.com/API/Upload_API.html) guide.


### Notifications
The notifications options are used to define what type of messages you want to receive about new builds, crashes and user feedback.
![notifications](/img/app/preferences/account-settings-3.png)


### Integrations
You can integrate your TestFairy account with different services in order to customize and streamline your work processes.

* __SMTP and Gmail__: look [here](https://docs.testfairy.com/Integrations/SMTP_and_Gmail.html) how to connect your SMTP email server or your gmail account (including enterprise G suite) so the emails you send from your TestFairy account will be sent from your business email and you will be able to see the sent items in your email account.

* __Slack:__ see [here](https://docs.testfairy.com/Integrations/Slack.html) for how to integrate your slack account with TestFairy.

* __Zendesk:__ see [here](https://docs.testfairy.com/Integrations/Zendesk.html) for how to integrate your account to Zendesk.

* __Webhooks:__ you can also connect various services using our webhooks. Here is an example how to connect [MSFT Teams](https://docs.testfairy.com/Integrations/Microsoft_Teams.html)


![integrations](/img/app/preferences/account-settings-4.png)


### Bug Systems
When you connect your bug system to the TestFairy service it creates a seamless process of reporting bugs straight to your [JIRA](https://docs.testfairy.com/Bug_Tracking/JIRA_Cloud.html), [Bugzilla](https://docs.testfairy.com/Bug_Tracking/Bugzilla.html), [GitHub](https://docs.testfairy.com/Bug_Tracking/Github.html), [Trello](https://docs.testfairy.com/Bug_Tracking/Trello.html) or one of the other systems you can connect.

![bug systems](/img/app/preferences/account-settings-5.png)


### Email templates
TestFairy lets you customize the invitation email it sends. This feature is available only if you use a [custom email](https://docs.testfairy.com/Integrations/SMTP_and_Gmail.html) server.
You can customize the app invitation email sent to invite testers to a specific app and the testers invite email that is used to invite testers to create a testers account in TestFairy.
The email is HTML based and can use custom tags.

![email templates](/img/app/preferences/account-settings-6.png)


### Security
* **Require user login before app download:** if you want your testers to first login to their tester account prior to downloading your app. This will prevent unregistered/unauthorized testers downloading apps.
* **Require [Google] Sign on for all users:** all users will have to sign on using a google email address. This is the case when you use google email integration.
* _Optional_ ``[after adding SAML/Single Sign-on]`` - Grant access to all apps to testers who sign-on with SSO. Testers who sign in using your SSO will have access to all apps.
#### SAML/Single Sign-on
Here you can add the [SSO](https://docs.testfairy.com/Single_Sign-On/SSO.html) metadata definitions file. When you add SAML/Single Sign-on it will contain your _ID_, _URL_ and _x509 certificate_.

![security](/img/app/preferences/account-settings-7.png)

### <a name="account"></a>Account

In the account menu you can change the following settings:

* First and last name of the account owner.
* Your company name.
* Your subdomain - the part that will come before your TestFairy domain URL: **subdomain**.testfairy.com
* Update your account password
* Change your account user name.
* Update your timezone


![account](/img/app/preferences/account-settings-8.png)

### Billing

Here you will see your account invoices.

![billing menu](/img/app/preferences/account-settings-9.png)

### Users whitelist

Allows recording of specific users, instead of recording all user sessions.
This is useful in cases where customer support teams wish to enable recording for a specific user that has a problem.

![whitelist](/img/app/preferences/account-settings-10.png)

What to read next: [Adding_And_Managing_Users](Adding_And_Managing_Users.html)

## Viewing Videos and Data
<iframe width="854" height="480" src="https://www.youtube.com/embed/INsKsWAV8mo?start=141" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>



One of the great advantages of TestFairy is the ease of use for you and your testers.

Once you uploaded your app and invited your testers, they can download the app in one click. If you seletced **Auto Update** in the **"Build Settings"** page, the testers won’t even have to worry about updating it any more, as newer versions will be automatically updated.

Your users do not need to do anything in order to start the video recording. Once they start using the app, video recording and data collection will start automatically. Sending back the application data is as seamless as the installation - your testers just use the application regularly, and TestFairy takes care of the rest. All you need to do as a developer is sit back, relax and watch the data appear on your TestFairy dashboard, showing your testers' behaviour in real time.

## Analyzing your Test Sessions

To analyze your test sessions, choose the app from the **Apps** menu on the top of the page and select a version from the presented chart.

<!-- ![ alt choose-build](../../img/app/choose-build-detail.png) -->
<img src="../../img/app/choose-build-detail.png" width="800"/>

## <a id="testing_overview"></a> Session Overview

Once in **Build Overview**, you can see all your testing sessions presented in a chart with relevant statistics.
To dive into the details of each session, just click on a session row to see the video recording and data collected during the session.


## Session Overview

The **Session Overview** page shows you a full, comprehensive and synchronized view of all the relevant information collected in a single session:

 * **Video recordings**

 * **Application logs**

 * **Metrics**: Below the video recording and logs, you can see performance graphs of CPU, memory, network and other parameters. All the graphs are synced with the video recording, so you can see exactly what happens to the device in every moment of each session.

 * **Screen shots**



If you'd like to find a particular session, or filter sessions according to specific criteria, click on **"Insights"** on the top navbar, next to the app selection menu.


  ![ alt insights-btn](../../img/app/insights-btn.png)




**What you should read next:** [Bug Reporting](Bug_Reporting.html).
