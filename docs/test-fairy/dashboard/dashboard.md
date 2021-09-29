---
id: dashboard
title: Dashboard
sidebar_label: Dashboard
---
## Dashboard Overview
<iframe width="800" height="600" frameborder="0" allowfullscreen="true" style="box-sizing: border-box; margin-bottom:5px; max-width: 100%; border: 1px solid rgba(0,0,0,1); background-color: rgba(255,255,255,0); box-shadow: 0px 2px 4px rgba(0,0,0,0.1);" src="https://testfairy.fleeq.io/l/1tvmj34u5q-r1ck6l9wd6"></iframe>


## TestFairy dashboard

The TestFairy dashboard is where you see all the information about the apps you have loaded to the service.


It includes a list of all apps with their own app definitions, the latest sessions recorded in your account, and separate tabs for crashes, feedbacks and [insights](https://docs.testfairy.com/TestFairy_Dashboard/Insights.html).


You can also [load apps](https://docs.testfairy.com/Getting_Started/Upload_Apps.html) using the `NEW UPLOAD` button and manage your [account preferences](https://docs.testfairy.com/Getting_Started/Account_Preferences.html) and [team members](https://docs.testfairy.com/Getting_Started/Adding_And_Managing_Users.html).

### `DASHBOARD` tab

![](/img/dashboard/dashboard-general.png)

The top bar has the general statistics of your account - number of sessions, crashes, apps, testers and users.


#### Apps table
Contains the list of all the apps loaded into the system.
The app in display is the last version loaded.

It details the app name and bundle ID, whether it is an iOS, Android or MacOS app, the latest version name & number, and some details about how many sessions, builds, crashes and issues were logged for the app.
You can also see the date the last build was loaded to the system and the date the latest session was logged.
Pressing on the app's row will lead you to the [Builds table](https://docs.testfairy.com/TestFairy_Dashboard/Builds.html).

The last column holds a link to the app's landing page if the app was loaded into the system.

#### Recent Sessions
A list of the recent sessions logged in the system.


### `TESTERS` tab

![](/img/dashboard/dashboard-testers.png)

Contains the list of your testers and assigned apps. See the [managing testers](https://docs.testfairy.com/Testers/Managing_Testers.html) page for more details.

### `CRASHES` tab

![](/img/dashboard/dashboard-crashes.png)

Contains a list of all crashes aggregated by stack trace. You can filter the list by app, version and timeframe.
Each crash is aggregated after symbolication (if possible) and appears in a separate line. It is possible that unsymbolicated crashes will appear in separate lines, one for each crash.

### `USER FEEDBACK` tab

![](/img/dashboard/dashboard-feedbacks.png)

Contains all user feedback submitted using the [shake to report](https://docs.testfairy.com/SDK/Getting_Feedback.html) functionality. The feedback is linked to the session in which it was created and contains the screenshot, the text the user entered and the reporter email (which can be different from the user identified in the session).
Each issue can be linked to a bug tracking system by pressing the CREATE BUG button in the ISSUE column. Apps that are already connected to a bug tracking system will display the issue link/number inside the button. Pressing the button will open the issue in the bug tracking system.


## Builds
<iframe src="https://embed.fleeq.io/l/0v2ir0nl2c-r169sigcks" frameborder="0" allowfullscreen="true" style="width:800px; height: 600px;"></iframe>


## Builds

The **Builds** page contains a list if all the builds for this app.

For each build you can see the following details:

![Builds Table](/img/dashboard/builds-table.png)


- **VERSION** - the build's name and version - see App versioning for more details.

- **SESSIONS** - the number of sessions logged for this build - number is linked to the Insights tab

- **CRASHES** - number of logged crashes for this build's version - linked to the CRASHES Tab.

- **DOWNLOADS** - number of downloads for this build.

- **FEEDBACKS** - number of feedbacks for this build - linked to the FEEDBACKS Tab.

- **UPLOADED** - when this was build loaded to the system.

- **TAGS** - short words describing the build - can be edited in the build settings menu and are searchable in the `Search` field at the top of the table. See below for more info.

- **BUILD STATUS** - Contains indicators for the build status:
  - Build is not loaded into the system - ![](/img/dashboard/status-icon-app-not-uploaded.png)  
  - Video is disabled - ![](/img/dashboard/status-icon-no-video.png)
  - Build is defined as Auto-update - ![](/img/dashboard/status-icon-auto-update.png)
  - Build has metadata - ![](/img/dashboard/status-icon-metadata.png)
  - Build has release notes - ![](/img/dashboard/status-icon-comment.png)
  - Build distribution is disabled - ![](/img/dashboard/ic_close_black_36.png)
  - Build was signed with a different certificate than the previous build - ![](/img/dashboard/ic_error_red_48dp.png)
  - Build dose not contain the TestFairy SDK - ![](/img/dashboard/status-icon-no-sdk.png)

- Settings button ![](/img/dashboard/ic_settings_black.png) - Pressing it opens the build settings menu.

Builds that are stared ( ![](/img/dashboard/star-yellow.png) ) are listed at the top of the table regardless of the upload order.

### Tags

Tags are labels attached to builds for identification and give additional searchable information about them.

The text may contain spaces and more than one word.

One can add tags to a build by adding them on upload using the [Upload API](https://docs.testfairy.com/API/Upload_API.html) or edit them in the [Build Settings](https://docs.testfairy.com/Getting_Started/App_Build_Settings.html) menu.
They can be searched with the `Search` box at the top of the Builds page.


### Metadata

Metadata is information specificly related to this build.

It is defined once when the build is added to testfairy via [Upload API](https://docs.testfairy.com/API/Upload_API.html) and can not be changed after the build is loaded.

The format of defining it is **metadata.key=value** For example, `metadata.branch=master`.
Only the **value** can be searched with the `Search` box at the top of the Builds table.


### Deleting builds and apps

In case you want to delete a build from the system select the checkbox next to it and at the bottom dropdown menu (**More Actions…**) choose `Delete Build`.

To delete the whole app you need to select all its builds in the top checkbox and then in the **More Actions…** choose `Delete Build`.

## Insights
<!---<iframe width="854" height="480" src="https://www.youtube.com/embed/i8crsqfJAFA" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>)--->

<iframe width="800" height="600" frameborder="0" allowfullscreen="true" style="box-sizing: border-box; margin-bottom:5px; max-width: 100%; border: 1px solid rgba(0,0,0,1); background-color: rgba(255,255,255,0); box-shadow: 0px 2px 4px rgba(0,0,0,0.1);" src="https://testfairy.fleeq.io/l/4vaf26t35u-pd0iztdypt"></iframe>


The **INSIGHTS** tab has information on all the crashes and sessions that were recorded in your apps.
When you first navigate to it you will see a list of the latest crashes in the system.

### Preset filters
The **Preset Segments** column on the left contains three preset filters:

  - ![](https://app.testfairy.com/images/app/header/ic_report_black_24dp_1x.png) Crashes - list of all crashes in the last month
  - ![](https://8640586.testfairy.com/images/app/header/status-icon-anr.png) Slow Session - all slow sessions in the last month
  - ![](https://8640586.testfairy.com/images/app/header/status-icon-comment.png) Received Feedback - all sessions with a feedback in the last month

### General Filters
For filtering the items in the list use the filters located at the top:

![filters](/img/getting-started/insights/insights-filter-1.png)

You can see all apps in your account or filter only one of them:

![](/img/getting-started/insights/insights-filter-app-name.png)

You can see all versions of the app you just filtered or a specific version.

![](/img/getting-started/insights/insights-filter-app-version.png)

You can also filter the timeframe of the list you want.

![](/img/getting-started/insights/insights-time-frame.png)

The list below will be filtered according to what you selected.

### Attribute filters
In addition to the general filters you can add filters of **session attributes**. In order to do this first select an attribute from the list of available attributes:

![](/img/getting-started/insights/attribute-filter.png)

  - The basic attributes types (User, Session, Location, Device) are default for any session in testfairy.

### Custom attributes filters
If you add [custom attributes](https://docs.testfairy.com/SDK/Session_Attributes.html) to your apps session you will see them here and be able to filter according to their values:

![](/img/getting-started/insights/custome-attributes.png)

  - This is an **extremely powerful** tool that can help you identify specific sessions and filter them in the multitude of sessions in your app, especially if you are running testfairy in a large scale internal app or in production.


--------------------------

**Please note** - when you define values for this field, do not use characters other than text or numbers (a-z A-Z 0-9) like `/` `"` `-` as they can not be searched on in this field. Alternatively, if you **do** have these characters you can search only for separate parts of the text without them. (for example: {attr1="dada-1270"} the `-` is not searchable so you can search for `dada` **or** `1270`.

----------------------------


After you select an attribute you add a logical expression and type a value in the text field:

![](/img/getting-started/insights/atribute-filter-logical.png)

The result is shown in the table.

You can add another line of attribute filter with the `+` sign or save this filter by pressing the `Save Segment` button. After giving it a name it will appear in the list of **Custom Segments** in the left column.

![](/img/getting-started/insights/filter-name.png)

## Testers Dashboard
The [Testers Dashboard](https://my.testfairy.com/) is the place where testers see all the apps they were invited to test.
This view is available to all testers in the system.

Developers can switch from this view to the full dashboard view with the `view as developer` menu item.

### (This is the Android view)

![](/img/dashboard/testers-dashboard-android.png) ![](/img/dashboard/testers-dashboard-android-menu.png)

### (This is the iOS view)

![](/img/dashboard/tester-dashboard-ios.png) ![](/img/dashboard/testers-dashboard-ios-menu.png)

### Menu
In the app view you can see all the apps designated to the tester.


Each app has all its details including:
- App name
- App <a href=https://developer.android.com/studio/build/application-id target=_blank> **applicationId**</a>
- App <a href=https://developer.android.com/studio/publish/versioning target=_blank> **versionName**</a>
- Update date - when it was last uploaded to the system


The green button is for downloading the app to your device.

If you press the `+` sign you will see the app's **release notes** and a link to view all **previous versions** of the app that are also available for download.

In the menu there is an option to see **My Apps** in the account, see **My Devices** (you will see only registered iOS devices) and **Log Out** of the account.

### Troubleshooting

<iframe width="800" height="600" frameborder="0" allowfullscreen="true" style="box-sizing: border-box; margin-bottom:5px; max-width: 100%; border: 1px solid rgba(0,0,0,1); background-color: rgba(255,255,255,0); box-shadow: 0px 2px 4px rgba(0,0,0,0.1);" src="https://testfairy.fleeq.io/l/8kblwik5sc-d1udj9q6hh"></iframe>

If an iOS application does not install on your device, we recommend that you run the `troubleshooting` tool:

1. Open your TestFairy account via the link [my.testfairy.com](https://my.testfairy.com) on the device you want to test.


2. Click the Tester icon ![](/img/tester/tester-icon-1.png) menu and choose **Troubleshooting**.


3. Click the `START` button to start the troubleshooting process.


4. Click **allow** to let the configuration profile download.


5. Close and go to the **settings app**. Click on the **profile downloaded** menu.


6. Install the configuration profile previously downloaded.


7. After the installation is complete, you will be directed to review the troubleshooting results.
