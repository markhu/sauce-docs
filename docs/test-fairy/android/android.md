---
id: android
title: Android
sidebar_label: Android
---
## Integrating Android SDK
<iframe src="https://embed.fleeq.io/l/k84b88ljvv-6tgpx1w80o" frameborder="0" allowfullscreen="true" style="width:800px; height: 600px;"></iframe>


Integrating the TestFairy SDK into your app can help you better understand how your app performs on real devices. It tells you when and how people are using your app, and provides you with any metrics you may need in order to optimize your user experience and code.

Both Java and Kotlin apps are supported.

- Changelog: View [changelog](http://docs.testfairy.com/Android/Changelog.html).
- Class reference: [https://docs.testfairy.com/reference/android/index.html](https://docs.testfairy.com/reference/android/index.html)

## Installation

<!-- Deprecated after Bintray
[ ![Download](https://api.bintray.com/packages/testfairy/testfairy/testfairy/images/download.svg) ](https://bintray.com/testfairy/testfairy/testfairy/_latestVersion)
-->

#### 1. Add the SDK to your app module's build.gradle (eg. `app/build.gradle`)
```
    dependencies {
        implementation 'com.testfairy:testfairy-android-sdk:1.+@aar'
    }
```

#### 2. Add the TestFairy maven repository to your project's build.gradle (eg. `PROJECT_ROOT/build.gradle`)
```
    buildscript {
        repositories {
            maven { url 'https://maven.testfairy.com' }
        }
    }
```

#### 3. Add TestFairy to your main activity's `onCreate`:
<iframe frameBorder="0" width="100%" height="200" src="https://app.testfairy.com/sdk/android/iframe"></iframe>


## Proguard (optional)

If you have *Proguard* enabled, please add this snippet to your proguard rules file (eg `proguard-rules.pro`,   `proguard.cfg` or others):
```
 -keep class com.testfairy.** { *; }
 -dontwarn com.testfairy.**
 -keepattributes Exceptions, Signature, LineNumberTable
 -dontusemixedcaseclassnames
```


## Upgrading

TestFairy is constantly improving and updating the Android SDK. Generally, it's a good idea to always use the latest SDK.

Using version wildcards like “1.+@aar”, will automatically upgrade your TestFairy to the latest version. To refresh dependency, and force Gradle to download the latest version, please run the command: `gradlew --refresh-dependencies`

If you are using a fixed version, for example: `testfairy:testfairy-android-sdk:1.2.4@aar`, you will have to manually update the version.

A list of changes is available in the [Android SDK Changelog](http://docs.testfairy.com/Android/Changelog.html).

## How to Identify users (Optional)

Here is a quick example for an easy way to identify users by email address.
```
TestFairy.setUserId("john@example.com");
```
For more identification options [read this](https://docs.testfairy.com/SDK/Identifying_Your_Users.html)


## <a name="permissions"></a>Additional Permissions (Optional)

TestFairy can record additional insights that require specific permissions. Below is a list of permissions required for each metric:

#### Logs - ```android.permission.READ_LOGS``` (Optional)

In order to automatically upload device logs (logcat) to your account, please add the permission ```android.permission.READ_LOGS```.
Please make sure to check the **"Log collection"** checkbox found under the **"Insights"** tab in ["Build Settings"](https://docs.testfairy.com/Getting_Started/Version_Settings.html). This can be done after the app was uploaded or the first session performed.

#### Tracking Battery Usage - ```android.permission.BATTERY_STATS``` (Optional)

In order to automatically upload the battery status to your account, please add the permission ```android.permission.BATTERY_STATS```.
The general battery status will be tracked, as well as the time when the device was connected or disconnected from a charger.

#### Tracking Phone Signal - ```android.permission.READ_PHONE_STATE``` (Optional)

In order to automatically upload phone signal to your account, please add the permission ```android.permission.READ_PHONE_STATE```.
The phone signal graph shows the GSM Signal Strength, with valid values (0-31, 99). 0 equals -113 dBm or less and 31 equals -51 dBm or more. For more information, please read [GSM standard TS 27.007, section 8.5] (http://www.etsi.org/deliver/etsi_ts/127000_127099/127007/08.05.00_60/ts_127007v080500p.pdf)

#### Tracking Wi-Fi Signal - ```android.permission.ACCESS_WIFI_STATE``` (Optional)

In order to automatically upload the wifi status to your account, please add the permission ```android.permission.ACCESS_WIFI_STATE```.
The wifi signal will be tracked.

## File Size

The size of the TestFairy SDK is 500KB.

<br><br>
You might also like to read [Manual integration with Eclipse and Ant](http://docs.testfairy.com/Android/Manual_integration_with_Eclipse_and_Ant.html).

## Troubleshoot

`Could not GET 'https://jcenter.bintray.com/testfairy/testfairy-android-sdk/1.11.45/testfairy-android-sdk-1.11.45.pom'. Received status code 400`
`Could not GET 'https://jcenter.bintray.com/testfairy/testfairy-android-sdk/1.11.45/testfairy-android-sdk-1.11.45.pom'. Received status code 403`
`Could not GET 'https://jcenter.bintray.com/testfairy/testfairy-android-sdk/1.11.45/testfairy-android-sdk-1.11.45.pom'. Received status code 407`

If you see one of these errors when you include TestFairy SDK in your project, please make sure you followed step 2 in the installation section on this page.
TestFairy is not on Jcenter any more, and you need to switch to maven.testfairy.com. Read more [here](https://docs.testfairy.com/FAQ/Migrate_from_Bintray.html).

## Manual integration with Eclipse and Ant
One of the key strengths of TestFairy's SDK, is the ease of installation. Our *.aar* archive updates the *AndroidManifest.xml* file with the minimum required permissions and activities. However, in some cases, you would more likely want to include the *.jar* archive, rather than the .aar. Such cases are when you are controlling the permissions manually, when using *Ant*, or when working with *Eclipse*.

Please follow these steps to integrate TestFairy's Android SDK in your project:

1. Download the latest *.jar* archive from [bintray](https://dl.bintray.com/testfairy/testfairy/testfairy/testfairy-android-sdk/) and download the *.jar* archive from the latest version.

2. Copy this .jar file into your project, most likely into a directory called `libs`. If you don't have such a directory, please create one in your source root.

3. (Eclipse) You will need to add this *.jar* archive to `Referenced Libraries`. Right-click on the *.jar* archive and select `Build Path > Add to Build Path`.

4. Edit your *AndroidManifest.xml* file and add these permissions:
  ```
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  ```

  Additional permissions are required for specific features in the SDK:
  ```
  // for auto-update feature
  <uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES"/>

  // for sending logs to testfairy
  <uses-permission android:name="android.permission.READ_LOGS" />

  // for tracking wifi signal
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />

  // for battery status
  <uses-permission android:name="android.permission.BATTERY_STATS" />  
  ```

5. Add this activity in your `<application>` section in *AndroidManifest.xml*:
  ```
  <activity android:name="com.testfairy.activities.ProvideFeedbackActivity" android:configChanges="orientation|screenSize" android:theme="@android:style/Theme.Holo.Light" />
  ```

6. Add Testfairy to your main applications's `onCreate`:
   ```
   import com.testfairy.TestFairy;

   public class MyApplication extends Application {

       @Override
       public void onCreate() {
           super.onCreate();
           TestFairy.begin(this, YOUR_APP_TOKEN); // e.g "0000111122223333444455566667777788889999";
       }
   ```

7. (Optional) If you have *Proguard* enabled, please add this snippet to your proguard rules file (eg `proguard-rules.pro`, `proguard.cfg` or others):
   ```
   -keep class com.testfairy.** { *; }
   -dontwarn com.testfairy.**
   -keepattributes Exceptions, Signature, LineNumberTable
   ```
8. (Optional) If you need NDK crashes enabled, please follow steps #2 and #3 with [this library](https://dl.bintray.com/testfairy/testfairy/com/testfairy/ndk/testfairy-android-ndk/) as well.

## Class Reference

[TestFairy Class Reference](https://app.testfairy.com/reference/android/)

## NDK Support
TestFairy SDK can also report crashes initiated from native code such as C/C++. For projects with such requirements, please setup your dependencies like this and you are good to go.

* Add the SDK and NDK support extension to your app module.
```
    dependencies {
        implementation 'com.testfairy:testfairy-android-sdk:1.+@aar'
        implementation 'com.testfairy:testfairy-android-ndk:1.+@aar'
    }
```

* Call `TestFairy.begin()` or `TestFairy.installCrashHandler()` as usual.

## Uploading Crash Symbols

Android projects using native libraries are likely to turn on compiler flags which strip symbol names from the final binaries. In release builds, these configurations result in crash reports with illegible stack trace lines. In order to reveal the symbols in a stripped build's crash report, you must upload a collection of your symbols to TestFairy.

* Install [TestFairy gradle plugin](https://github.com/testfairy/testfairy-gradle-plugin).

* Sync your project.

Make sure you have a correct API key set in the plugin configuration. To find your API key, please refer to your [preferences](https://app.testfairy.com/settings) page.

* Run `./gradlew testfairyNdkDebug` in your project root.

If you have multiple variants for your project, run the command for each variant like this: `./gradlew testfairyNdkRelease`, `./gradlew testfairyNdkMyVariant` etc.

* Optionally, upload your APK with the following command.

`./gradlew testfairyRelease`.

## Uploading with Android Studio
The TestFairy plugin for *Android Studio* and *IntelliJ IDEA* provides a single-click deployment of builds onto the TestFairy platform.

### Installation

1. Open *Android Studio*.

2. Select `File --> Settings` (in Windows) or `Android Studio --> Preferences` (in Mac/Linux) menu.
3. In the shown window, select `Plugins` from the left tab, and then click `Marketplace`
> ![Alt](http://docs.testfairy.com/img/android/android-studio-plugin/open-plugins.png)

4. In the search bar, type `TestFairy` and install the `TestFairy Integration` plugin:
> ![Alt](http://docs.testfairy.com/img/android/android-studio-plugin/install-testfairy-plugin.png)

5. When returned to the previous dialog, click `OK`. You will be asked to restart. All plugins require a restart to complete installation, so click `Restart` at your convenience.

### Usage

With the plugin successfully installed in your development editor, a small icon now appears in your task bar.

![Alt](http://docs.testfairy.com/img/android/android-studio-plugin/testfairy-deploy-icon.png)

When using for the first time, you will be prompted for an API KEY. This is your private key that can be found in your [User Preferences page](https://app.testfairy.com/settings).

### Source & License

Sources for the Android Studio plugin can be found on our [github](https://github.com/testfairy/testfairy-android-studio-plugin).





## Customizing feedback dialog
See the [SDK Documentation](https://docs.testfairy.com/SDK/Customizing_feedback_dialog.html) for more information.

### Feedback Form UI Customization

TestFairy SDK takes a look at a bunch of special fields in `SharedPreferences` to paint the feedback form. You can use the following utility method to override these values.

```java
public static void putString(Activity activity, String key, String value) {
	SharedPreferences prefs = activity.getPreferences(Activity.MODE_PRIVATE);
	SharedPreferences.Editor editor = prefs.edit();
	editor.putString(key, value);
	editor.apply();
}
```

Here is a list of fields you can override in your app.

These keys will be used to override text contents of the form.

- `"com.testfairy.feedback.description"`
- `"com.testfairy.feedback.title"`
- `"com.testfairy.feedback.thankYouText"`
- `"com.testfairy.feedback.verifyErrorText"`
- `"com.testfairy.feedback.sendingProgressText"`
- `"com.testfairy.feedback.poweredByText"`
- `"com.testfairy.feedback.emailPlaceholder"`
- `"com.testfairy.feedback.feedbackDescriptionPlaceholder"`
- `"com.testfairy.feedback.editScreenshot"`
- `"com.testfairy.feedback.takeScreenshot"`
- `"com.testfairy.feedback.removeScreenshot"`
- `"com.testfairy.feedback.takeScreenRecord`"
- `"com.testfairy.feedback.screenRecorded"`

These keys will be used to override content description of icon buttons. We strongly suggest make use of these keys for better accessiblity in your apps.

- `"com.testfairy.feedback.sendButtonContent"`
- `"com.testfairy.feedback.cancelButtonContent"`
- `"com.testfairy.feedback.screenshotThumbnail"`

These keys will be used to override the consent dialog users are shown when a screen recording is going to be captured.

- `"com.testfairy.feedback.consentDialogTitle"`
- `"com.testfairy.feedback.consentDialogMessage"`
- `"com.testfairy.feedback.consentDialogOkButton"`
- `"com.testfairy.feedback.consentDialogCancelButton"`

In Europe, GDPR mandates that you must clearly explain why you are collecting user data and how you are utilizing this data for your business needs. It is strongly suggested that these reasons should be stated in the consent dialog in a clear way. This kind of practice is being adopted by many countries/states and is really important to protect the privacy of your users.

Example:

```java
putString(
    myActivity,
    "com.testfairy.feedback.thankYouText",
    "Thank you for the feedback. We'll take a look at it and notify you shortly."
);
```

### Feedback Prompt Dialog Customization

The SDK recognizes shake gestures and automatically prompts a pop up dialog, asking for confirmation to show the feedback form. It is possible to customize colors in this dialog with the following code.

```java
getSharedPreferences("testfairy.prefs.dialog", MODE_PRIVATE).edit()
    .putInt("textColor", Color.GREEN)
    .putInt("backgroundColor", Color.BLUE)
    .putInt("titleColor", Color.RED)
    .commit();
```

### Class Reference

For more information, please refer to the Android SDK [class reference](https://app.testfairy.com/reference/android/).

## Class Reference
Android SDK class reference has been moved [here](https://docs.testfairy.com/reference/android/index.html).

## Android FAQ
<a name="top"></a>

* [My app crashes while offline, will I get the report?](#crashes-offline)
* [Will crashes be caught even after a session stopped recording?](#crashes-after-stop)
* [What is an APK?](#what-is-apk)
* [What is "instrumentation"?](#what-is-instrumentation)
* [Which architectures are supported?](#android-archs)
* [Where is the keyboard in the captured video?](#android-keyboard)
* [Why isn't TestFairy recording any videos?](#android-no-videos)
* [Am I required to use the TestFairy SDK?](#android-sdk-required)
* [How do I capture touches not caught by TestFairy?](#android-view-touches-as-events)

### <a name="crashes-offline"></a>My app crashes while offline, will I get the report?

Yes.

TestFairy keeps crashes on disk if it can't send them immediately. The next time the app runs, TestFairy will send out the saved crash reports and attach them to the appropriate sessions.

[Back to top](#top)

### <a name="crashes-after-stop"></a>Will crashes be caught even after a session stopped recording?

Yes.

Session max-duration controls how much of the session will be recorded. Many developers won't be interested in video recording beyond the initial 10 minutes. Crashes are caught regardless of the max-duration limit.

In cases where a crash happens beyond the max-duration limit, the report will be attached to the session, along with the part that was recorded.

[Back to top](#top)

### <a name="what-is-apk"></a>What is an APK?

APK stands for Android PacKage. Simply put, it's a .zip file with a different extension, and it contains all the files of an app. The compilation process results with an APK, which can be installed on physical Android devices or emulators.

The .APK file contains many files, which can be viewed using an archiver such as WinZIP, WinRAR or The Unarchiver.

[Back to top](#top)

### <a name="what-is-instrumentation"></a>What is "instrumentation" ?

Instrumentation is a process where code is added to an existing program (or app) in order to monitor, trace, benchmark and debug.

TestFairy uses instrumentation in Android to provide the app developer with a wide range of monitoring capabilities, without the need to write a single line of code.

This procedure is done in real-time during the upload of an APK file. During the process, TestFairy will add instructions to monitor calls to (for example) startActivity, GPS location updates, audio record buffer callbacks and others. Each can be enabled and disabled by the developer when uploading a build, using the checkboxed customizations under **"Advanced Settings"**.

[Back to top](#top)

### <a name="android-archs"></a>Which architectures are supported?

TestFairy supports every architecture the Android platform supports. This includes ARM, x86 and mips.

[Back to top](#top)

### <a name="android-keyboard"></a>Where is the keyboard in the captured video?

TestFairy captures the screen display generated by your app. In Android, the keyboard belongs to another process, and is rendered onto the screen using a system service.

This means that TestFairy (not your app) has access to the pixels or what is being rendered by that process. TestFairy will not be able to record another process's video display.

Therefore, if your app is a keyboard service in itself, you will only see the keyboard, rather than the app that is using it.

[Back to top](#top)

### <a name="android-no-videos"></a>Why isn't TestFairy recording any videos?

When uploading an APK via the web interface, TestFairy can automatically use instrumentation, and add our SDK to your app. This is very useful for Product and QA Managers who don't have access or permissions to the code. With instrumentation, there is no SDK to integrate. However, TestFairy cannot be instrumented in cases of multidex or instant-run. For these cases, you will have to integrate the SDK.

[Back to top](#top)

### <a name="android-sdk-required"></a>Am I required to use the TestFairy SDK?

The TestFairy platform is used for both distribution and for analytics. You can use either both, or just one of them.

[App Distribution](https://docs.testfairy.com/Getting_Started/How_To_Invite_Testers.html) does not require integration of the TestFairy SDK and provides an easy-to-use platform for sending iOS IPA files to testers and colleagues in your enterprise. Simply upload an Ad Hoc or Enterprise signed IPA files and send an e-mail invitation or App Landing Page to the selected testers.

Using analytics requires integration of the SDK. This is a 2-minute task that involves adding just a single line of code to your project. With analytics enabled, you will able to see a video recording of your app being used, as well as receive logs from the device, analyse usage with checkpoints or loading view controllers and much much more. For more information, please follow the [integration manual](https://docs.testfairy.com/Android/Integrating_Android_SDK.html).

[Back to top](#top)

### <a name="android-view-touches-as-events"></a>How do I capture touches not caught by TestFairy?

TestFairy attempts to catch user touches in your app, however, these are limited to buttons and list views. If there's a View who's touches you'd like to capture, you can make use of the `TestFairy.addEvent` to see touches appear as events in your timeline.

As an example, in the code below, a `View.OnClickListener` is attached to an `ImageView`. Using the `onClick` callback, an event was sent to TestFairy with a custom message, and, in this case, the content description of the Image.

```java
findViewById(R.id.imageView2).setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        String description = view.getContentDescription().toString();
        TestFairy.addEvent("ImageView clicked: " + description);
    }
});
```

[Back to top](#top)

### <a name="android-class-not-in-apk"></a>Why my application cannot find some TestFairy classes in runtime?

Some compile-time dependencies may preprocess existing binaries in your project to perform tasks such as performance profiling, multidexing and dependency injection. When used alongside Proguard or R8, this may cause incorrect removal of TestFairy classes during a build. If such issue occurs, your app will crash with a `ClassNotFoundException` or a similar exception. In order to circumvent that, make sure you append the rules below to your existing proguard rule set and add necessary exclusion statements to your gradle plugin configurations if necessary.

```
 -keep class com.testfairy.** { *; }
 -dontwarn com.testfairy.**
 -keepattributes Exceptions, Signature, LineNumberTable
 -dontusemixedcaseclassnames
```

[Back to top](#top)
