---
id: platforms
title: Platforms
sidebar_label: Platforms
---
## Cordova
Adding the TestFairy plugin to your Cordova or Phonegap project is simple.

For Ionic applications, please check out the [Ionic](https://docs.testfairy.com/Platforms/Ionic.html) documentation.

## Installation

Add the plugin to your project via [npm](https://www.npmjs.com/package/com.testfairy.cordova-plugin). Run the following command from a terminal:

```
cordova plugin add com.testfairy.cordova-plugin
```

Alternatively, you can install it directly from GitHub:

```
cordova plugin add https://github.com/testfairy/testfairy-cordova-plugin
```

## Upgrading

To upgrade your plugin, please run:

```
cordova plugin update com.testfairy.cordova-plugin
```

## Usage

Initialize TestFairy with your [App Token](https://app.testfairy.com/settings/#apptoken) by calling `TestFairy.begin`. Your **APP TOKEN** is available at `https://app.testfairy.com/settings/#apptoken`.

We recommend to invoking `TestFairy.begin` from `onDeviceReady` in `index.js`:

```
  onDeviceReady: function() {
    app.receivedEvent('deviceready');
    TestFairy.begin("APP TOKEN");
  }
```

### Logging Errors

We recommend logging error event to TestFairy. This will display the exceptions along with the rest of the session data, including logs and attributes. Please
refer to the [Exception Logging](https://docs.testfairy.com/SDK/Exception_Logging.html#cordova) document for more information.

### Identifying Your Users

See the [SDK Documentation](https://docs.testfairy.com/SDK/Identifying_Your_Users.html#cordova) for more information.

### Session Attributes

See the [SDK Documentation](https://docs.testfairy.com/SDK/Session_Attributes.html#cordova) for more information.

### Remote Logging

See the [SDK Documentation](https://docs.testfairy.com/SDK/Remote_Logging.html#cordova) for more information.


## Support for ARM architecture vs x86

`ERROR ITMS-90087: "Unsupported Architectures. The executable TestFairy.framework contains unsupported architectures '[x86_64, i386]'`


This happens when you export your iOS app for the App store. The App Store only supports apps built for the ARM architecture, however to allow developers to also test in the iOS Simulator, we include the architectures for 64-bit (x86_64) and 32-bit (i386) Intel architectures.

The quickest solution is to strip these architectures from `TestFairy.framework` when archiving. You must add the following run script to your Xcode build phases.

```
APP_PATH="${TARGET_BUILD_DIR}/${WRAPPER_NAME}"

find "$APP_PATH" -name 'TestFairy.framework' -type d | while read -r FRAMEWORK
do
    FRAMEWORK_EXECUTABLE_NAME=$(defaults read "$FRAMEWORK/Info.plist" CFBundleExecutable)
    FRAMEWORK_EXECUTABLE_PATH="$FRAMEWORK/$FRAMEWORK_EXECUTABLE_NAME"
    echo "Executable is $FRAMEWORK_EXECUTABLE_PATH"
    echo $(lipo -info "$FRAMEWORK_EXECUTABLE_PATH")

    FRAMEWORK_TMP_PATH="$FRAMEWORK_EXECUTABLE_PATH-tmp"

    if $(lipo "$FRAMEWORK_EXECUTABLE_PATH" -verify_arch "i386") ; then
        lipo -output "$FRAMEWORK_TMP_PATH" -remove "i386" "$FRAMEWORK_EXECUTABLE_PATH"
        echo "    i386 architecture removed"
        rm "$FRAMEWORK_EXECUTABLE_PATH"
        mv "$FRAMEWORK_TMP_PATH" "$FRAMEWORK_EXECUTABLE_PATH"
    fi

    if $(lipo "$FRAMEWORK_EXECUTABLE_PATH" -verify_arch "x86_64") ; then
        lipo -output "$FRAMEWORK_TMP_PATH" -remove "x86_64" "$FRAMEWORK_EXECUTABLE_PATH"
        echo "    x86_64 architecture removed"
        rm "$FRAMEWORK_EXECUTABLE_PATH"
        mv "$FRAMEWORK_TMP_PATH" "$FRAMEWORK_EXECUTABLE_PATH"
    fi
done
```

> **Note**: It's important that you only run this script during **only when installing**. The image below shows the necessary checkbox to prevent this script from running during regular development builds

![only-when-archiving](/img/only-when-installing.png)

## Where to go from here?

Congratulations! You've successfully integrated TestFairy into your Cordova project! Visit your [dashboard](http://app.testfairy.com/), where you should see your app listed.

* Have a look at the [API documentation](https://github.com/testfairy/testfairy-cordova-plugin/blob/master/www/testfairy.js) for other calls you can make to the TestFairy plugin

* Follow the project on [GitHub](https://github.com/testfairy/testfairy-cordova-plugin) for updates, bug reports, or to contribute to the project!

## Ionic
Adding the TestFairy plugin to your Ionic project is simple. The following instructions are for Ionic 3.

## Installation

Run the following commands from your application root folder:

```
ionic cordova plugin add com.testfairy.cordova-plugin
```

Alternatively, you can install it directly from GitHub:

```
ionic cordova plugin add https://github.com/testfairy/testfairy-cordova-plugin
```

## Upgrading

To upgrade your plugin, please run:

```
ionic cordova plugin update com.testfairy.cordova-plugin
```

## Usage

Initialize TestFairy with your [App Token](https://app.testfairy.com/settings/#apptoken) by calling `TestFairy.begin`. Your **APP TOKEN** is available at `https://app.testfairy.com/settings/#apptoken`.

We recommend to invoking `TestFairy.begin` from `platform.ready()` in `src/app/app.component.ts`. Also, be sure to declare `TestFairy` at the top of the file.

```
import { Component } from '@angular/core';
import { Platform } from 'ionic-angular';
import { StatusBar } from '@ionic-native/status-bar';
import { SplashScreen } from '@ionic-native/splash-screen';

import { HomePage } from '../pages/home/home';

// Declare the TestFairy instance
declare var TestFairy: any;

@Component({
  templateUrl: 'app.html'
})
export class MyApp {
  rootPage:any = HomePage;

  constructor(platform: Platform, statusBar: StatusBar, splashScreen: SplashScreen) {
    platform.ready().then(() => {
			TestFairy.begin(APP TOKEN);
      // Okay, so the platform is ready and our plugins are available.
      // Here you can do any higher level native things you might need.
      statusBar.styleDefault();
      splashScreen.hide();
    });
  }
}
```

**Note**: We currently do not support plugin mocking or browser development. During your development phase, we recommend checking for the existence of `TestFairy` on the `window` object before invoking any methods on the TestFairy object, e.g.

```
// Check if TestFairy is available (will be undefined in browser)
if ((<any>window).TestFairy) {
	TestFairy.begin(APP TOKEN);
}
```

### Identifying your users

See the [SDK Documentation](https://docs.testfairy.com/SDK/Identifying_Your_Users.html#cordova) for more information.

### Session Attributes

See the [SDK Documentation](https://docs.testfairy.com/SDK/Session_Attributes.html#cordova) for more information.

### Remote Logging

See the [SDK Documentation](https://docs.testfairy.com/SDK/Remote_Logging.html#cordova) for more information.

## Where to go from here?

Congratulations! You've successfully integrated TestFairy into your Ionic project! Visit your [dashboard](http://app.testfairy.com/), where you should see your app listed.

* Have a look at the [API documentation](https://github.com/testfairy/testfairy-cordova-plugin/blob/master/www/testfairy.js) for other calls you can make to the TestFairy plugin

* Follow the project on [GitHub](https://github.com/testfairy/testfairy-cordova-plugin) for updates, bug reports, or to contribute to the project!

## React Native
Adding the TestFairy plugin to your Ionic project is simple. The following instructions are for Ionic 3.

## Installation

Run the following commands from your application root folder:

```
ionic cordova plugin add com.testfairy.cordova-plugin
```

Alternatively, you can install it directly from GitHub:

```
ionic cordova plugin add https://github.com/testfairy/testfairy-cordova-plugin
```

## Upgrading

To upgrade your plugin, please run:

```
ionic cordova plugin update com.testfairy.cordova-plugin
```

## Usage

Initialize TestFairy with your [App Token](https://app.testfairy.com/settings/#apptoken) by calling `TestFairy.begin`. Your **APP TOKEN** is available at `https://app.testfairy.com/settings/#apptoken`.

We recommend to invoking `TestFairy.begin` from `platform.ready()` in `src/app/app.component.ts`. Also, be sure to declare `TestFairy` at the top of the file.

```
import { Component } from '@angular/core';
import { Platform } from 'ionic-angular';
import { StatusBar } from '@ionic-native/status-bar';
import { SplashScreen } from '@ionic-native/splash-screen';

import { HomePage } from '../pages/home/home';

// Declare the TestFairy instance
declare var TestFairy: any;

@Component({
  templateUrl: 'app.html'
})
export class MyApp {
  rootPage:any = HomePage;

  constructor(platform: Platform, statusBar: StatusBar, splashScreen: SplashScreen) {
    platform.ready().then(() => {
			TestFairy.begin(APP TOKEN);
      // Okay, so the platform is ready and our plugins are available.
      // Here you can do any higher level native things you might need.
      statusBar.styleDefault();
      splashScreen.hide();
    });
  }
}
```

**Note**: We currently do not support plugin mocking or browser development. During your development phase, we recommend checking for the existence of `TestFairy` on the `window` object before invoking any methods on the TestFairy object, e.g.

```
// Check if TestFairy is available (will be undefined in browser)
if ((<any>window).TestFairy) {
	TestFairy.begin(APP TOKEN);
}
```

### Identifying your users

See the [SDK Documentation](https://docs.testfairy.com/SDK/Identifying_Your_Users.html#cordova) for more information.

### Session Attributes

See the [SDK Documentation](https://docs.testfairy.com/SDK/Session_Attributes.html#cordova) for more information.

### Remote Logging

See the [SDK Documentation](https://docs.testfairy.com/SDK/Remote_Logging.html#cordova) for more information.

## Where to go from here?

Congratulations! You've successfully integrated TestFairy into your Ionic project! Visit your [dashboard](http://app.testfairy.com/), where you should see your app listed.

* Have a look at the [API documentation](https://github.com/testfairy/testfairy-cordova-plugin/blob/master/www/testfairy.js) for other calls you can make to the TestFairy plugin

* Follow the project on [GitHub](https://github.com/testfairy/testfairy-cordova-plugin) for updates, bug reports, or to contribute to the project!

## Expo
<iframe width="560" height="315" src="https://www.youtube.com/embed/HpLOsNwd_FM" frameborder="0" allowfullscreen></iframe>

[TestFairy for React Native](https://www.npmjs.com/package/react-native-testfairy) is a bridge to the TestFairy SDK and it is also supported for Expo projects. Integrating the TestFairy SDK into your app enables you to better understand how your app performs on real devices. It tells you when and how people are using your app, and provides you with any metrics you may need to optimize your user experience and code.

# Requirements

You will have to eject your Expo project before installing TestFairy. This is a revertable process but reverting will also make you lose access to TestFairy features. Apps that require native components are expected to utilize the bare workflow as stated in the [Expo docs](https://docs.expo.io/expokit/eject/).

# Steps

From your project root, run the following commands:

```
expo eject
npm install --save react-native-testfairy

cd ios
pod install
```

# Notes

Since all Expo apps are React Native apps behind the scenes, all features introduced in [TestFairy for React Native](https://www.npmjs.com/package/react-native-testfairy) applies to Expo as well.

## Unity
In this document:

- [Installation](#installation)
- [Setting Screen Name](#set-screen-name)
- [Logging Exceptions](#log-exceptions)
- [Troubleshooting](#troubleshooting)
- [Identifying Your Users](#identify-users)
- [Setting Session Attributes](#session-attributes)
- [Remote Logging](#remote-logging)

<a name="installation"></a>
## Installation

The steps in this section are an example of how to add the TestFairy Unity SDK to your Unity project.

1. From the TestFairy Unity SDK GitHub page, download the [latest](https://github.com/testfairy/testfairy-unity-plugin/releases) version of the `unitypackage`.
   ![download-latest](/img/unity/unity-latest.png)

2. In your open Unity project, navigate to **Assets** --> **Import Package** --> **Custom Package**

  ![custom-import](/img/unity/custom-import.png)

3. In the Import Unity Package window, first click **All** to include the TestFairy SDK in your app. Then click **Import**.
   ![select-files](/img/unity/file-select.png)

4. To use the TestFairy Unity SDK, click `mainCamera` in Hierarchy and in the Inspector click `Add Component`.
	> **Note:** you can add the TestFairy script to any game object. TestFairy is a singleton so no harm is done.

  ![Step 2](https://raw.githubusercontent.com/testfairy/testfairy-unity-plugin/master/Images/step2.png)

5. Click `Add Component` again, and select a `Script` component. Type in the name of the script, for example `mainCameraScript`, and click on `Create and Add`.

  ![Step 3](https://raw.githubusercontent.com/testfairy/testfairy-unity-plugin/master/Images/step3.png)

6. Edit the newly created CSharp script, add `using TestFairyUnity;` to the import section, and a call to `TestFairy.begin();` with your app token. You can find your app token in the [Account Settings](https://app.testfairy.com/settings/#apptoken) page.

  ![Step 4](https://raw.githubusercontent.com/testfairy/testfairy-unity-plugin/master/Images/step4.png)

 Here is the code, for easy copy-pasting:

 ```
 using UnityEngine;
 using System.Collections;
 using TestFairyUnity;

 public class mainCameraScript : MonoBehaviour {

     // Use this for initialization
     void Start () {
         TestFairy.begin("PUT YOUR SDK APP TOKEN HERE SEE COMMENT ABOVE");
     }

     ...
 }
 ```

7. Save, build and run.

## Usage

<a name="set-screen-name"></a>
### Setting Screen Name

TestFairy can capture screenshots during a recorded session. It attempts to autmatically name a screenshot based on different measures. In order to override this you can invoke `setScreenName`, and set your own name for a captured screen. `setScreenName` expects a String, so developers are free to label screenshots with any appropriate label. Some developers make use of the level name to set the screenshot, for example:

```
using UnityEngine;
using System.Collections;
using TestFairyUnity;
using UnityEngine.SceneManagement;

public class cameraScript : MonoBehaviour {
...
	void OnLevelWasLoaded(int level) {
		TestFairy.setScreenName(Application.loadedLevelName);
	}
...
}
```

<a name="log-exceptions"></a>
### Log your exceptions

If you would like to capture exception logs and send them to the TestFairy dashbord use this code example:

```
private void OnEnable()
{
	Application.logMessageReceivedThreaded += HandleLog;
}

private void OnDisable()
{
	Application.logMessageReceivedThreaded -= HandleLog;
}

private void HandleLog(string message, string stackTrace, LogType type)
{
	TestFairy.log(message);
	TestFairy.log(stackTrace);
}
```

<a name="troubleshooting"></a>
### Troubleshooting

If you omit adding the above script, you may encounter the following errors:

> ERROR ITMS-90087: "Unsupported Architectures. The executable TestFairy.framework contains unsupported architectures '[x86_64, i386]'

This happens when you export your iOS app for the App store. The App Store only supports apps built for the ARM architecture, however to allow developers to also test in the iOS Simulator, we include the architectures for 64-bit (x86_64) and 32-bit (i386) Intel architectures.

> Error: exportArchive: IPA processing failed
> Error Domain=IDEFoundationErrorDomain Code=1 "IPA processing failed" UserInfo={NSLocalizedDescription=IPA processing failed}

This happens when you export an Ad hoc version of your iOS app. Most often seen in Unity Cloud build.

<a name="identify-users"></a>
### Identifying your users

See the [SDK Documentation](https://docs.testfairy.com/SDK/Identifying_Your_Users.html#unity) for more information.

<a name="session-attributes"></a>
### Session Attributes

See the [SDK Documentation](https://docs.testfairy.com/SDK/Session_Attributes.html#unity) for more information.

<a name="remote-logging"></a>
### Remote Logging

See the [SDK Documentation](https://docs.testfairy.com/SDK/Remote_Logging.html#unity) for more information.

## Xamarin Component
Xamarin Component is available [here](https://docs.testfairy.com/Platforms/Xamarin_Component.html)

TestFairy is available for both Android and iOS. You can install the bindings by 1 of 2 ways:

1. Download the latest binding DLL directly from [GitHub](https://github.com/testfairy/testfairy-xamarin/releases) for your specific platform.

1. Install the bindings through [NuGet](https://www.nuget.org/packages/TestFairy.Xamarin/).

You will need an app token (TESTFAIRY_APP_TOKEN), which can be found in your [settings page](http://app.testfairy.com/settings/)

## Using the Xamarin SDK

Open `AppDelegate.cs` in your solution, and override or add the following code to `FinishedLaunching`.

```
using TestFairyLib;
...

public override bool FinishedLaunching (UIApplication app, NSDictionary options)
{
	TestFairy.Begin (TESTFAIRY_APP_TOKEN);

	// Rest of the method here
	// ...
}
```

## Usage

### Identifying your users

See the [SDK Documentation](https://docs.testfairy.com/SDK/Identifying_Your_Users.html#xamarin) for more information.

### Session Attributes

See the [SDK Documentation](https://docs.testfairy.com/SDK/Session_Attributes.html#xamarin) for more information.

### Remote Logging

See the [SDK Documentation](https://docs.testfairy.com/SDK/Remote_Logging.html#xamarin) for more information.

### Upload dSYM

With TestFairy, symbolicating crash reports is as easy as pie. A simple Build Phase script can automatically upload the compressed .dSYM file for future symbolicaton.

To enable automatic uploads of .dSYM files, please follow these steps:

#### Step 1:

Copy **upload_dsym.sh** to your project folder. [Download here](https://s3.amazonaws.com/testfairy/sdk/upload-dsym.sh).

#### Step 2:

In Xamarin Studio, click on your project in the left sidebar, then open **"Settings"** and choose **Options**.

![alt](../../img/xamarin/project_options.png)

#### Step 3:

Click on **Custom Commands** on the left, press **Select a project operation**  and select **After Build**

![alt](../../img/xamarin/custom_command.png)

#### Step 4:

Add the following command to the command line

```sh
sh upload-dsym.sh UPLOAD_API_KEY -p DSYM_PATH
```

Make sure to replace **UPLOAD_API_KEY** with your upload API key, which can be found in the [Settings](https://app.testfairy.com/settings/) page.  
Replace **DSYM_PATH** with the path of your build folder.

#### Step 5:

Set the *"Working Directory"* to the path of *upload-dsym.sh* file

![alt](../../img/xamarin/upload_dsym_command.png)

### Xamarin Insights Integration

With Insights, Xamarin developers can review their app usage using the Xamarin Insights component. TestFairy fills in the gap by providing additional metrics, such as CPU usage and memory allocation and even video capture from the device. Any question you may have, as a developer, will be answered in the TestFairy session reports.

![alt](../../img/ios/xamarin-insights/xamarin-insights-integration.png)

In the left sidebar of **Insights**, you will now see a link to the session recorded by TestFairy.

## Integration

By simply adding the following code, the session recorded by TestFairy will be associated in Xamarin Insights as well (as seen in the screenshot above.) Place this snippet right after initializing Xamarin.Insights and TestFairy.

```csharp
NSNotificationCenter.DefaultCenter.AddObserver (TestFairy.SessionStartedNotification, delegate (NSNotification n) {
	  NSString sessionUrl = (NSString)n.UserInfo.ObjectForKey(TestFairy.SessionStartedUrlKey);
	  Insights.Track ("TestFairy", new Dictionary<string, string> {{ "URL", sessionUrl }});
});
```

## Android
Either in your custom Android Application class, or in any Activity class, simply make a call to Com.TestFairy.TestFairy.Begin(<TESTFAIRY_APP_TOKEN>). Below, you can see an example of invoking begin from the Main Activity.

```
using Com.Testfairy;
...

public class MainActivity : Activity {
	protected override void OnCreate (Bundle savedInstanceState)
    {
		base.OnCreate (savedInstanceState);

		TestFairy.Begin (this, TESTFAIRY_APP_TOKEN);
		SetContentView (Resource.Layout.Main);
        ...
    }
}

```

## Telling TestFairy what to record

TestFairy can record screens cast directly from the device, as well as monitor CPU consumption and memory allocations. It grabs
logs and even enables your users to provide feedback upon shaking their device.

To configure how and what TestFairy records, visit your **Build Settings**. You will see the build after calling Begin () at
least once.

## Mixing with other crash handlers

TestFairy plays nice. There is no problem using the crash handler with another reporter.

## Titanium
The TiTestFairy Module extends the Appcelerator Titanium Mobile framework, with the TestFairy Android and iOS SDKs. The TestFairy SDK enables integration with TestFairy to give you a better understanding of how your app performs on real devices. It tells you when and how people are using your app, and provides you with any metric you may need to optimize your user experience and code.

## Installation

* Simply add the following lines to your `tiapp.xml` file:
```xml
<modules>
	<module platform="iphone">com.testfairy.titestfairy</module>
</modules>
```

* Download the [latest release.](https://github.com/testfairy/ti.testfairy/releases/latest/)
  * Be sure to either download either the Android (com.testfairy.titestfairy-android-2.1.3.zip) or the iOS (com.testfairy.titestfairy-iphone-2.1.3.zip) depending on the platform you're targeting.

* Add the module to your Titanium Mobiles
  - “Help” -> "Install Mobile Module..."
  - or by unzipping the contents of the module zip file into your `Titanium/modules/iphone` or `Titanium/modules/android` folders.

* Include the module in your code and use it:

```javascript
	var TiTestFairy = require('com.testfairy.titestfairy');
	TiTestFairy.begin("<APP TOKEN>");
```

NOTE: Replace 'APP TOKEN' with your token, which can be found in the [user preferences page](https://app.testfairy.com/settings/#app-token).

For more detailed code examples take a look at our [example app](https://github.com/testfairy/ti.testfairy/blob/feat-readme/example/app.js).

## Usage

### Identifying your users

See the [SDK Documentation](https://docs.testfairy.com/SDK/Identifying_Your_Users.html#titanium) for more information.

### Session Attributes

See the [SDK Documentation](https://docs.testfairy.com/SDK/Session_Attributes.html#titanium) for more information.

### Remote Logging

See the [SDK Documentation](https://docs.testfairy.com/SDK/Remote_Logging.html#titanium) for more information.

## Reference

`TiTestFairy.version;` - Returns the version of the TestFairy SDK.

`TiTestFairy.setCorrelationId(correlationId)` - Sets an identifier that can be looked up through dashboard.

`TiTestFairy.pushFeedbackController()` - Present a feedback dialog to the user.

`TiTestFairy.sendUserFeedback(string)` - Send a feedback on behalf of the user. Call when using a in-house feedback view controller with a custom design and feel. Feedback will be associated with the current session.

`TiTestFairy.updateLocation(locations)` - Mark geo location at this point (to be used with `navigator.geolocation.getCurrentPosition`).

`TiTestFairy.checkpoint(checkpointName)` - Mark a checkpoint in session.

`TiTestFairy.pause()` - Pauses the current session until resume() is called.

`TiTestFairy.resume()` - Resumes a paused session.

`TiTestFairy.sessionUrl()` - Returns the address of the recorded session on TestFairy's developer portal. Will return nil if recording has not started yet.

`TiTestFairy.takeScreenshot()` - Takes a screenshot.

## Nativescript
TestFairy for Nativescript is a bridge to the [TestFairy](https://www.testfairy.com) SDK. Integrating the TestFairy SDK into your app enables you to better understand how your app performs on real devices. It tells you when and how people are using your app, and provides you with any metrics you may need to optimize your user experience and code.

## Installation

```
tns plugin add nativescript-testfairy
```

## Usage
Once the native library is added to your project, you can now enable session recording with TestFairy. You will need an app token, which can be found in your [Preferences](http://app.testfairy.com/settings/) page on your TestFairy account.

Next, from your JavaScript file, (app.js or app.ts for example), import the TestFairy bridge into your project, and invoke `begin` passing in the app token. The best time to invoke `begin` is usually on `launchEvent`.

Here's an example of how to start your recording in TypeScript:
```
import * as application from 'tns-core-modules/application';
import { TestFairySDK } from 'nativescript-testfairy';

application.on(application.launchEvent, (args) => {
    TestFairySDK.begin(<insert ios app token here>);
});

application.start({ moduleName: "main-page" });
```

Here's the same example of starting your recording in JavaScript:
```

require("./bundle-config");
var application = require("application");
var TestFairySDK = require('nativescript-testfairy').TestFairySDK;

application.on(application.launchEvent, (args) => {
    TestFairySDK.begin(<insert ios app token here>);
});

application.start({ moduleName: "main-page" });
```

Here's a final sample of starting your recording using Angular

```
import { Component } from "@angular/core";
import { TestFairySDK } from 'nativescript-testfairy';

@Component({
    moduleId: module.id,
    selector: "ns-app",
    templateUrl: "app.component.html"
})
export class AppComponent {
	constructor() {
		TestFairySDK.begin(<insert ios app token here>);
	}
}

```

And that's it! You can now log into your [account](http://app.testfairy.com) and view your sessions. Also, feel free to refer to the [documentation](https://github.com/testfairy/react-native-testfairy/blob/master/index.js) for other available APIs.

### User ID and Session Attributes

See the [SDK Documentation](https://docs.testfairy.com/SDK/Identifying_Your_Users.html#nativescript) for more information.

### Remote Logging

See the [SDK Documentation](https://docs.testfairy.com/SDK/Identifying_Your_Users.html#nativescript) for more information.

### Hiding views

See the [SDK Documentation](https://docs.testfairy.com/SDK/Identifying_Your_Users.html#nativescript) for more information.

### Where to go from here?

* Follow the project on [GitHub](https://github.com/testfairy/nativescript-testfairy) for updates, bug reports, or to contribute to the project!

## Neptune Software
In order to add the TestFairy plugin to a Neptune project, you need to do the following procedure.

## Enable the TestFairy plugin
Add the following to the config.xml file in the Neptune Cockpit under Run / Mobile Client / Device.
```
<plugin name="com.testfairy.cordova-plugin" source="npm"/>
```

## Initialize the TestFairy SDK:

Add the following code to your `init` script in the App Designer:

```
document.addEventListener("deviceready", function() {
    TestFairy.begin("APP TOKEN");
});
```

Remember to replace **APP TOKEN** with your own app token as displayed in [User Preferences](https://app.testfairy.com/settings/)

## Flutter
### Adding TestFairy to your flutter project

If you are developing your app in flutter here are the instructions to add the TestFairy sdk.

#### Installing
Use this package as a library

### 1. Depend on it
Add this to your package's pubspec.yaml.

```
dependencies:
  testfairy_flutter: any
```

### 2. Install it
You can install packages from the command line:
with Flutter:
```
$ flutter packages get
```
Alternatively, your editor might support flutter packages get. Check the docs for your editor to learn more.

### 3. Import it
Now in your Dart code, you can use:
```
import 'package:testfairy_flutter/testfairy.dart';

void main() {
  TestFairy.begin("SDK-myToken");
  runApp(MyApp());
}
```

### Quick Start
Include the library and run your main app like this.

Make sure your project is [AndroidX](https://flutter.dev/docs/development/androidx-migration) compatible.

Minimum supported iOS target is 9.0.

```yaml
# inside pubspec.yaml

dependencies:
  testfairy_flutter: any
```

```dart
// inside your main.dart

// @dart = 2.12
// You can use other dart versions but we suggest 2.12 for better compile time checks.
import 'dart:async';
import 'dart:io';
import 'package:testfairy_flutter/testfairy_flutter.dart';

void main() {
  HttpOverrides.global = TestFairy.httpOverrides();

  runZonedGuarded(
    () async {
      try {
        FlutterError.onError =
            (details) => TestFairy.logError(details.exception);

        // Call `await TestFairy.begin()` or any other setup code here.

        runApp(TestFairyGestureDetector(child: TestfairyExampleApp()));
      } catch (error) {
        TestFairy.logError(error);
      }
    },
    (e, s) {
      TestFairy.logError(e);
    },
    zoneSpecification: new ZoneSpecification(
      print: (self, parent, zone, message) {
        TestFairy.log(message);
      },
    )
  );
}
```

### How to compile with latest Flutter and null-safe Dart?

In order to use TestFairy with the latest **stable** Flutter channel, you must set the minimum version for the plugin as 2.1.0.

In order to use TestFairy with the latest **unstable** Flutter channel, you must clone this repo and use it as an offline dependency instead of the published version in pub.

1. Clone this [repo](https://github.com/testfairy/testfairy-flutter).

2. Use the following code to include the clone as an offline dependency (assuming both projects reside in the same directory as siblings).

```yaml
dependencies:
  testfairy_flutter:
    path: ../testfairy-flutter # or "./testfairy-flutter" if you cloned it inside your main project as a child directory
```

3. Checkout **testfairy-flutter** to your VCS without including its **.git** directory.

4. When there is a new update in this repo, delete **testfairy-flutter** and retry the steps.

### Troubleshoot
- **I see `warning: None of the architectures in ARCHS (x86_64) are valid` when I build and iOS app.**

Launch your Runner workspace and add `x86_64` to `VALID_ARCHS` under **Build Settings**.

- **I see `Specs satisfying the TestFairy dependency were found, but they required a higher minimum deployment target.` when I build and iOS app.**

You have to update the native SDK alongside with CocoaPods repository.

Run `pod repo update` and update the plugin in *pubspec.yaml*. Then run `cd ios; pod update TestFairy; cd ..`.

- **I have my own `HttpOverrides.global` setup. How can I make it work with TestFairy?**

Copy [this](https://github.com/testfairy/testfairy-flutter/blob/master/lib/src/network_logging.dart) file to your project. Add the necessary functionality and assign to `HttpOverrides.global` an instance from your new implementation.

- **I see `Errno::ENOENT - No such file or directory @ rb_sysopen - ./ios/Pods/Local Podspecs/testfairy.podspec.json` when I build an iOS app.**

This happens due to a pod misconfiguration bug on the Flutter side. We have [a blog post](https://blog.testfairy.com/errnoenoent-fix-for-flutter-ios/) explaining the fix.

Clean your project, remove *ios/Podfile* and Xcode workspace file entirely. (make sure you have backups just in case)
```
flutter clean
rm -rf ios/Podfile ios/Podfile.lock pubspec.lock ios/Pods ios/Runner.xcworkspace
```

Revert to **cocoapods 1.7.5** temporarily.
```
gem uninstall cocoapods
gem install cocoapods -v 1.7.5
```

Add the following line to the beginning of your iOS project's generated Podfile.
```
# Beginning of file
use_frameworks!

# The rest of the file contents
# ...
```

Install pods.
```
pod repo update
cd ios
pod install
cd ..
```

Retry your build.

Once your build is successful, you can update cocoapods back to its latest version. If the error reoccurs, you will have to revert back to 1.7.5 and retry the steps.

- **I see `Automatically assigning platform ios with version 8.0` when I build.**

TestFairy supports iOS 9.0 and above. Please change the build target accordingly in your Xcode project.

- **I see `Looks like TestFairy has an upgrade to do... 1.X.Y+hotfixZ is the latest stable branch` or errors related to Jetifier in the logs when I call an SDK method.**

Migrate your Android project to AndroidX by following [this](https://flutter.dev/docs/development/androidx-migration) guide.

- **I see `Undefined symbols for architecture` error during compilation.**

You must use frameworks and specify a platform version of at least `9.0` in your generated iOS project's Podfile. Please make the following changes in *ios/Podfile* and rebuild.
```
target 'Runner' do
  platform :ios, '9.0'   ####################################### <--- add this and specify at least 9.0

  use_frameworks!        ####################################### <--- add this, and try building if there is
                         #######################################      no Swift code or plugin in the project.
                         #######################################      If there is Swift code, please also add
                         #######################################      the marked line below

  ...
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['ENABLE_BITCODE'] = 'NO'
      config.build_settings['SWIFT_VERSION'] = '3.2'  ########## <--- add this, change the version to what's being
                                                      ##########      used in the project, remove if there is none
    end
  end
end
```

- **CocoaPods could not find compatible versions for pod "TestFairy".**

This is an old bug in the plugin pubspec file. First, run `flutter clean` in your root directory.

Please move *ios/Podfile.lock* into a temporary place before running `pod repo update; pod install` in your *ios* directory.

If some of the libraries you use need to be at specific versions, copy the necessary lines from your backed up *Podfile.lock* into the newly created one. Please keep the lines related to TestFairy (note the title case in the name) untouched.

Finally, run `pod repo update; pod install; pod update TestFairy` again to re-download libraries from the replaced lines.

If everything went smoothly, this issue should never happen again.

- **There are syntax errors in TestFairyFlutterPlugin.java or TestFairyFlutterPlugin.m file.**

In your project root, run `flutter clean; cd ios; pod repo update; pod install; pod update TestFairy; cd ..` and test again.

### API Reference
You can find a detailed documentation of the latest Dart interface [here](https://pub.dartlang.org/documentation/testfairy_flutter/latest/).

## Lumberyard
### Distributing Lumberyard Apps

### Android

Requirements:
* Lumberyard and Android SDK installed on Windows 10

#### Step 1 - Download Android SDK Components

Use Android's **SDK Manager** to download following components:

* Google Play APK Expansion Library
* Google Play Licensing Library
* Android SDK Platform-Tools
* Android SDK Tools

#### Step 2 - Download and Setup Lumberyard Components

Run Lumberyard's **Setup Assistant**.

If you haven't installed Lumberyard core, click *Custom Install* and verify that the engine root path is correct.

On the *Getting Started* page, enable the following items.

* Compile the game code
* Compile the engine and asset pipeline
* Compile the Lumberyard Editor and tools
* Compile for Android devices

On the *Required Software* section, install and configure paths for the following items.

* Android Native Development (NDK)
* Android Software Development Kit (SDK) Tools
* Java SE Development Kit (JDK) - Make sure you use the [official Java SE 8 from Oracle](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) or [Java SE 8 OpenJDK reference implementation](https://jdk.java.net/java-se-ri/8). Other JDK releases won't work and you will have WAF errors during clean builds.

#### Step 3 - Enable OpenGL ES 3.X for Lumberyard

Close the editor and all of its componenets. Then, open *lumberyard_version\dev\AssetProcessorPlatformConfig.ini* in a text editor to make the following changes.

* Remove the semicolon before `es3=enabled` to enable it. Your development platform gets enabled automatically, so you don't have to enable `pc` or `osx_gl` unless they are required by your custom build schemes.

```
[Platforms]
;pc=enabled
es3=enabled
;ios=enabled
;osx_gl=enabled
```

#### Step 4 - Generate Android Studio Project

* Run **Project Configurator** to activate your current project.

* Using a command line app, navigate to *lumberyard_version\dev* folder.

* Run `lmbr_waf.bat configure` to generate your Android Studio project if you haven't already.

#### Step 5 - Generate Shaders for Release

* Build, deploy, and run your app on an Android device by using Lumberyard Editor's Deployment Tool Plugin. Run remote shader compiler if it doesn't launch automatically.

* In your app, explore every area in every level to ensure that all shader permutations required for the app are generated.

* Once you complete exploring all included levels, close the app.

* Embed the shader PAK files into your app or put them in a remotely accessible location where your app can access later. PAK files are located in *lumberyard_version\dev\Build\es3\game_project_name* folder. For more details, please refer to [this](https://docs.aws.amazon.com/lumberyard/latest/userguide/android-shaders-building.html).


#### Step 6 - Build

* Using a command line app or terminal, navigate to *lumberyard_version\dev* folder.

* Determine your build's target CPU architecture. (i.e armv8)

* Determine your build's type. (i.e profile, debug, release)

* Run the following command to build your APK. Make sure the CPU arch and build type is set correctly in the following command.

```
REM : replace 'armv8' and release 'words' if necessary.

lmbr_waf.bat -p all build_android_armv8_clang_release --package-projects-automatically=True
```

#### Step 7 - Upload to TestFairy

Once your APK is built, you can choose your favourite upload method to finalize distribution. Make sure the correct CPU architecture is set for the project binaries path.

To upload with **curl**, run the following command in *lumberyard_version\dev\BinAndroidCPU_ARCHClang* folder. Make sure your APK file name is set correctly.

```
curl https://upload.testfairy.com/api/upload -F api_key='your_api_key' -F file=@ProjectName.apk
```

Optionally, you can download and use [TestFairy command line uploader](https://github.com/testfairy/command-line-uploader) if you don't have **curl** installed.

## AWS Device Farm
### Android Instrumentation

With our open source Android Instrumentation runner, you can inspect individual test runs happening on AWS Device Farm through your TestFairy dashboard.

* Install [these](https://github.com/testfairy-blog/TestFairyInstrumentationExamples) to initialize the SDK in your test suite.

* Run your tests in Device Farm as **Instrumentation** to see it in action.

If you are new to AWS Device Farm, take a look at this introductory [blog post](https://blog.testfairy.com/device-farm-instrumentation-with-testfairy-android-sdk/) for a complete tutorial.
