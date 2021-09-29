---
id: faq
title: FAQ
sidebar_label: FAQ
---
## Why Do I See User-1
When seeing "User-1gf8d8ga" as the session User ID, it means that the user for this session was not identified.

In such cases, we generate a random username, in order to help you aggregate sessions by user.

In order to identify sessions and know which user used your app, please call the method `setUserId`.

[See examples for using setUserId](https://docs.testfairy.com/SDK/Identifying_Your_Users.html)

__Before__ calling `setUserId` it looks like this:

![Before using setUserId](/img/faq-user-1-before.png)

In order to identify your sessions, simply call `setUserId`

__After__ calling `setUserId` it looks like that:

![After user setUserId](/img/faq-user-1-after.png)

For more information please read the SDK docs here: [Identifying Your Users](https://docs.testfairy.com/SDK/Identifying_Your_Users.html)


## How to Build the Testers App
TestFairy provides customers who run the service on a [private cloud](https://docs.testfairy.com/SDK/Private_Cloud_Integration.html) to build their own TestFairy Testers App.

This way, you can cusomtize and brand it as you wish.

In order to get do that please do the following:

# Android

### Source Code
Fork this project: [https://github.com/testfairy/testers-app-android](https://github.com/testfairy/testers-app-android)

### Code Changes
Change [Base_URL](https://github.com/testfairy/testers-app-android/blob/master/TestFairyApp/src/main/java/com/testfairy/app/MainActivity.java#L49)

```
private static final String BASE_URL = "https://<YOUR_SUBDOMAIN_HERE>.testfairy.com";
```

# iOS

### Source Code

Fork this project: [https://github.com/testfairy/testers-app-ios](https://github.com/testfairy/testers-app-ios)

### Code Changes

Change [config.xml](https://github.com/testfairy/testers-app-ios/blob/master/src/config.xml#L10)

```
<content src="https://<YOUR_SUBDOMAIN_HERE>.testfairy.com" />
```




## How to disable TestFairy in production
TestFairy is a platform with many use-cases. Some enterprises use the platform during their development, some use it to record user experiences to improve their product, others run it in production to assist in customer support.

The SDK is very modular and is built to handle the your needs and your company's needs.

This document talks about how to exclude the TestFairy SDK from production builds. It was designed for enterprises who use TestFairy throughout development and QA cycles, but would like to remove TestFairy SDK when building production releases.

## iOS

### Option 1: Calling [TestFairy begin] only in DEBUG

Without a call to [TestFairy begin], the SDK is not initialized. An uninitialized SDK won't consume any memory, won't open sockets, and won't catch uncaught exceptions. Even though it does not impact your app in any way, the SDK is still linked with your app. This is the easiest option.

##### Objective-C
```
#ifdef DEBUG
[TestFairy begin:@"APP_TOKEN"];
#endif
```

##### Swift
```
#if DEBUG
TestFairy.begin("APP_TOKEN")
#endif
```

If your publishing workflow has multiple build schemes or you plan to implement such phases, please proceed to [this post](https://blog.testfairy.com/ios-build-schemes-explained/) to learn how to do that.

We suggest defining a compiler flag for each scheme you have to enable the SDK for schemes relevant to testing like below.

##### Objective-C
```
#if defined(DEBUG)
[TestFairy begin:@"APP_TOKEN"];
#elif defined(SCHEME1)
[TestFairy begin:@"APP_TOKEN"];
#elif defined(SCHEME2)
[TestFairy begin:@"APP_TOKEN"];
#else
// Don't initialize the SDK
#endif
```

##### Swift
```
#if DEBUG
TestFairy.begin("APP_TOKEN")
#elseif SCHEME1
TestFairy.begin("APP_TOKEN")
#elseif SCHEME2
TestFairy.begin("APP_TOKEN")
#else
// Don't initialize the SDK
#endif
```

If you are also worried about reducing the app size in your final release build, proceed to Option 2.

### Option 2: Configure link options in a scheme for App Store

A common pattern we see from our customers is having a dedicated scheme for App Store. Meaning there's a Debug, Release and App Store (and maybe others.)

The link phases that are explained in the integration document only apply to Debug and Release schemes, and can be excluded from the App Store scheme.

This solution still requires use of `#ifdef` or `#if` as before, but can also completely omit the library from being linked with the app.

Navigate to project build settings and locate **Excluded Source File Name** option. Expand the list and find the build scheme you want to exclude TestFairy from. Double click the row add two entries to the excluded file list, one for **TestFairy.h**, one for **libTestFairy.a** files.

Try building your project. If the compilation fails, locate the lines where TestFairy is used and wrap them with `#ifdef` or `#if` directives explained in Option 1.

<a name="ios-noop"></a>
### Option 3: No-op SDK

Similar to Option #2, you're required to have multiple schemes in your project, but **does not** require the use of `#ifdef` or `#if`.

1. Download the [TestFairy iOS No-Op SDK](https://github.com/testfairy/testfairy-ios-sdk-noop)
2. Add `TestFairy.m` to your project's *Production* or *App Store* scheme. (Note, that the `.m` file needs to be put in a place where it can find the `TestFairy.h` file).
3. Navigate to project build settings and locate **Excluded Source File Name** option. Expand the list and find the build scheme you want to exclude TestFairy from. Double click the row add an entry to the excluded file list for the **libTestFairy.a** file.

This will allow you to keep all your calls to `TestFairy` as-is, but replaced with empty implementations.

## Android

### Option 1: Calling TestFairy.begin() only in Debug mode.

Your Gradle variants can alter the code path of your app. Use debug flavor to call `TestFairy.begin()`, and release flavor to emit this call.

If you are not used to working with build variants, refer to [this post](https://blog.testfairy.com/create-a-custom-build-in-android/) the learn how.

In order for ProGuard to fully crop the TestFairy SDK from the final binary, you may use a wrapper class that differs in each of your flavors.

* Create a new Java folder for your **release** variant.
* Create a Java class somewhere in the shared (main) variant.
* Create the same package structure and Java class in the **release** variant as well.
* Put the code below into the Java class under **main/java**.
```
public class TestFairyWrapper {
  public static void begin(Activity activity, String apikey) {
    TestFairy.begin(activity, apikey);
  }
}
```
* Put the code below into the Java class under **release/java**.
```
public class TestFairyWrapper {
  public static void begin(Activity activity, String apikey) {
    // Do nothing
  }
}
```
* Call `TestFairyWrapper.begin()` in your main activity.

Without any calls to any of the TestFairy SDK, Proguard will eventually remove the entire compiled code from the result `classes.dex` and the final APK.

### Option 2: Use a class loader

Android allows loading classes into memory on-the-fly. This is for advanced developers. You can use Java reflections to load TestFairy class into memory only on a Debug build.

Replace the code where you call `TestFairy.begin()` with the code below.

```
try {
    Class cls = Class.forName("com.testfairy.TestFairy");
    Method method = cls.getMethod("begin", android.content.Context.class, String.class);
    method.invoke(cls, this, "SDK-XXXXXXX");
} catch (Exception e) { /* ignore */ }
```

Then, in your `build.gradle` file, change the SDK dependency with `debugImplementation 'testfairy:testfairy-android-sdk:1.+@aar'` or any other version of your choosing.

## Strict Storage Security With S3
TestFairy allows enterprise clients with sensitive data and strict security requirements, to use their own CDN for storage.

This means that apps are uploaded via API to the company's CDN, and TestFairy only keeps the URL to the app.

Note: In these cases, the *NEW UPLOAD* button is disabled.

This also means that all of the app artifacts (IPA and APK files) are stored on a self-managed S3 bucket, and in order to upload files, you will have to use the [Upload API](https://docs.testfairy.com/API/Upload_API.html) and provide pre-signed URLs to an artficat for processing.

For more information please [contact TestFairy Support](https://testfairy.com/contact)

## Disable Play Protect
In order to disable Goggle Play Protect, do the following:
---
* In your device Play Store open the menu and press Play Protect:

![alt](../../img/android/playstore/PlayStore1.png)
---
* Under the Play Protect section, disable the option like this:

![alt](../../img/android/playstore/PlayStore2.png)   **⇒**  ![alt](../../img/android/playstore/PlayStore3.png)

## Running TestFairy In Production
Does TestFairy work in production with live traffic?

Yes. TestFairy works both in testing and in production. However, before doing that, please read this document carefully.

When running TestFairy in production, you may record sensitive data such as medical information, financial data or photos.

Therefore it is important to follow these guidelines:

1. On iOS, you **must** request explicit user consent before recording start.
Please read carefully the [Apple guidelines](https://developer.apple.com/app-store/review/guidelines/) and pay special attention to section 2.5.14

2. On Android, you **must** use [TestFairy Production SDK](https://docs.testfairy.com/Android/Production_SDK.html) to comply with [Play Store Developer Distribution Agreement](https://play.google.com/about/developer-distribution-agreement.html).

3. When recording sensitive data you **must** use TestFairy's [end-to-end encryption](/Security/End_to_End_Data_Encryption.html) with your own private keys, so that only your team will be able to see your sessions.

4. You **must** [hide sensitive data](/SDK/Hiding_Sensitive_Data.html) such as credit card numbers, passwords, or other PII, so that this info will not be uploaded to the server.

5. It is strongly recomended to use a [private cloud](/Security/Private_Cloud.html) .

6. In case you are using TestFairy for customer support to better understand your users in case of a technical issue,
it is recomended to add a button to your app menu (call it "advanced support"?) and have that button call `TestFairy.begin()`.
Before calling `begin()` ask the user if this is ok to record their screen for quality assurance purposes.
When doing that, make sure that session duration is set to 2-3 minutes, just enough to identify the cause of a problem.

7. You **must** include a proper disclaimer in your app terms of service document.
You must explain exactly what data you collect, and how to request deletion of that data.
For more information about [GDPR](/Security/GDPR.html), please [contact the TestFairy team](https://testfairy.com/contact)

8. Please make sure never to use TestFairy Auto-update with apps that are shipped to production. This is a clear violation of both Apple and Google's terms.

## Android TV Video Player Tracking
How do I see events such as buffering and playback statuses for video players in my TestFairy dashboard?

You can take a look at [this blog post](https://blog.testfairy.com/tracking-video-events-in-android-tv-with-mediaplayer/) to do it manually or copy [this](https://github.com/testfairy-blog/TestFairyMediaPlayerGlue/blob/master/TestFairyMediaPlayerGlue.java) utility file in your project.

Once you import the extension, you can initialize the tracker with these one liners.

#### with MediaPlayer
```java
// Initialize
TestFairyMediaPlayerGlue.PlayerWrapper wrapper = TestFairyMediaPlayerGlue.createByWrapping(myMediaPlayer);
// use wrapper to configure further listeners and behavior
```

#### or with MediaPlayerAdapter

```java
// Initialize
TestFairyMediaPlayerGlue.PlayerAdapterWrapper wrapper = TestFairyMediaPlayerGlue.createByWrapping(myPlayerAdapter);
// use wrapper to configure further listeners and behavior
```

#### or with ExoPlayer

Copy [this](https://github.com/testfairy-blog/TestFairyMediaPlayerGlue/blob/master/TestFairyExoPlayerAnalyticsListener.java) listener in your project and initialize it with the following line.

```java
// Initialize
exoPlayer.addAnalyticsListener(new TestFairyExoPlayerAnalyticsListener(exoPlayer));
```

The internals of `TestFairyExoPlayerAnalyticsListener` is explained [here](https://blog.testfairy.com/exoplayer-analytics-for-android-tv/) for curious hackers.

## Deleting your account
At TestFairy we understand that at some point you may want to delete your data. As much as we are sad to see you leaving us, we will help you make it happen.

First, this document is for __developers__, users who uploaded apps to TestFairy, added the TestFairy SDK to their app, and invited testers to their project.
If you are a developer, please continue reading.


If you are a __tester__, please contact the developer who invited you to their project and ask to be removed.

### How to delete your developer account:

In order to delete your TestFairy account please follow these steps:

  1. Start by removing all the other admins from your account. Log in, go to the [Team](https://app.testfairy.com/settings/cpanel/) menu at the top right, select all admins in the account and remove them:

  ![](/img/FAQ/delete-account-01.png)

  2. Once all admins are removed go to your [Account Preferences](https://app.testfairy.com/settings/account/) → Account section and at the bottom of the screen press the `Delete my account` button

  ![](/img/FAQ/delete-account-02.png)

  ![](/img/FAQ/delete-account-03.png)

Your account is now deleted.

### How to delete the data of a specific tester:

TestFairy helps developers record videos showing how users used their apps.
In order to be able to track the sessions of a specific user, you must call __setUserId()__ with a unique identifier that can help you locate the specific session/s.


If one of your testers asked you to delete their data please do the following.

1. Remove the tester from your [testers list](https://app.testfairy.com/testers)

2. Search for the [sessions](https://app.testfairy.com/search) of this user and delete them one by one.

If you did not call setUserId() or you don't have any other way to locate the specific sessions that need to be deleted, please delete the builds that were used by the user.


## App Not Installed Android 10
Are are having problem installing an app on Android 10, and getting an error message "App not installed"?

![](/img/android/sdk/app_not_installed.png)

Here are a few possible reasons:

# Is the app already installed on your device?

It might be that an app with the same package name that has a different signature is already be installed on your device. Android does not allow different signatures for the same package name. In order to solve that, please delete the app from your device and try again.

In order to prevent this error in the future, please make sure you always sign your consecutive builds with the same signature. If changing the signature was intentional, you can go ahead and change the package name as well, or just communicate the change with your testers and ask them to uninstall the app with deprecated signatures before proceeding with the installation.

# Is the device out of storage?

 This is easy to solve. Free up some space and try again.

Installing an app requires at least twice the space consumed by the APK package plus total uncompressed space consumed by the app files.

# Does the device allow installation from unknown sources?

By default Android allows installation only from the Play Store. In order to allow installation of apps from other sources, open the __Settings__ app and locate "Install Unknown Apps" under __Privacy/Security__ settings. Enable the permission for the app which you use to install your APK. In most cases, this is the app being updated, a file manager or the browser. Old Android devices expose this setting under a single toggle named "Install App from Unknown Sources".

# Does the problem happen only on Android 10?

If you can install your app on old Android versions without a problem, and only new versions (Android 10?) give you a hard time, it might be related to your signature.

Although this is not a globally defined default, some Android manufactures (Google and others)require signing apps with a v2 signature on their latest versions and may not allow installing apps signed only with the v1 signature scheme.

If you build your app via Android Studio's __Generate Signed Bundle / Apk__ command, make sure you tick the v2 signature checkbox as well as v1 to include both signatures in the final APK.

![](/img/android/sdk/generate_v1_v2_sign.png)

  * If you prefer signing your app during a build automatically, make sure you include the following settings in your *app/build.gradle* script.

```
android {
    defaultConfig {
        ...
    }

    signingConfigs {
        debug {
            v1SigningEnabled true
            v2SigningEnabled true

            // Add debug keystore credentials here
        }

        release {
            v1SigningEnabled true
            v2SigningEnabled true

            // Add release keystore credentials here
        }
    }
}
```

## How to verify if an app is signed with v1 or v2?

In order to verify that both signatures are included in the APK by running the following command inside your build tools folder (*$ANDROID_HOME/build-tools/x.y.z*).

`./apksigner verify --print-certs -v path/to/app.apk`

The expected output looks like this:

```
Verifies
Verified using v1 scheme (JAR signing): true
Verified using v2 scheme (APK Signature Scheme v2): true
```

Check out [Android docs](https://source.android.com/security/apksigning/v2) to learn more about v2 signatures.

## Improving Flutter Performance
Are you having performance issues with TestFairy Flutter Plugin?

Here are a few possible solutions:

## Gestures are sometimes ignored or app feels sluggish

Try disabling `TestFairyGestureDetector` to see if it makes a difference.

```dart
// Change this
runApp(TestFairyGestureDetector(child: TestfairyExampleApp()));

// into this
runApp(TestfairyExampleApp());
```

## Network calls are slower than they are supposed to be

Try disabling network logging or update to TestFairy plugin 2.X.Y releases.

```dart
// Remove this line entirely to disable network logging
HttpOverrides.global = TestFairy.httpOverrides();
```

## Devices with big screens suffer from frame drops or sessions have too little screenshots

Get in touch with <a href="mailto:support@testfairy.com">support@testfairy.com</a> to discuss how we can improve this together.

## Null Safety in Flutter
Starting from Dart SDK 2.12, Flutter apps automatically opt-in for [null safety](https://dart.dev/null-safety/understanding-null-safety) in Dart code. TestFairy Flutter plugin is developed to support this shift. However not all apps are ready to make the transition to null-safe Dart. When you compile your app, if your errors look similar to this, it means your app has null-safe code mixed with the old Dart type system.

```
Error: This requires the null safety language feature, which is experimental.
    You can enable the experiment using the '--enable-experiment=non-nullable' command line option.
```

To be able to utilize these new features, apps can either [migrate](https://dart.dev/null-safety/migration-guide) to null-safe Dart or [run in mixed mode](https://dart.dev/null-safety/unsound-null-safety).

Due to the nature of how null-safety implemented and what kind of guarentees it allows during compile time checks, this type of mixed mode programs require [extra attention](https://dart.dev/null-safety/unsound-null-safety#testing-or-running-mixed-version-programs) to build.

We advocate for the full migration in general but if that is not possible, here is a few steps to get started with null safety.

* Use latest Flutter and Dart SDK.

```yaml
# pubspec.yaml

environment:
  sdk: '>=2.12.0 <3.0.0'
  flutter: ">=1.22.0"
```

* Run `dart pub get` to update dependencies.

* You'll start seeing lots of Dart analysis errors, that's alright.

* Add `// @dart=2.9` to beginning of every file that is still using the old Dart to let the compiler know which files should skip compile time checks for null safety.

If you are still having analysis error, it means some of your dependencies doesn't have the `// @dart=2.9` annotation properly placed in their source code. Try checking if those libraries has null-safe (named usually as `libname-nullsafe`) versions in `pub`.

## Feedback Form Customizations
See the [SDK Documentation](https://docs.testfairy.com/SDK/Customizing_feedback_dialog.html) for more information.

## Migrate from Bintray
Jfrog has recently announced the [sunset of JCenter and Bintray](https://jfrog.com/blog/into-the-sunset-bintray-jcenter-gocenter-and-chartcenter/), great services that we used to distribute our SDK.

As a result, starting from version [1.12.0](/Android/Changelog.html), the TestFairy Android SDK will be hosted under [maven.testfairy.com](https://maven.testfairy.com).

In order to continue get updates, developers MUST update gradle to keep getting new TestFairy Android SDK versions.

Please follow the steps below to point your project to the new maven repository.

For Further reading on this subject please reffer to our blog: [JCenter and Bintray is shutting down, what to do?
](https://testfairy.com/blog/jcenter-and-bintray-is-shutting-down-what-to-do/)

### 1. Add TestFairy maven repository to your project's **build.gradle** script

In *PROJECT_ROOT/build.gradle*:

```
    buildscript {
        repositories {
            maven { url 'https://maven.testfairy.com' }
        }
    }
```


### 2. Change TestFairy SDK dependency lines in your app's **build.gradle** script

In *PROJECT_ROOT/app/build.gradle*:

```
    dependencies {
        // Delete this line: `implementation 'testfairy:testfairy-android-sdk:1.+@aar'`

        // Add this line:
        implementation 'com.testfairy:testfairy-android-sdk:1.+@aar'
    }
```
