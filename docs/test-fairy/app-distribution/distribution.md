---
id: distribution
title: App Distribution
sidebar_label: App Distribution
---
## Distributing Your Apps
<iframe width="800" height="600" frameborder="0" allowfullscreen="true" style="box-sizing: border-box; margin-bottom:5px; max-width: 100%; border: 1px solid rgba(0,0,0,1); background-color: rgba(255,255,255,0); box-shadow: 0px 2px 4px rgba(0,0,0,0.1);" src="https://testfairy.fleeq.io/l/9162234x94-qc3qn71j97"></iframe>

The distribution process starts with [loading your apps](https://docs.testfairy.com/Getting_Started/Upload_Apps.html) to Testfairy.
* If you have an Android app simply go to your dashboard and follow the instructions in the [Upload](https://docs.testfairy.com/Getting_Started/Upload_Apps.html) section.
* If you are distributing an iOS app with an
  * __[Enterprise certificate](https://developer.apple.com/programs/ios/enterprise/)__ the process is identical to the Android distribution.
  * __Ad-hoc__ certificate iOS apps require some preparation, described [here](https://docs.testfairy.com/iOS_SDK/Adding_UDIDs_to_iOS_development_profile.html).
* If you're distributing Apps for MacOS, you **must zip** your App (a MacOS app will have an `.app` extension, after zipping, it should have a `.zip` extension). Then you can follow the normal upload process described [here](https://docs.testfairy.com/Getting_Started/Upload_Apps.html).

After you have an app loaded you can start distributing it to your testers.

Distributing your app is a simple process:

  ![upload process](/img/upload-process-1.png)

- You will only need to decide if you want testers to login (verify) their account prior to download or just let anybody with the link download your app.


The distribution process described above can be done with a pre-registered list of testers or with invitations to testers that are sent for a specific build.


### Email invitations
Inviting your testers via email is done in two ways:
#### Pre invitation
Pre-inviting them by adding them to your testers list in the [TESTERS](https://app.testfairy.com/testers/) tab of the dashboard in advance, and then inviting them to the build in the invite testers menu of a specific build.


  ![inviting testers to a build](/img/getting-started/invite-testers-from-build-1.png)


  The pre invitation is used when iOS apps are distributed to specific devices when you don't use an enterprise certificate.   It is also commonly used when you have an in house testing team.


#### Adding to a specific build
Adding their email to a specific build at the empty email box at the bottom of the testers list.

  ![add tester email](/img/getting-started/invite-testers-from-build-2.png).

This will send them an email with a download link and can be done with Android and iOS apps that are signed with an [enterprise certificate](https://developer.apple.com/programs/ios/enterprise/). It is also commonly used when you have an in house testing team and want to add them to several builds and different apps.


### Landing pages

You can also build a community of testers or distribute you app by using our pre-designed [landing page](https://docs.testfairy.com/App_Distribution/Landing_Pages.html). The landing pages link can be sent to testers for downloading you apps. The download link in the landing page can also be secured by login (opt-in) requiring the testers to log in before downloading your app.


### Testers dashboard

The [tester dashboard](https://my.testfairy.com/) is the place where tester see all the apps they were invited to test.
This view is available to all testers in the system. Developer can switch from this view to the full dashboard view with the `view as developer` menu item.

### Permissions

Permissions (Group Permissions) are used in order to manage app distribution to groups of testers/users.

The permissions are defined for each app (and all its builds) so all testers that are part of the group can download all the apps builds.

The permissions are based on defining groups of testers as described in [Managing tester groups](https://docs.testfairy.com/Testers/Managing_Testers.html).

Once you have defined the groups of some or all of the testers the groups appear in the permissions screen.

  ![permissions](/img/app_distribution/permissions-screen-1.png)

Ticking the checkbox of a group makes the app (and all its builds) available for that group (and hence all its testers).
The app is then displayed in the [testers dashboard](https://docs.testfairy.com/TestFairy_Dashboard/Testers_Dashboard.html) and can be downloaded by the testers. Unchecking a group checkbox will remove the app from the testers dashboard that are part of that group.

### Production

Please note that Auto Update must be disabled for apps that are running in production.


## Auto Update
## How does auto-update work?
TestFairy Auto-Update allows developers to push new app versions automatically, in order to make sure that all users are on the latest version of their app. When a new version is set to auto-update, all users with older versions will see a notification next time they use the app, suggesting to update.

Auto-update cannot be used in production. [See here](https://docs.testfairy.com/Android/Production_SDK.html) to learn how to opt out.

### How to configure auto-update in the dashboard?
In order for the auto-update to work, Your app must include the [TestFairy SDK](https://docs.testfairy.com/SDK/Adding_The_Testfairy_SDK_To_Your_App.html) in your application.

There are 3 ways of configure auto-update for a specific build:

#### Option 1. On Upload

When uploading a new app or version, check the auto-update checkbox.

![TestFairy build settings ](/img/auto-update-img2.png)

#### Option 2. In Build Settings

After build is uploaded, open [build settings](https://docs.testfairy.com/Getting_Started/App_Build_Settings.html), and under **App Distribution**, check the Auto-Update checkbox.

![TestFairy build settings ](/img/auto-update-img1.png)

#### Option 3. Configure auto-update via upload API

When uploading a new build via our [upload api](https://docs.testfairy.com/API/Upload_API.html) set the `auto-update` parameter to `on` .

### How to Verify which app is set to auto-update ?

Open your app and look at the list of builds. The right column has an icon of a rownded arrow indicating this is the auto-update version.

![](/img/auto-update-dashboard-place.png)


### What will be the user experience on auto-update ?

- Auto-Update will upgrade all the previous installations of an app to the selected version.
- When your app starts, the SDK will check if a new version is available and is marked for auto update.
- If so, the user will see a message telling him that a new version is ready and asking him to update:
![auto update message](/img/app_distribution/auto-update-msg.png)


- If the user agrees, the new version will download and install on his device.
- If the user declines the old version of the app will load. The message will again display when the app is loaded again.

### Reasons that auto update may fail

Here are some reasons when auto-update of an app may fail:
* The version number and name of the new build are **the same** as the old one. Auto-update will only work when versions are **different**.
* The TestFairy SDK must be integrated into Both versions for auto-update to work.
* (in Android) The sign certificate of each version must be the same. If an app is not signed with the same certificate TestFairy cant perform the auto-update action.
* (In iOS) - you will have to sign your app with an __AD-HOC__ or __ENTERPRISE__ certificate for the auto-update feature to work.


### A method to force auto update

Occasionally you will want all testers of an app to only test the latest version released. In this case you can use the following method to make sure users and testers **can not** run older versions of the app and must upgrade to the version marked as auto-update.

The classes used are named [`sessionStateListener`](https://docs.testfairy.com/reference/android/com/testfairy/SessionStateListener.html#SessionStateListener--) → `onAutoUpdateDismissed` in **Android** and [`testFairySessionStateDelagate`](https://app.testfairy.com/reference/ios/Protocols/TestFairySessionStateDelegate.html) → `autoUpdateDismissed` in **iOS**.
These methods get the result of the pop up message displayed to the user asking to update. You can then write code to perform the action of your choice.


### How to downgrade you app?

Auto-update works only in cases where version **is unique** and the new version was uploaded to TestFairy **after** the old version. The version number or code of the app is not important, only the __upload date__.

Therefore, in order to downgrade an app you will need to do the following work around process:
   (Assuming you want to downgrade from version 1.5 to 1.4)

   * **Re-upload** version 1.4 to TestFairy using a new version name (1.41 for instance).
   * Mark it as an **auto-update** version.

This will cause the system to perform an auto-update of version 1.5 to version 1.41 thus in effect **downgrading** your app to version 1.4.


----------

## Landing Pages
TestFairy Landing pages allow you to easily distribute apps to testers.
Every TestFairy app has a landing page that is created automatically.
Landing page can be disabled at the top of the landing page settings page.

![disable landing page](/img/landing-pages-on-off.png)


![landing page settings](/img/app_distribution/landing_pages/landing-page-fields.png)


* **Landing page URL:** The URL that is automatically generated for each landing page. The last token of the url is configurable.

* **App version:** Indicates which version of the app will be shown. You can choose to always show the latest version, always show the auto-update version, or freeze on a specific version.

* **Visability:**  
  * _Open Beta (Anyone can download)_ - Landing page is visible to anybody.
  * _Closed Beta (Testers required to login)_ - Users must log in in order to see the page.

* **App description:** A description you add to the landing page for testers instructions or other information. Can be formatted in <a href=https://guides.github.com/features/mastering-markdown/ target=_blank >Markdown</a>.

* **Add release notes:** Check in order to automatically include [release notes](/App_Distribution/Release_Notes.html) in landing page

* **Add custom CSS:**  Check in order to add custom CSS, for [landing page customization](https://docs.testfairy.com/FAQ/Landing_Page_Customization.html)


Once you make changes to the settings you need to save them so they take effect. You can preview the changes using the `Preview landing page` button.

#### Recruitment Pages

Recruitment pages allow you to easily let users request to join your testing project.

When users signup, they will show up in your account in "Pending Apprvoal" status and you will get an email allowing you to approve or reject these users. Once approved they will get an email inviting them to download the app.

* In order for recruitment pages to work, visibility must be in "open beta" mode.

* Users who sign up and approved will atuamatically be added to a testers group called "recruit".

* in case your app is an iOS app signed with an ad-hoc certificate, users will first get an email asking them to register their device and only after they register, you will get an email with their UDID.

* It is possible to automatically approve all users who signup, please contact us to enable this option for your account.



## Landing Page Customization
## How to customize your apps landing page?
Landing pages created for app distribution can be customized to have the look and feel of your company or brand.

The basic landing page that is automatically generated looks like this:


![landing page](/img/landing-page-customization-areas.png)


The following elements can be changed via the Add custom CSS option in the landing page settings:


 * **Page title** - class `.testfairy-app-name`

 * **Release notes** - class `.testfairy-description`

 * **Feedback Instructions** - class `.community-sub-title.dev`

 * **Background** - class `.testfairy-background`


Here is an example for a CSS code you can use in order to customize your landing page:

```

.testfairy-background {background-image: url("https://www.testfairy.com/images/castle-cloud.jpg") !important;}
.testfairy-app-name {color: green;}
.testfairy-description {color: red;}
.community-sub-title.dev {color: blue;}

```


![css editing](/img/landing-page-customization-css-place.png)

## Manage Apps Distribution
### Disable the landing page

If you do not want a landing page you can disable it on the landing page settings page for that specific app:

![dissable landing page](/img/landing-pages-on-off.png)

Disabling the page will not stop the distribution of the app since it still appears in the **testers dashboard** and is still alive in the system.


If you want to **`stop`** distribution of your app you will need to do one of 2 actions:

### Disable distribution

In the build **Settings** go to **App Distribution**  and change it to `Disabled` and press save changes.

![](/img/app_distribution/dissable-dist-build.png)

You will see a message confirming the new settings have been changed:

![](/img/app_distribution/app-dist-save-sucsess.png)

And If you go to the build overview you will see another message that the build is expired and testers will not be able to install this build:

![](/img/app_distribution/build-invalid.png)

_______
**PLEASE NOTE:** Once the build is disabled the app **will not appear** in the testers dashboard but Testers who already installed the app will be able to continue using it.
_______

### Deleting the build from the dashboard

If you want to delete a build from the system go to the builds **App Overview** menu:

![](/img/app_distribution/select-builds.png)

On the left column select the checkbox of the build you want to delete. You can choose one, many or all the builds.

Once you select the build, in the bottom actions drop down choose Delete (n) builds:

![](/img/app_distribution/delet-builds.png)

Confirm the deletion:

![](/img/app_distribution/confirm-delete.png)

A message confirming the duild was deleted will be displayed.

## App Versioning
## App naming and versioning

When loading an app to Testfairy the service decodes the app name, version number and version name of the build and displays it in the dashboard.


### Displayed name in the dashboard

The app name used in the dashboard is the **Display Name** in your iOS xcode project or the Value of the `string name=”app_name”` in the **strings.xml** file in the `res/values` directory of your Android app in Android studio.

**In Android Studio:**
![](/img/app_distribution/android-studio-app-name.png)


**In Xcode:**
![](/img/app_distribution/xcode-ios-app-display-name.png)


### Android


These are the two fields identifying a build:

- **versionCode** - A positive integer used as an internal version number.
- **versionName** — A string used as the version number shown to users.


These fields will be translated and displayed in the following fields on the TestFairy Dashboard:

- Version = **versionName**
- Version code = **versionCode** - displayed in (brackets) after the version field.

![](/img/app_distribution/android-version-numbering.png)


### iOS:


These are 2 fields for identifying the app:

- **Bundle version** - a string composed of one to three period-separated integers. Can only contain numeric characters (0-9) and periods.
- **Bundle versions string, short** - a string.


These fields will be translated and displayed in the following fields on the TestFairy Dashboard:

- Version = **Bundle versions string, short**
- Version code = **Bundle version** - displayed in (brackets) after the version field.

![](/img/app_distribution/ios-version-numbering.png)

Read more about app versioning for <a href="https://developer.android.com/studio/publish/versioning#appversioning" target="_blank">Android</a>, or <a href="https://developer.apple.com/library/archive/technotes/tn2420/_index.html" target="_blank">iOS</a>.

## Separating your apps and builds in the TestFairy dashboard

In case you upload an app with the same version and package name (or Bundle Identifier), and this app already exists in your account, the new app will override the old app.

If you want to keep the old app you can do one of the following:

1. Change the app version. Either increment the app version name or number, or add a numeric/textual suffix.

2. Change the app package name (or Bundle Identifier)

Please note that since TestFairy apps are grouped by package name, uploading an app with a new package name will create a new TestFairy project, so that apps with package name com.company.app will be grouped seperately than apps with package name com.company.app.debug


## Release Notes
There are several ways to update a builds release notes:

### 1. Upload

When [uploading a new app or version](https://docs.testfairy.com/Getting_Started/Upload_Apps.html) from the dashboard, after the app is uploaded, enter the release notes in the last dialog.

![TestFairy Release Notes](/img/upload-release-notes.png)

### 2. Change Build Settings

After an app or new buils is uploaded, open the build settings, and under **App Distribution** change the release notes:

![TestFairy Release Notes](/img/settings-release-notes.png)

### 3. Upload API

The recommended way to upload apps is to use the [upload API](https://docs.testfairy.com/API/Upload_API.html).

In order to add release notes, use the comment field.
Here is an example:

```
curl https://upload.testfairy.com/api/upload \
	-F api_key='your_api_key' \
	-F file=@sample.apk \
	-F symbols_file=@sample_mapping.txt \
	-F testers_groups='friends,beta' \
	-F notify='on'\
  -F comment='Put Release Notes Here'
```

### 4. Jenkins

By default, The [TestFairy Jenkins plugin](https://wiki.jenkins.io/display/JENKINS/TestFairy+Plugin) will use the comments that were included in every commit, in a pretty standard way.
In order to add your own release notes, create a text file in the following location:

```
$JENKINS_HOME/jobs/$JOB_NAME/builds/$BUILD_ID/testfairy_change_log
```

The content of this file will override the default changelog.

Read more about the [TestFairy Jenkins plugin](https://wiki.jenkins.io/display/JENKINS/TestFairy+Plugin)

### How to stylize the release notes

TestFairy builds can include the use of <a href="https://guides.github.com/features/mastering-markdown/" target="_blank">Markdown</a> in the release notes and app description that will appear in [email invitations](), [landing pages](https://docs.testfairy.com/App_Distribution/Landing_Pages.html) and in the [testers dashboard]() tooltips.



## Tags
Tags are text labels that can be attached to builds and used for identification and search. Every build (app version) can have different tags.

#### How to add tags to builds that are uploaded via API

- Tags can be added programmatically when uploading the build via the [TestFairy Upload API](https://docs.testfairy.com/API/Upload_API.html) using the `tags` parameter.


#### How to add/edit tags to existing builds

- Once the build is already available in your dashboard, Tags can be added, edited or deleted in [build settings](https://docs.testfairy.com/TestFairy_Dashboard/Builds.html) menu under __App Distribution__ --> __Tags__.

#### Displaying tags to admins

Tags appear in a project page:

![](/img/dashboard/builds-table.png)  

In the dashboard, Tags are searchable in the `Search...` textbox available at the top right.

#### Displaying tags to testers

Testers can see Tags in their Testers Dahsboard available at [my.testfairy.com](my.testfairy.com):

![](/img/app_distribution/builds-my-view.png)  

Tags are also available at the top of every landing page, just below the main headline:

![](/img/app_distribution/landing-page-tags.png)  
