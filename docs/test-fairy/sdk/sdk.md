---
id: sdk
title: SDK
sidebar_label: SDK
---
## Adding The Testfairy SDK To Your App
TestFairy's SDK takes your app to the next level.

Our tools help you understand how users really interact with your app.

We handle problems like crashes and on-screen error messages, and we even integrate with your current development workflow.

Some of our features include:

- Recording videos of how users interact with your apps
- Handling crashes and exceptions
- Sending logs to the TestFairy dashboard for later inspection
- Identifying and tagging users, for searching and custom reports
- Auto-Updates, to make sure your users are on the latest version

### Supported platforms

In order to add the TestFairy SDK to your app, please select your development platform from the following list:

- [Android](../Android/Integrating_Android_SDK.html)
- [iOS](../iOS_SDK/Integrating_iOS_SDK.html)
- [Cordova and PhoneGap](../Platforms/Cordova.html)
- [Ionic](../Platforms/Ionic.html)
- [ReactNative](../Platforms/React_Native.html)
- [Unity](../Platforms/Unity.html)
- [Xamarin](../Platforms/Xamarin.html)
- [Titanium](../Platforms/Titanium.html)
- [Adobe Air](../Platforms/Adobe_Air.html)
- [Nativescript](../Platforms/Nativescript.html)
- [Neptune Software](../Platforms/Neptune_Software.html)
- [Flutter](../Platforms/Flutter.html)

## Begin with options
TestFairy requires that you call `begin` in order to start recording your sessions. However, developers have the option to override the build settings to determine what is enabled during a session recording.

Here are some commonly used options:

* [Crash Reporting](#crash-reporting)
* [Video Recording](#video-recording)
* [Recorded Metrics](#recorded-metrics)
* [Max session Length](#max-session-length)

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;"  href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios-objc" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#ios-objc">
			<div>iOS</div>
		</a>
	</div>

	<h2>
		<a name="crash-reporting"></a>
		Crash Reporting
	</h2>
	<p>TestFairy provides a means of capturing and recording stack traces if your application crashes. Stack traces can be vital to understanding any underlying bugs in your app. However, some apps may want to disable TestFairy's crash handling. Invoke <b>enableCrashHandler</b> or <b>disableCrashHandler</b> before calling <b>begin</b>.</p>
	<p>Note that once the TestFairy crash handler has been enabled, it cannot be disabled unless the app is restarted.</p>
	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.enableCrashHandler();</b><br/>
				<b>TestFairy.disableCrashHandler();</b>
			</p>

			<h3>Code Example</h3>
			<p>In the following example, the TestFairy crash handler will be disabled.</p>
			<pre><code class="java">
import com.testfairy.TestFairy;

public class MyApplication extends Application {
	@Override
	public void onCreate() {
		super.onCreate();

		TestFairy.disableCrashHandler();
		TestFairy.begin(this, "&lt;app token&gt;");
	}
}
</code></pre>
		</div>

		<div data-w-tab="tab-ios-objc" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>[TestFairy enableCrashHandler];</b><br/>
				<b>[TestFairy disableCrashHandler];</b>
			</p>

			<h3>Code Example</h3>
			<p>In the following example, the TestFairy crash handler will be disabled.</p>
			<pre><code class="objectivec">
@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	[TestFairy disableCrashHandler];
	[TestFairy begin:@"&lt;app token&gt;"];
}
</code></pre>
		</div>

		<p>Your <b>app token</b> is available from your <a href="https://app.testfairy.com/settings#apptoken" target="_blank">account preferences</a> once logged in.
	</div>

	<div id="video-recording">
	<br>
	<br>
	<br>
	</div>
	<h2>
	Video Recording
	</h2>
	<p>TestFairy provides an option to enable or disable video recording, and to control the parameters of the recording. Invoke <b>disableVideo</b>, or <b>enableVideo</b> before <b>begin</b>.</p>
	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.disableVideo();</b><br/>
				<b>TestFairy.enableVideo("&lt;policy&gt;", "&lt;quality&gt;", &lt;frames per second&gt;);</b>
			</p>
			<p>Refer to the <a href="https://app.testfairy.com/reference/android/index.html">Class Reference</a> for more information on values for <b>policy</b> and <b>quality</b>.</p>

			<h3>Code Example</h3>
			<p>In the following example, video will only be recorded when wifi is available. A high quality video will be recorded every 2 seconds.</p>
			<pre><code class="java">
import com.testfairy.TestFairy;

public class MyApplication extends Application {
	@Override
	public void onCreate() {
		super.onCreate();

		TestFairy.enableVideo("wifi", "high", 2.0);
		TestFairy.begin(this, "&lt;app token&gt;");
	}
}
</code></pre>
		</div>

		<div data-w-tab="tab-ios-objc" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>[TestFairy disableVideo];</b><br/>
				<b>[TestFairy enableVideo:@"&lt;policy&gt;" quality:@"&lt;quality&gt;"  framesPerSecond:&lt;frames per second&gt;];</b>
			</p>
			<p>Refer to the <a href="https://app.testfairy.com/reference/ios/Classes/TestFairy.html">Class Reference</a> for more information on values for <b>policy</b> and <b>quality</b>.</p>

			<h3>Code Example</h3>
			<pre><code class="objectivec">
@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	[TestFairy enableVideo:@"wifi" quality:@"high" framesPerSecond:2.0];
	[TestFairy begin: @"&lt;app token&gt;"];
}
</code></pre>
		</div>

		<p>Your <b>app token</b> is available from your <a href="https://app.testfairy.com/settings#apptoken" target="_blank">account preferences</a> once logged in.
	</div>


	<h2>
	<a name="recorded-metrics"></a>
	Recorded Metrics
	</h2>
	<p>TestFairy can collect a number of different metrics from your app. Developers can choosed to override the metrics defined in their app's build settings.</p>
	<p>Developers can call <b>enableMetric</b> or <b>disableMetric</b> before invoking <b>begin</b> with the metric they wish to enable or disable recording.</p>
	<p>Note that any metric that is enabled or disabled will override the settings set in your app's build settings</p>
	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.enableMetric("&lt;metric&gt;");</b><br/>
				<b>TestFairy.disableMetric("&lt;metric&gt;");</b><br/>
			</p>
			<p>Refer to the <a href="https://app.testfairy.com/reference/android/index.html">Class Reference</a> for more information on which metric can be passed.</p>

			<h3>Code Example</h3>
			<p>In the following snippet, the CPU metric will be recorded, and the Memory metric wil not be recorded, regarless of what's set in the build settings.</p>
			<pre><code class="java">
import com.testfairy.TestFairy;

public class MyApplication extends Application {
	@Override
	public void onCreate() {
		super.onCreate();

		TestFairy.enableMetric("cpu");
		TestFairy.disableMetric("memory");
		TestFairy.begin(this, "&lt;app token&gt");
	}
}
</code></pre>
		</div>

		<div data-w-tab="tab-ios-objc" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>[TestFairy enableMetric:@"&lt;metric&gt;"];</b><br/>
				<b>[TestFairy disableMetric:@"&lt;metric&gt;"];</b>
			</p>
			<p>Refer to the <a href="https://app.testfairy.com/reference/ios/Classes/TestFairy.html">Class Reference</a> for more information on which metric can be passed.</p>

			<h3>Code Example</h3>
			<p>In the following snippet, the CPU metric will be recorded, and the Memory metric wil not be recorded, regardless of what's set in the build settings.</p>
			<pre><code class="objectivec">
@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	[TestFairy enableMetric:@"cpu"];
	[TestFairy disableMetric:@"memory"];
	[TestFairy begin: @"&lt;app token&gt"];
	// ...
}
</code></pre>
		</div>
		<p>Your <b>app token</b> is available from your <a href="https://app.testfairy.com/settings#apptoken" target="_blank">account preferences</a> once logged in.
	</div>


	<h2>
	<a name="max-session-length"></a>
	Max Session Length
	</h2>
	<p>TestFairy only records for a fixed period of time. Developers can override the maximum recording period by calling <b>setMaxSessionLength</b> before calling <b>begin</b>.</p>
	<p>Note that the value passed into this method must be less than or equal to the value defined in the build settings. A value larger than the one in the build settings will be ignored.</p>
	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.setMaxSessionLength(&lt;session length in seconds&gt;);</b>
			</p>

			<h3>Code Example</h3>
			<pre><code class="java">
import com.testfairy.TestFairy;

public class MyApplication extends Application {
	@Override
	public void onCreate() {
		super.onCreate();

		TestFairy.setMaxSessionLength(10 * 60); // Record for 10 minutes
		TestFairy.begin(this, "&lt;app token&gt;");
	}
}
</code></pre>
		</div>

		<div data-w-tab="tab-ios-objc" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>[TestFairy setMaxSessionLength:&lt;session length in seconds&gt;];</b>
			</p>

			<h3>Code Example</h3>
			<pre><code class="objectivec">
@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	[TestFairy setMaxSessionLength:(10 * 60)]; // Record for 10 minutes
	[TestFairy begin:@"&lt;app token&gt;"];
}
</code></pre>
		</div>
		<p>Your <b>app token</b> is available from your <a href="https://app.testfairy.com/settings#apptoken" target="_blank">account preferences</a> once logged in.
	</div>


	<h2>
	<a name="video-recording"></a>
	Feedback Form
	</h2>
	<p>TestFairy provides an option to enable or disable feedback collection. Invoke <b>disableFeedbackForm</b>, or <b>enableFeedbackForm</b> before <b>begin</b>.</p>
	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.disableFeedbackForm();</b><br/>
				<b>TestFairy.enableFeedbackForm("&lt;method&gt;");</b>
			</p>
			<p>Refer to the <a href="https://app.testfairy.com/reference/android/index.html">Class Reference</a> for more information on values for <b>method</b>.</p>

			<h3>Code Example</h3>
			<p>In the following example, feedback will be enabled when the device is shook.</p>
			<pre><code class="java">
import com.testfairy.TestFairy;

public class MyApplication extends Application {
	@Override
	public void onCreate() {
		super.onCreate();

		TestFairy.enableFeedbackForm("shake");
		TestFairy.begin(this, "&lt;app token&gt;");
	}
}
</code></pre>
		</div>

		<div data-w-tab="tab-ios-objc" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>[TestFairy disableFeedbackForm];</b><br/>
				<b>[TestFairy enableFeedbackForm:@"&lt;method&gt;"];</b>
			</p>
			<p>Refer to the <a href="https://app.testfairy.com/reference/ios/Classes/TestFairy.html">Class Reference</a> for more information on values for <b>method</b>.</p>

			<h3>Code Example</h3>
			<p>In the following example, feedback will be enabled when the user either shakes or takes a screenshot on the device.</p>
			<pre><code class="objectivec">
@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	[TestFairy enableFeedbackForm:@"shake|screenshot"];
	[TestFairy begin: @"&lt;app token&gt;"];
}
</code></pre>
		</div>

		<p>Your <b>app token</b> is available from your <a href="https://app.testfairy.com/settings#apptoken" target="_blank">account preferences</a> once logged in.
	</div>

</div>

## Hiding Sensitive Data
TestFairy allows developers to hide specific views from the recorded video. As a developer, you may choose to hide one or more views from the video for security and privacy reasons.

For example, you might want to prevent all information related to credit card data from appearing in the session.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;"  href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#ios">
			<div>iOS</div>
		</a>
		<a data-w-tab="tab-react-native" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#react-native">
			<div>React Native</div>
		</a>
		<a data-w-tab="tab-nativescript" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#nativescript">
			<div>Nativescript</div>
		</a>
		<a data-w-tab="tab-xamarin" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#xamarin">
			<div>Xamarin</div>
		</a>
	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
			<p>To hide a view from video, all you need to do is this:</p>
			<p>
				<b>TestFairy.hideView(Integer.valueOf(R.id.my_view));</b><br />
				or<br />
				<b>TestFairy.hideView(View myView);</b>
			</p>

			<p>
				Replace <b>R.id.my_view</b> with the identifier of the view you wish to hide. Please review the full example below:
			</p>

			<h3>Code Example</h3>
			<pre>
public class MyActivity extends Activity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.my_activity);

        TestFairy.hideView(findViewById(R.id.credit_card));
    }
}
			</pre>
		</div>

		<div data-w-tab="tab-ios" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				To hide a view from video, all you need to do is call the static instance method hideView in the TestFairy class:
			</p>

			<p>
				<b>UIView *view = ...</b><br />
				<b>[TestFairy hideView:view];</b><br />
			</p>

			<h3>Code Example</h3>
			<pre>
@interface MyViewController : UIViewController {
    IBOutlet UITextField *usernameView;
    IBOutlet UITextField *creditCardView;
    IBOutlet UITextField *cvvView;
}

@implementation MyViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    [TestFairy hideView:creditCardView];
    [TestFairy hideView:cvvView];
}
			</pre>
		</div>

		<div data-w-tab="tab-react-native" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				In order to hide views from your recorded session, you will need to pass a reference to a view to TestFairy. First, give the element to be hidden a ref attribute. For example:
			</p>

			<p>
				<b>&lt;Text ref="instructions"&gt;This will be hidden&lt;/Text&gt;</b>
			</p>

			<p>Next, in a component callback, such as componentDidMount, pass the reference ID back to TestFairy by invoking hideView.</p>

			<h3>Code Example</h3>
			<pre>
const TestFairy = require('react-native-testfairy');
var MyComponent = React.createClass({

    componentDidMount: function() {
        TestFairy.hideView(this.refs.instructions);
    },

    render: function() {
        return (&lt;Text ref="instructions"&gt;This will be hidden&lt;/Text&gt;);
    }
});
			</pre>
		</div>

		<div data-w-tab="tab-nativescript" class="w-tab-pane">
			<h3>Syntax</h3>
			<p><b>TestFairySDK.hideView(view);</b></p>

			<h3>Code Example</h3>
			<pre>
// in Nativescript
import { TestFairySDK } from 'nativescript-testfairy';

// in Javascript
var TestFairySDK = require('nativescript-testfairy').TestFairySDK;

TestFairySDK.hideView(view);
			</pre>
		</div>


		<div data-w-tab="tab-xamarin" class="w-tab-pane">
			<h3>Syntax</h3>
			<p><b>TestFairy.HideView (View view)</b> - on Android</p>
			<p><b>TestFairy.HideView (UIView view)</b> - on iOS</p>

			<h3>Code Example</h3>
			<pre>
// Be sure to import TestFairy
using TestFairyLib;

// On Android
View view = ...
TestFairy.HideView (view);

// On iOS
UIView view = ...
TestFairy.HideView (view);
			</pre>
		</div>

	</div>
</div>

### Sample video

Below is a sample screen taken from a demo video. On the left, you can see what the app normally looks like. On the right, there is a screenshot taken with the "Card Number" EditText hidden by testfairy-secure-viewid.

<div>
	<img style="float:left; border: none; box-shadow: none;" src="../../img/ios/hidden_views/iphone-with-fields.png" width="400" />
	<img style="float:left; border: none; box-shadow: none;" src="../../img/ios/hidden_views/iphone-no-fields.png" width="400" />
</div>

<br clear="both"/>

### Notes

* Hidden views are removed **before** sending video.
* You may hide multiple views.
* You may add the same view multiple times, no checks needed.

## Attaching Files To Sessions
TestFairy allows developers to attach files to sessions. As a developer, you can upload up to 5 files to a given session, with a maximum size of 15MB per file. Files must be local to the device.
Be sure to check the device logs if there were any problems uploading files. Only file extensions [.jpeg, .jpg, .png, .txt and .sqlite] are supported, others uploads will be ignored.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios">
			<div>iOS</div>
		</a>
	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
      <p>
        To attach a file to a session, all you need to do is call the static instance method attachFile in the TestFairy class:
      </p>
      <p>
        <b>File file = ...</b><br />
        <b>TestFairy.attachFile(file);</b><br />
      </p>
      <h3>Code Example</h3>
      <pre>
File file = new File("/path/to/file.txt");
TestFairy.attachFile(file);
      </pre>
		</div>

		<div data-w-tab="tab-ios" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				To attach a file to a session, all you need to do is call the static instance method attachFile in the TestFairy class:
			</p>
			<p>
				<b>NSURL *file = ...</b><br />
				<b>[TestFairy attachFile:file];</b><br />
			</p>

			<h3>Code Example</h3>
			<pre>
NSURL *file = [NSURL fileURLWithPath:"/path/to/file.txt"];
[TestFairy attachFile:file];
			</pre>
		</div>

	</div>
</div>

## Private Cloud Integration
The TestFairy enterprise suite can be installed on a private cloud on any AWS location in the US, Europe, Asia or South America. Servers can be protected by custom firewall rules allowing access only from your offices, according to your security policy.

With this installation, all the data is stored privately using your own resources.

# Set your endpoint

Once you've got your private cloud setup, make sure to get the URL endpoint your apps will direct all of its data towards. This URL must be passed into the SDK before the `begin` method is called.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios">
			<div>iOS</div>
		</a>
		<a data-w-tab="tab-cordova" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#cordova">
			<div>Cordova</div>
		</a>
		<a data-w-tab="tab-react-native" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#react-native">
			<div>React Native</div>
		</a>
		<a data-w-tab="tab-nativescript" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#nativescript">
			<div>Nativescript</div>
		</a>
		<a data-w-tab="tab-xamarin" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#xamarin">
			<div>Xamarin</div>
		</a>
		<a data-w-tab="tab-unity" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#unity">
			<div>Unity</div>
		</a>
		<a data-w-tab="tab-adobe-air" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#adobe-air">
			<div>Adobe Air</div>
		</a>
		<a data-w-tab="tab-titanium" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#titanium">
			<div>Titanium</div>
		</a>
	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
      <p>
        <b>TestFairy.setServerEndpoint("&lt;your private cloud url here&gt;");</b><br />
      </p>
      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import com.testfairy.TestFairy;

TestFairy.setServerEndpoint("my-subdomain.testfairy.com");
TestFairy.begin(context, "&lt;your app token here&gt;");
      </pre>
		</div>

		<div data-w-tab="tab-ios" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
        <b>[TestFairy setServerEndpoint:@"&lt;your private cloud url here&gt;"];</b><br />
      </p>
      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
#import "TestFairy.h"

[TestFairy setServerEndpoint:@"my-subdomain.testfairy.com"];
[TestFairy begin:@"&lt;your app token here&gt;"];
      </pre>
		</div>

		<div data-w-tab="tab-cordova" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
        <b>TestFairy.setServerEndpoint("&lt;your private cloud url here&gt;");</b><br />
      </p>
      <h3>Code Example</h3>
      <pre>
TestFairy.setServerEndpoint("my-subdomain.testfairy.com");
TestFairy.begin("&lt;your app token here&gt;");
      </pre>
		</div>

		<div data-w-tab="tab-react-native" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
        <b>TestFairy.setServerEndpoint("&lt;your private cloud url here&gt;");</b><br />
      </p>
      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
const TestFairy = require('react-native-testfairy');

TestFairy.setServerEndpoint("my-subdomain.testfairy.com");
TestFairy.begin("&lt;your app token here&gt;");
      </pre>
		</div>


		<div data-w-tab="tab-nativescript" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
        <b>TestFairySDK.setServerEndpoint("&lt;your private cloud url here&gt;");</b><br />
      </p>
      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import { TestFairySDK } from 'nativescript-testfairy';

TestFairySDK.setServerEndpoint("my-subdomain.testfairy.com");
TestFairySDK.begin("&lt;your app token here&gt;");
      </pre>
		</div>

		<div data-w-tab="tab-xamarin" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
        <b>TestFairy.SetServerEndpoint ("&lt;your private cloud url here&gt;");</b><br />
      </p>
      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
using TestFairyLib;

TestFairy.SetServerEndpoint ("my-subdomain.testfairy.com");
TestFairy.Begin ("&lt;your app token here&gt;");
      </pre>
		</div>

		<div data-w-tab="tab-unity" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
        <b>TestFairy.setServerEndpoint("&lt;your private cloud url here&gt;");</b><br />
      </p>
      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
using TestFairyUnity;

TestFairy.setServerEndpoint("my-subdomain.testfairy.com");
TestFairy.begin("&lt;your app token here&gt;");
      </pre>
		</div>

		<div data-w-tab="tab-adobe-air" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
        <b>AirTestFairy.setServerEndpoint("&lt;your private cloud url here&gt;");</b><br />
      </p>
      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import com.testfairy.AirTestFairy;

AirTestFairy.setServerEndpoint("my-subdomain.testfairy.com");
AirTestFairy.begin("&lt;your app token here&gt;");
      </pre>
		</div>

		<div data-w-tab="tab-titanium" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
        <b>TiTestFairy.setServerEndpoint("&lt;your private cloud url here&gt;");</b><br />
      </p>
      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
var TiTestFairy = require('com.testfairy.titestfairy');

TiTestFairy.setServerEndpoint("my-subdomain.testfairy.com");
TiTestFairy.begin("&lt;your app token here&gt;");
      </pre>
		</div>

	</div>
</div>

## Identifying Your Users
TestFairy allows the developer to correlate sessions to app-specific information such as users, server-sessions or events.
This is useful in cases where sessions are anonymous and or when sessions are related to server activities that are critical to understanding test behavior.

Furthermore, TestFairy enables the identification of users with traits such as name, email or phone number. These traits will later be available for the developer to search upon, or review when looking at a specific session recording.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios">
			<div>iOS</div>
		</a>
		<a data-w-tab="tab-cordova" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#cordova">
			<div>Cordova</div>
		</a>
		<a data-w-tab="tab-react-native" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#react-native">
			<div>React Native</div>
		</a>
		<a data-w-tab="tab-nativescript" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#nativescript">
			<div>Nativescript</div>
		</a>
		<a data-w-tab="tab-xamarin" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#xamarin">
			<div>Xamarin</div>
		</a>
		<a data-w-tab="tab-unity" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#unity">
			<div>Unity</div>
		</a>
		<a data-w-tab="tab-adobe-air" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#adobe-air">
			<div>Adobe Air</div>
		</a>
		<a data-w-tab="tab-titanium" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#titanium">
			<div>Titanium</div>
		</a>
	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.setUserId("&lt;userId&gt;");</b><br />
      </p>

			<p>Where <b>userId</b> is a string representing an association to your backend. We recommend passing values such as email, phone number, or user id that your app may use. This value may not be nil, and is searchable via API and web search.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import com.testfairy.TestFairy;

TestFairy.setUserId("john@example.com");
      </pre>
		</div>

		<div data-w-tab="tab-ios" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>[TestFairy setUserId:@"&lt;userId&gt;"];</b><br />
			</p>

			<p>Where <b>userId</b> is a string representing an association to your backend. We recommend passing values such as email, phone number, or user id that your app may use. This value may not be nil, and is searchable via API and web search.</p>

			<h3>Code Example</h3>
			<pre>
// Be sure to import TestFairy
#import "TestFairy.h"

[TestFairy setUserId:@"john@example.com"];
			</pre>
		</div>

		<div data-w-tab="tab-cordova" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.setUserId("&lt;userId&gt;");</b><br />
      </p>

			<p>Where <b>userId</b> is a string representing an association to your backend. We recommend passing values such as email, phone number, or user id that your app may use. This value may not be nil, and is searchable via API and web search.</p>

      <h3>Code Example</h3>
      <pre>
TestFairy.setUserId("john@example.com");
      </pre>
		</div>

		<div data-w-tab="tab-react-native" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.setUserId("&lt;userId&gt;");</b><br />
      </p>

			<p>Where <b>userId</b> is a string representing an association to your backend. We recommend passing values such as email, phone number, or user id that your app may use. This value may not be nil, and is searchable via API and web search.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
const TestFairy = require('react-native-testfairy');

TestFairy.setUserId("john@example.com");
      </pre>
		</div>


		<div data-w-tab="tab-nativescript" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairySDK.setUserId("&lt;userId&gt;");</b><br />
      </p>

			<p>Where <b>userId</b> is a string representing an association to your backend. We recommend passing values such as email, phone number, or user id that your app may use. This value may not be nil, and is searchable via API and web search.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import { TestFairySDK } from 'nativescript-testfairy';

TestFairySDK.setUserId("john@example.com");
      </pre>
		</div>

		<div data-w-tab="tab-xamarin" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.SetUserId ("&lt;userId&gt;");</b><br />
      </p>

			<p>Where <b>userId</b> is a string representing an association to your backend. We recommend passing values such as email, phone number, or user id that your app may use. This value may not be nil, and is searchable via API and web search.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
using TestFairyLib;

TestFairy.SetUserId ("john@example.com");
      </pre>
		</div>

		<div data-w-tab="tab-unity" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.setUserId("&lt;userId&gt;");</b><br />
      </p>

			<p>Where <b>userId</b> is a string representing an association to your backend. We recommend passing values such as email, phone number, or user id that your app may use. This value may not be nil, and is searchable via API and web search.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
using TestFairyUnity;

TestFairy.setUserId("john@example.com");
      </pre>
		</div>

		<div data-w-tab="tab-adobe-air" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>AirTestFairy.setUserId("&lt;userId&gt;");</b><br />
      </p>

			<p>Where <b>userId</b> is a string representing an association to your backend. We recommend passing values such as email, phone number, or user id that your app may use. This value may not be nil, and is searchable via API and web search.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import com.testfairy.AirTestFairy;

AirTestFairy.setUserId("john@example.com");
      </pre>
		</div>

		<div data-w-tab="tab-titanium" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TiTestFairy.setUserId("&lt;userId&gt;");</b><br />
      </p>

			<p>Where <b>userId</b> is a string representing an association to your backend. We recommend passing values such as email, phone number, or user id that your app may use. This value may not be nil, and is searchable via API and web search.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
var TiTestFairy = require('com.testfairy.titestfairy');

TiTestFairy.setUserId("john@example.com");
      </pre>
		</div>

	</div>
</div>

### Notes

1. `setUserId:` may be called many times.
2. You may call `setUserId` before or after `begin`.

## Session Attributes
TestFairy can collect additional information from your session, which can help you generate better insights.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios">
			<div>iOS</div>
		</a>
		<a data-w-tab="tab-cordova" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#cordova">
			<div>Cordova</div>
		</a>
		<a data-w-tab="tab-react-native" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#react-native">
			<div>React Native</div>
		</a>
		<a data-w-tab="tab-nativescript" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#nativescript">
			<div>Nativescript</div>
		</a>
		<a data-w-tab="tab-xamarin" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#xamarin">
			<div>Xamarin</div>
		</a>
		<a data-w-tab="tab-unity" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#unity">
			<div>Unity</div>
		</a>
		<a data-w-tab="tab-adobe-air" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#adobe-air">
			<div>Adobe Air</div>
		</a>
		<a data-w-tab="tab-titanium" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#titanium">
			<div>Titanium</div>
		</a>
	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.setAttribute("&lt;key&gt;", "&lt;value&gt;");</b><br />
      </p>

			<p>The first value is a string <b>key</b> to help you search for the attribute in your session. The second parameter, <b>value</b>, is any string value for the attribute associated with the session. Neither value can be nil. These attributes are available later in the session recording page, are available via API, and are searchable.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import com.testfairy.TestFairy;

TestFairy.setAttribute("payment-method","free");
TestFairy.setAttribute("account-type","driver");
TestFairy.setAttribute("phone","+1-672-154-5109");
TestFairy.setAttribute("level","20");

      </pre>
		</div>

		<div data-w-tab="tab-ios" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>[TestFairy setAttribute:@"&lt;key&gt;" withValue:@"&lt;value&gt;"];</b><br />
      </p>

			<p>The first value is a string <b>key</b> to help you search for the attribute in your session. The second parameter, <b>value</b>, is any string value for the attribute associated with the session. Neither value can be nil. These attributes are available later in the session recording page, are available via API, and are searchable.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
#import "TestFairy.h"

[TestFairy setAttribute:@"name" withValue:@"John Snow"];
[TestFairy setAttribute:@"phone" withValue:@"+672-14-5109"];
[TestFairy setAttribute:@"age" withValue:@"20"];
[TestFairy setAttribute:@"favorite_color" withValue:@"blue"];
      </pre>
		</div>

		<div data-w-tab="tab-cordova" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.setAttribute("&lt;key&gt;", "&lt;value&gt;");</b><br />
      </p>

			<p>The first value is a string <b>key</b> to help you search for the attribute in your session. The second parameter, <b>value</b>, is any string value for the attribute associated with the session. Neither value can be nil. These attributes are available later in the session recording page, are available via API, and are searchable.</p>

      <h3>Code Example</h3>
      <pre>
TestFairy.setAttribute("name","John Snow");
TestFairy.setAttribute("phone","+672-14-5109");
TestFairy.setAttribute("age","20");
TestFairy.setAttribute("favorite_color","blue");
      </pre>
		</div>

		<div data-w-tab="tab-react-native" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.setAttribute("&lt;key&gt;", "&lt;value&gt;");</b><br />
      </p>

			<p>The first value is a string <b>key</b> to help you search for the attribute in your session. The second parameter, <b>value</b>, is any string value for the attribute associated with the session. Neither value can be nil. These attributes are available later in the session recording page, are available via API, and are searchable.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
const TestFairy = require('react-native-testfairy');

TestFairy.setAttribute("name","John Snow");
TestFairy.setAttribute("phone","+672-14-5109");
TestFairy.setAttribute("age","20");
TestFairy.setAttribute("favorite_color","blue");
      </pre>
		</div>


		<div data-w-tab="tab-nativescript" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairySDK.setAttribute("&lt;key&gt;", "&lt;value&gt;");</b><br />
      </p>

			<p>The first value is a string <b>key</b> to help you search for the attribute in your session. The second parameter, <b>value</b>, is any string value for the attribute associated with the session. Neither value can be nil. These attributes are available later in the session recording page, are available via API, and are searchable.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import { TestFairySDK } from 'nativescript-testfairy';

TestFairySDK.setAttribute("name","John Snow");
TestFairySDK.setAttribute("phone","+672-14-5109");
TestFairySDK.setAttribute("age","20");
TestFairySDK.setAttribute("favorite_color","blue");
      </pre>
		</div>

		<div data-w-tab="tab-xamarin" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.SetAttribute ("&lt;key&gt;", "&lt;value&gt;");</b><br />
      </p>

			<p>The first value is a string <b>key</b> to help you search for the attribute in your session. The second parameter, <b>value</b>, is any string value for the attribute associated with the session. Neither value can be nil. These attributes are available later in the session recording page, are available via API, and are searchable.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
using TestFairyLib;

TestFairy.SetAttribute ("name","John Snow");
TestFairy.SetAttribute ("phone","+672-14-5109");
TestFairy.SetAttribute ("age","20");
TestFairy.SetAttribute ("favorite_color","blue");
      </pre>
		</div>

		<div data-w-tab="tab-unity" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.setAttribute("&lt;key&gt;", "&lt;value&gt;");</b><br />
      </p>

			<p>The first value is a string <b>key</b> to help you search for the attribute in your session. The second parameter, <b>value</b>, is any string value for the attribute associated with the session. Neither value can be nil. These attributes are available later in the session recording page, are available via API, and are searchable.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
using TestFairyUnity;

TestFairy.setAttribute("name","John Snow");
TestFairy.setAttribute("phone","+672-14-5109");
TestFairy.setAttribute("age","20");
TestFairy.setAttribute("favorite_color","blue");
      </pre>
		</div>

		<div data-w-tab="tab-adobe-air" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>AirTestFairy.setAttribute("&lt;key&gt;", "&lt;value&gt;");</b><br />
      </p>

			<p>The first value is a string <b>key</b> to help you search for the attribute in your session. The second parameter, <b>value</b>, is any string value for the attribute associated with the session. Neither value can be nil. These attributes are available later in the session recording page, are available via API, and are searchable.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import com.testfairy.AirTestFairy;

AirTestFairy.setAttribute("name","John Snow");
AirTestFairy.setAttribute("phone","+672-14-5109");
AirTestFairy.setAttribute("age","20");
AirTestFairy.setAttribute("favorite_color","blue");
      </pre>
		</div>

		<div data-w-tab="tab-titanium" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TiTestFairy.setAttribute("&lt;key&gt;", "&lt;value&gt;");</b><br />
      </p>

			<p>The first value is a string <b>key</b> to help you search for the attribute in your session. The second parameter, <b>value</b>, is any string value for the attribute associated with the session. Neither value can be nil. These attributes are available later in the session recording page, are available via API, and are searchable.</p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
var TiTestFairy = require('com.testfairy.titestfairy');

TiTestFairy.setAttribute("name","John Snow");
TiTestFairy.setAttribute("phone","+672-14-5109");
TiTestFairy.setAttribute("age","20");
TiTestFairy.setAttribute("favorite_color","blue");
      </pre>
		</div>

	</div>
</div>

Adding these lines will mark this session with the values above, so when you review the recording, you have more information about the person running the app.

### Notes

1. `setAttribute` may be called many times.
2. You may call `setAttribute` before or after `begin`.
3. You can only store a maximum of 64 keys. The keys can be a maximum of 64 characters. The values can have a maximum of 1000 characters.

## Remote Logging
TestFairy allows developers to log items with a session, without logging to the console output. In some cases, there are work arounds that allow you to wrap the TestFairy remote logging method in a way that will both log to the console and to the session.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios">
			<div>iOS - Objective C</div>
		</a>
		<a data-w-tab="tab-ios-swift" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-swift">
			<div>iOS - Swift</div>
		</a>
		<a data-w-tab="tab-cordova" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#cordova">
			<div>Cordova</div>
		</a>
		<a data-w-tab="tab-react-native" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#react-native">
			<div>React Native</div>
		</a>
		<a data-w-tab="tab-nativescript" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#nativescript">
			<div>Nativescript</div>
		</a>
		<a data-w-tab="tab-xamarin" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#xamarin">
			<div>Xamarin</div>
		</a>
		<a data-w-tab="tab-unity" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#unity">
			<div>Unity</div>
		</a>
		<a data-w-tab="tab-adobe-air" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#adobe-air">
			<div>Adobe Air</div>
		</a>
		<a data-w-tab="tab-titanium" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#titanium">
			<div>Titanium</div>
		</a>
	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.log("&lt;tag&gt;", "&lt;message&gt;");</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import com.testfairy.TestFairy;

TestFairy.log("Tag", "Hello, TestFairy!");
      </pre>
		</div>

		<div data-w-tab="tab-ios" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TFLog(@"&lt;message with format&gt;", &lt;arguments&gt;);</b><br />
				<b>[TestFairy log:@"&lt;message&gt;"];</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
#import "TestFairy.h"

TFLog(@"Hello, %@", @"TestFairy!");
[TestFairy log:@"Hello, TestFairy!"];
      </pre>

			<p>We recommend sending all calls to <code>NSLog</code> to TestFairy so you can continue to use <code>NSLog</code> and see all your log statements in your session.</p>
			<p>To enable sending logs to TestFairy, you will have to redefine <code>NSLog</code> using a macro with the following lines (This macro allows you to continue using NSLog in your code, while also adding the logs to the  matching session in TestFairy).</p>

			<p><strong>Changing your Prefix Header</strong></p>
			<pre><code class=" hljs cs"><span class="hljs-preprocessor">#import "TestFairy.h"</span>
<span class="hljs-preprocessor">#<span class="hljs-keyword">define</span> NSLog(s, ...) do { NSLog(s, ##__VA_ARGS__); TFLog(s, ##__VA_ARGS__); } while (0)</span>
</code></pre>
			<ol>
			<li>Either add the above line to a global header in your project, accessible to every class file</li>
			<li>Update or create a Prefix Header (.pch) for your project. If you do not have a PCH file in your project, you can follow the steps in the next section</li>
			</ol>
			<p><strong>Creating a new Prefix Header</strong></p>
			<p>If your project doesn’t already include a Prefix Header (.pch), follow these steps to add it:<br></p>
			<ol>
				<li>Create a new file under iOS &gt; Other &gt; PCH File.</li>
				<li>Name your file “PCH file”.</li>
				<li>Add these two lines of code to the file:<br>
				<code>#import "TestFairy.h"<br/>
				#define NSLog(s, ...) do { NSLog(s, ##__VA_ARGS__); TFLog(s, ##__VA_ARGS__); } while (0)</code></li>
				<li><p>From the Project Navigator, select your project and the corresponding target.</p></li>
				<li><p>Project &gt; Build Settings &gt; Search: "Prefix Header".</p></li>
				<li><p>Under "Apple LLVM 7.0" you will get the Prefix Header key.</p></li>
				<li><p>Type the path of the file, for example: "$(SRCROOT)/$(PROJECT_NAME)/ProjectName-Prefix.pch". Please note that your file may be at a different location.</p></li>
				<li><p>Make sure the option "Precompile Prefix Header" is set to YES.</p></li>
				<li><p>Clean your project, and rebuild.</p></li>
			</ol>
		</div>

		<div data-w-tab="tab-ios-swift" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.log("&lt;message&gt;")</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
TestFairy.log("Hello, TestFairy!")
      </pre>

			<p>We recommend wrapping all <b>print</b> statements with a custom method, which will output to both the console and to TestFairy sessions. One suggestion we have is to create a new file named <code>TestFairyLog.swift</code> in your source path, and add the following to the contents of the file:</p>
<pre><code class="swift">//
//  TestFairyLog.swift
//
//  Copyright © TestFairy. All rights reserved.
//

import Foundation

public func print(_ items: Any..., separator: String = " ", terminator: String = "\n") {
	let output = items.map { "\($0)" }.joined(separator: separator)
	TestFairy.log(output)
	Swift.print(output, terminator: terminator)
}
</code></pre>
			<p>This will print any output to both the Xcode console, and to the active session on TestFairy.</p>
		</div>

		<div data-w-tab="tab-cordova" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.log("&lt;message&gt;");</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
TestFairy.log("Hello, TestFairy!");
      </pre>

			<p>We recommend wrapping all <b>log</b> statements with a custom method, which will output to both the console and to TestFairy sessions. One suggestion we have is to add a method that looks like this:</p>
			<pre>
var testfairyConsoleLog = console.log;
console.log = function(message) {
	testfairyConsoleLog(message);
	TestFairy.log(message);
}
			</pre>
		</div>

		<div data-w-tab="tab-react-native" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.log("&lt;message&gt;");</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
const TestFairy = require('react-native-testfairy');

TestFairy.log("Hello, TestFairy!");
      </pre>

			<p>We recommend wrapping all <b>log</b> statements with a custom method, which will output to both the console and to TestFairy sessions. One suggestion we have is to add a method that looks like this:</p>
			<pre>
var testfairyConsoleLog = console.log;
console.log = function(message) {
	testfairyConsoleLog(message);
	TestFairy.log(message);
}
			</pre>
		</div>


		<div data-w-tab="tab-nativescript" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairySDK.log("&lt;message&gt;");</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import { TestFairySDK } from 'nativescript-testfairy';

TestFairySDK.log("Hello, TestFairy!");
      </pre>

			<p>We recommend wrapping all <b>log</b> statements with a custom method, which will output to both the console and to TestFairy sessions. One suggestion we have is to add a method that looks like this:</p>
			<pre>
var testfairyConsoleLog = console.log;
console.log = function(message) {
	testfairyConsoleLog(message);
	TestFairySDK.log(message);
}
			</pre>
		</div>

		<div data-w-tab="tab-xamarin" class="w-tab-pane">
			<p>We recommend wrapping all <b>TFLog</b> statements with a custom method, which will output to both the console and to TestFairy sessions. One suggestion we have is to add a method that looks like this:</p>

      <h3>Code Example</h3>

      <pre>
// Be sure to import TestFairy
using TestFairyLib;

public static void Log(string format, params object[] arg)
{
    using (var nsFormat = new NSString(string.Format(format, arg)))
    {
        CFunctions.TFLog(nsFormat.Handle, "");
        Console.WriteLine(string.Format(format, arg));
    }
}
      </pre>

			<p>Now, you can log statements using this call:</p>
			<pre>
Log("Hello {0}", "World");
			</pre>
		</div>

		<div data-w-tab="tab-unity" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.log("&lt;message&gt;");</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
using TestFairyUnity;

TestFairy.log("Hello, TestFairy!");
      </pre>
		</div>

		<div data-w-tab="tab-adobe-air" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>AirTestFairy.log("&lt;message&gt;");</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import com.testfairy.AirTestFairy;

AirTestFairy.log("Hello, TestFairy!");
      </pre>
		</div>

		<div data-w-tab="tab-titanium" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TiTestFairy.log("&lt;message&gt;");</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
var TiTestFairy = require('com.testfairy.titestfairy');

TiTestFairy.log("Hello, TestFairy!");
      </pre>
		</div>

	</div>
</div>

## Exception Logging
TestFairy allows developers to log up to 5 exceptions or errors to a given session. **Note**: This does not mark the sessions as crashed, it will only log the exception or error to the session.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios">
			<div>iOS - Objective C</div>
		</a>
		<a data-w-tab="tab-ios-swift" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-swift">
			<div>iOS - Swift</div>
		</a>
		<a data-w-tab="tab-cordova" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#cordova">
			<div>Cordova</div>
		</a>
		<a data-w-tab="tab-react-native" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#react-native">
			<div>React Native</div>
		</a>
		<a data-w-tab="tab-nativescript" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#nativescript">
			<div>Nativescript</div>
		</a>
	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.logThrowable(&lt;throwable exception&gt;);</b><br />
			</p>

			<h3>Code Example</h3>
			<pre>
// Be sure to import TestFairy
import com.testfairy.TestFairy;

TestFairy.logThrowable(new Throwable("Some Message"));
			</pre>
		</div>

		<div data-w-tab="tab-ios" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>[TestFairy logError:&lt;NSError&gt;];</b><br />
				<b>[TestFairy logError:&lt;NSError&gt; stacktrace:&lt;NSArray&lt;NSString&gt;&gt;];</b><br />
			</p>

			<h3>Code Example</h3>
			<pre>
// Be sure to import TestFairy
#import "TestFairy.h"

[TestFairy logError:[NSError errorWithDomain:@"com.your.domain" code:-1 userInfo:@{NSLocalizedDescriptionKey: @"Some Message"}]];
			</pre>
		</div>

		<div data-w-tab="tab-ios-swift" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.logError(&lt;NSError&gt;)</b><br />
				<b>TestFairy.logError(&lt;NSError&gt;, stacktrace:&lt;[String]&gt;)</b><br />
			</p>

			<h3>Code Example</h3>
			<pre>
let error = NSError(domain: "com.your.domain", code: -1, userInfo: [NSLocalizedDescriptionKey : "Some Message"])
TestFairy.logError(error)
			</pre>
		</div>


		<div data-w-tab="tab-cordova" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.logException(&lt;Error&gt;);</b><br />
			</p>

			<h3>Code Example</h3>
			<pre>
var error = new Error("Some Message");
TestFairy.logException(error);
			</pre>

			<p>We recommend adding a listener to the <b>window</b> to capture <b>error</b> statements, which will automatically send the exception to TestFairy sessions. One suggestion we have is to add a method that looks like this:</p>
			<pre>
window.addEventListener("error", function(e) {
	TestFairy.logException(e);
});
			</pre>
		</div>

		<div data-w-tab="tab-react-native" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.logException(&lt;Error&gt;);</b><br />
			</p>

			<h3>Code Example</h3>
			<pre>
// Be sure to import TestFairy
const TestFairy = require('react-native-testfairy');

var error = new Error("Some Message");
TestFairy.logException(error);
			</pre>

			<p>We recommend replacing the <b>Global Handler</b> with a custom method, which will automatically send the exception to TestFairy sessions. One suggestion we have is to add a method that looks like this:</p>
			<pre>
var ErrorUtils = require('ErrorUtils');
var originalGlobalHandler = ErrorUtils.getGlobalHandler();
ErrorUtils.setGlobalHandler((error, isFatal) => {
	TestFairy.logException(error);
	originalGlobalHandler.handleException(error, isFatal);
});
			</pre>
		</div>


		<div data-w-tab="tab-nativescript" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>TestFairySDK.logException(&lt;Error&gt;);</b><br />
			</p>

			<h3>Code Example</h3>
			<pre>
// Be sure to import TestFairy
import { TestFairySDK } from 'nativescript-testfairy';

var error = new Error("Some Message");
TestFairySDK.logException(error);
			</pre>

			<p>We recommend adding a listener to the <b>window</b> to capture <b>error</b> statements, which will automatically send the exception to TestFairy sessions. One suggestion we have is to add a method that looks like this:</p>
			<pre>
window.addEventListener("error", function(e) {
	TestFairy.logException(e);
});
			</pre>
		</div>

	</div>
</div>

## Network Logging
With TestFairy, you can log all your network requests. This gives you an easy way to monitor network access your app is doing.


![Log Network](/img/sdk/logHttp.png)


<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios-objc" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-objc">
			<div>iOS - Objective C</div>
		</a>
		<a data-w-tab="tab-ios-swift" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-swift">
			<div>iOS - Swift</div>
		</a>
		<a data-w-tab="tab-ios-react-native" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#react-native">
			<div>React Native</div>
		</a>
	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.addNetworkEvent(URI uri, String method, int code, long startTimeMillis, long endTimeMillis, long requestSize, long responseSize, String errorMessage);</b><br />
			</p>

			<h3>Code Example</h3>
			<p>If you are using <b>OkHttp</b> or <b>Retrofit</b> all you need to do is add CustomHttpInterceptor to your client:</p>
			<pre>
// Be sure to import TestFairy
import com.testfairy.TestFairy;

public class CustomHttpInterceptor implements Interceptor {
	@Override
	public Response intercept(@NonNull Chain chain) throws IOException {

		Request request = chain.request();
		long startTimeMillis = System.currentTimeMillis();
		Long requestSize = request.body() != null ? request.body().contentLength() : 0;
		Response response;
		try {
			response = chain.proceed(request);
		} catch (IOException e) {
			long endTimeMillis = System.currentTimeMillis();
			TestFairy.addNetworkEvent(request.url().uri(), request.method(), -1, startTimeMillis, endTimeMillis, requestSize, -1, e.getMessage());
			throw e;
		}

		long endTimeMillis = System.currentTimeMillis();
		long responseSize = response.body() != null ? response.body().contentLength() : 0;
		TestFairy.addNetworkEvent(request.url().uri(), request.method(), response.code(), startTimeMillis, endTimeMillis, requestSize, responseSize, null);
		return response;
	}
}


OkHttpClient client = new OkHttpClient.Builder()
	.addInterceptor(new CustomHttpInterceptor())
	.build();
			</pre>
		</div>

		<div data-w-tab="tab-ios-objc" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>[TestFairy addNetwork:(NSURLSessionTask *)task error:(NSError *)error]</b><br />
			</p>

			<h3>Code Example</h3>
			<p>If you are using <b>NSURLConnection</b> all you need to do is add callback to your request at the beginning of the request and at the end.</p>
			<p>Note: If you have <b>AFNetworking</b> added to your project, network requests will be automatically captured when enabled in your build settings.</p>
			<pre>
// Be sure to import TestFairy
#import "TestFairy.h"

__block NSURLSessionTask *task = [[NSURLSession sharedSession] dataTaskWithURL:url completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
	// ...
	[TestFairy addNetwork:task error:error];
}];
[TestFairy addNetwork:task error:nil];
[task resume];
			</pre>
		</div>

		<div data-w-tab="tab-ios-swift" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.addNetwork(&lt;URLSessionTask&gt;, error:&lt;NSError&gt;)</b><br />
			</p>

			<h3>Code Example</h3>
			<p>If you are using <b>URLConnection</b> all you need to do is add callback to your request at the beginning of the request and at the end:</p>
			<pre>
var task: URLSessionTask? = nil
task = URLSession.shared.dataTask(with: URL(string:"")!) { (data, response, error) in
	TestFairy.addNetwork(task, error: error)
}
TestFairy.addNetwork(task, error: nil)
task?.resume()
			</pre>

			<p>With <b>Alamofire</b>, it's even easier:</p>
			<pre>
import Alamofire

NotificationCenter.default.addObserver(forName: Request.didResume, object: nil, queue: nil) { (notification) in
	let info = notification.userInfo
	let request = info?["org.alamofire.notification.key.request"] as! Request
	request.tasks.forEach { TestFairy.addNetwork($0, error: nil) }
}

NotificationCenter.default.addObserver(forName: Request.didComplete, object: nil, queue: nil) { (notification) in
	let info = notification.userInfo
	let request = info?["org.alamofire.notification.key.request"] as! Request
	request.tasks.forEach { TestFairy.addNetwork($0, error: nil) }
}
			</pre>
		</div>

		<div data-w-tab="tab-ios-react-native" class="w-tab-pane">
			<p>TestFairy supports network logging for Fetch API. Simply call the following method to start capturing network calls.</p>
			<pre>
// Capture network logs
TestFairy.enableNetworkLogging(window);

// Capture network logs including http headers and content
TestFairy.enableNetworkLogging(window, { includeHeaders: true, includeBodies: true });

// Disable network logging
TestFairy.disableNetworkLogging(window);
			</pre>
		</div>

	</div>
</div>

## Adding Events
Events are used to provide insights on the how testers use your apps.

These can help you keep track of when a tester reaches key points in your app, such as visiting the in-app store.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;"  href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios-objc" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#ios-objc">
			<div>iOS</div>
		</a>
		<a data-w-tab="tab-react-native" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#react-native">
			<div>React Native</div>
		</a>

	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
			<p>To add an event to your timeline, all you need to do is this:</p>
			<p>
				<b>TestFairy.addEvent("&lt;event name&gt;");</b>
			</p>

			<h3>Code Example</h3>
			<pre>
public class MyActivity extends Activity {
	private void onPurchaseComplete() {
		TestFairy.addEvent("Purchase OK");
	}
}
			</pre>
		</div>

		<div data-w-tab="tab-ios-objc" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
			<p>To add an event to your timeline, all you need to do is this:</p>
			<p>
				<b>[TestFairy addEvent:@"&lt;event name&gt;"];</b>
			</p>

			<h3>Code Example</h3>
			<pre>
@implementation ViewController
- (void)viewDidLoad {
	[super viewDidLoad];
	[TestFairy addEvent:@"Purchase OK"];
	//...
}
// ...
@nd
			</pre>
		</div>

		<div data-w-tab="tab-react-native" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>To add an event to your timeline, all you need to do is this:</p>
			<p>
				<b>TestFairy.addEvent("&lt;event name&gt;");</b>
			</p>

			<h3>Code Example</h3>
			<pre>
const TestFairy = require('react-native-testfairy');
var MyComponent = React.createClass({
    componentDidMount: function() {
        TestFairy.addEvent("Purchase OK");
    }
});
			</pre>
		</div>

	</div>
</div>

By adding the line above, a new column in your [Build Coverage Report](http://docs.testfairy.com/Getting_Started/Testing_Reports.html) page will appear, titled according to the event (in this case "Purchase OK").

Please remember that events are rendered in a table, consider using indicative names and keep them short.

## Customizing feedback dialog
In-app feedback works out of the box, allowing users to report bugs by shaking their device.

This feature is customizable and allows you to launch the feedback from from a button inside your UI or any other gesture, or change the way the feature works.

If you already called `begin` and have a session, you can simply use `showFeedbackForm` to launch the form yourself.

Otherwise, you can utilize `showFeedbackForm` anywhere in your app to launch the form without a session. The user will be presented with possible actions to take such as capturing a new screenshot or screen recording.

Here are a few methods that can help you customize the feedback behaviour:

- [`setBrowserUrl`](#setBrowserUrl): Open a web browser instead of a built-in dialog (eg, a questionnaire).
- [`setEmailFieldVisible`](#setEmailFieldVisible): Whether or not email input text should be displayed.
- [`setEmailMandatory`](#setEmailFieldVisible): Whether or not people have to identify themselves when submitting feedback.
- [`setDefaultText`](#setDefaultText): Set the initial text content of the feedback form to standardize reported feedbacks with submission guidelines.
- [`setCallback`](#setCallback): Get notified when a feedback has been sent.
- `setRecordVideoButtonVisible`: Set whether set record video button is visible.
- `setTakeScreenshotButtonVisible`: Set whether screenshot button is visible.
- [`setFeedbackInterceptor`](#setFeedbackInterceptor): Intercept sent feedbacks to modify their message, email or attached screenshot on the fly.
- [`setFeedbackVerifier`](#setFeedbackVerifier): Intercept sent feedbacks to accept or reject them based on custom logic.
- [`setFeedbackFormFields`](#setFeedbackFormFields): Create a customized Feedback form.

#### <a name="setBrowserUrl"></a>setBrowserUrl

You can setBrowserUrl, so TestFairy will open your own url for user feedback (or a questionnaire etc. ).

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
    <div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
        <a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
            <div>Android</div>
        </a>
    </div>
    <div class="docs-tabs-content w-tab-content">
        <div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
            <h3>Code Example</h3>
            <pre>
FeedbackOptions feedbackOptions = new FeedbackOptions.Builder()
    .setBrowserUrl("https://www.myfeedbackform.com")
    .build();
TestFairy.setFeedbackOptions(feedbackOptions);
            </pre>
        </div>
    </div>
</div>

#### <a name="setEmailFieldVisible"></a>setEmailFieldVisible / setEmailMandatory

You can decide whether the email field is visible or not, and whether the email is mandatory or not.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
    <div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
        <a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
            <div>Android</div>
        </a>
        <a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-objc">
            <div>iOS</div>
        </a>
    </div>
    <div class="docs-tabs-content w-tab-content">
        <div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
            <h3>Code Example</h3>
            <pre>
FeedbackOptions feedbackOptions = new FeedbackOptions.Builder()
    .setEmailFieldVisible(true)
    .setEmailMandatory(true)
    .build();
TestFairy.setFeedbackOptions(feedbackOptions);
            </pre>
        </div>
        <div data-w-tab="tab-ios" class="w-tab-pane">
            <h3>Code Example</h3>
            <pre>
[TestFairy setTestFairyFeedbackOptions:[TestFairyFeedbackOptions createWithBlock:^(TestFairyFeedbackOptionsBuilder *builder) {
    builder.isEmailMandatory = YES;
    builder.isEmailVisible = YES;
}]];
            </pre>
        </div>
    </div>
</div>


#### <a name="setDefaultText"></a>setDefaultText

In order to change the default text that users see in the feedback form textarea, please use the following:

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
    <div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
        <a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
            <div>Android</div>
        </a>
        <a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-objc">
            <div>iOS</div>
        </a>
    </div>
    <div class="docs-tabs-content w-tab-content">
        <div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
            <h3>Code Example</h3>
            <pre>
FeedbackOptions feedbackOptions = new FeedbackOptions.Builder()
    .setDefaultText("Tested on the following device:\n" +
                        "\n\n" +
                        "Steps to reproduce:\n" +
                        "1.\n\n" +
                        "2.\n\n" +
                        "3.\n\n" +
                        "Actual Result:\n" +
                        "Expected Result:\n")
    .build();
TestFairy.setFeedbackOptions(feedbackOptions);
            </pre>
        </div>
        <div data-w-tab="tab-ios" class="w-tab-pane">
            <h3>Code Example</h3>
            <pre>
[TestFairy setTestFairyFeedbackOptions:[TestFairyFeedbackOptions createWithBlock:^(TestFairyFeedbackOptionsBuilder *builder) {
    builder.defaultText = @"Tested on the following device:\n" +
                        "\n\n" +
                        "Steps to reproduce:\n" +
                        "1.\n\n" +
                        "2.\n\n" +
                        "3.\n\n" +
                        "Actual Result:\n" +
                        "Expected Result:\n";
}]];
            </pre>
        </div>
    </div>
</div>

#### <a name="setCallback"></a>setCallback

You can get a callback to your application if a feedback was sent, cancelled or failed.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
    <div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
        <a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
            <div>Android</div>
        </a>
    </div>
    <div class="docs-tabs-content w-tab-content">
        <div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
            <h3>Code Example</h3>
            <pre>
FeedbackOptions feedbackOptions = new FeedbackOptions.Builder()
    .setEmailFieldVisible(true)
    .setEmailMandatory(true)
    .setCallback(new FeedbackOptions.Callback() {
        @Override
        public void onFeedbackSent(FeedbackContent content) {
            Toast.makeText(MyActivity.this, "onFeedbackSent text = " + content.getEmail() + ", " + content.getText() , Toast.LENGTH_LONG).show();
        }

        @Override
        public void onFeedbackCancelled() {
            Toast.makeText(MyActivity.this, "onFeedbackCancelled", Toast.LENGTH_LONG).show();
        }

        @Override
        public void onFeedbackFailed(int reason, FeedbackContent content) {
            Toast.makeText(MyActivity.this, "onFeedbackFailed text = " + content.getEmail() + ", " + content.getText() , Toast.LENGTH_LONG).show();
        }
    })
    .build();

TestFairy.setFeedbackOptions(feedbackOptions);
            </pre>
        </div>
    </div>
</div>

#### <a name="setFeedbackInterceptor"></a>setFeedbackInterceptor

A submitted feedback's content can be inspected with custom interceptors. Intereptors can modify the inspected feedback's message, user email or attached bitmap. This way, it is possible to add extra text to the submitted message such as ids from issue trackers and meta data relevant to current context the feedback is submitted from.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
    <div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
        <a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
            <div>Android</div>
        </a>
        <a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-objc">
            <div>iOS</div>
        </a>
    </div>
    <div class="docs-tabs-content w-tab-content">
        <div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
            <h3>Code Example</h3>
            <pre>
FeedbackOptions feedbackOptions = new FeedbackOptions.Builder()
    .setFeedbackInterceptor(new FeedbackOptions.FeedbackInterceptor() {
        @Override
        public FeedbackContent intercept(FeedbackContent feedbackContent) {
            String exampleText = "Issue: " + generateIssueId() + "\n";

            return new FeedbackContent(
                exampleText + feedbackContent.getText(),
                feedbackContent.getEmail(),
                feedbackContent.getTimestamp(),
                feedbackContent.getBitmap()
            );
        }
    })
    .build();

TestFairy.setFeedbackOptions(feedbackOptions);
            </pre>
        </div>
        <div data-w-tab="tab-ios" class="w-tab-pane">
            <h3>Code Example</h3>
            <pre>
[TestFairy setTestFairyFeedbackOptions:[TestFairyFeedbackOptions createWithBlock:^(TestFairyFeedbackOptionsBuilder *builder) {
    builder.interceptor = ^TestFairyFeedbackContent *(TestFairyFeedbackContent *content) {
        NSString *exampleText = [NSString stringWithFormat:@"Issue: %@", [self generateIssueId]];
        return [[TestFairyFeedbackContent alloc] initWith:[NSString stringWithFormat:@"%@\n%@", exampleText, content.text]
                                                    email:content.email
                                                timestamp:content.timestamp
                                                    bitmap:content.bitmap];
    };
}]];
            </pre>
        </div>
    </div>
</div>

#### <a name="setFeedbackVerifier"></a>setFeedbackVerifier

It is also possible to define custom feedback verification logic by providing a verifier implementation.

First, implement the following interface with your custom logic. We provide an example but you can choose your own rules for the allowed feedbacks.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
    <div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
        <a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
            <div>Android</div>
        </a>
        <a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-objc">
            <div>iOS</div>
        </a>
    </div>
    <div class="docs-tabs-content w-tab-content">
        <div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
            <h3>Code Example</h3>
            <pre>
public class MyFeedbackVerifier implements FeedbackVerifier {
    private String lastError = null;

    @Override
    public boolean verifyFeedback(FeedbackContent content) {
        lastError = null;

        if (content.getEmail() == null || content.getEmail().equals("")) {
            lastError = "Missing email address";
            return false;
        }

        if (content.getEmail().endsWith("@example.com") || content.getEmail().endsWith("@gmail.com")) {
            lastError = "Email address cannot end with @example.com or @gmail.com";
            return false;
        }

        if (content.getText().trim().length() < 10) {
            lastError = "Feedback body must be at least 10 characters long, please write something..";
            return false;
        }

        Map<String, String> attributes = content.getAttributes();
        if (attributes.containsValue("IMPORTANT_CREDENTIALS")) {
            // Example security measure to reject sensitive data coming from custom feedback form fields
            lastError = "Please remove your password from the submitted feedback.";
            return false;
        }

        return true;
    }

    @Override
    public String getVerificationFailedMessage() {
        return lastError;
    }
}
            </pre>

            <p>Then call the SDK with your verifier.</p>

            <pre>
TestFairy.setFeedbackVerifier(new MyFeedbackVerifier());
            </pre>
        </div>
        <div data-w-tab="tab-ios" class="w-tab-pane">
            <h3>Code Example</h3>
            <pre>
#import <TestFairy.h>
@interface MyFeedbackVerifier: NSObject<TestFairyFeedbackVerifier>
@end

@implementation MyFeedbackVerifier {
    NSString *_lastError;
}

- (BOOL)verifyFeedback:(TestFairyFeedbackContent *)content {
    if (content.email == nil) {
        _lastError = @"Missing email address";
        return NO;
    }

    return YES;
}

- (NSString *)getVerificationFailedMessage {
    return _lastError;
}

@end
            </pre>

            <p>Then call the SDK with your verifier.</p>

            <pre>
[TestFairy setTestFairyFeedbackOptions:[TestFairyFeedbackOptions createWithBlock:^(TestFairyFeedbackOptionsBuilder *builder) {
    builder.verifier = [[MyFeedbackVerifier alloc] init];
}]];
            </pre>
        </div>
    </div>
</div>

#### <a name="setFeedbackFormFields"></a>setFeedbackFormFields

Do you want to add custom input fields to the submitted feedbacks?

TestFairy SDK is transitioning to a new layout system which provides a fully customizable feedback form experience with its `FeedbackOptions` API.

Warning : Support for custom fields is still in its early stages. All class names and method signatures may change during development.

This API consists of an interface to adapt any native view to the form, and some built-in implementations of it for basic field types such as text areas and pickers.

To get started, copy the code below and modify it according to your needs.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
    <div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
        <a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
            <div>Android</div>
        </a>
        <a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-objc">
            <div>iOS</div>
        </a>
        <a data-w-tab="tab-flutter" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#flutter">
            <div>Flutter</div>
        </a>
    </div>
    <div class="docs-tabs-content w-tab-content">
        <div data-w-tab="tab-ios" class="w-tab-pane">
            <h3>Code Example</h3>
            <pre>
NSArray *formFields = @[
    [[TestFairyStringFeedbackFormField alloc] initWithAttribute:@":userId" // :userId is built-in for emails
                                                             label:@"Email "
                                                       placeholder:nil
                                                      defaultValue:@""],
[[TestFairyTextAreaFeedbackFormField alloc] initWithAttribute:@":text" // :text is built-in for feedback messages
                                                     placeholder:@"Describe your feedback"
                                                    defaultValue:@""],
[[TestFairySelectFeedbackFormField alloc] initWithAttribute:@"city"
                                                      label:@"Cities"
                                                     values:@{
                                                            @"London": @"LON", // humanReadableName: machineReadableName
                                                            @"Paris": @"PAR",
                                                            @"Berlin": @"BER",
                                                            @"Los Angeles": @"LA",
                                                            @"Beijing": @"BEI",
                                                     }
                                                defaultValue:@"Paris"],
];

[TestFairy setTestFairyFeedbackOptions:[TestFairyFeedbackOptions createWithBlock:^(TestFairyFeedbackOptionsBuilder *builder) {
    builder.feedbackFormFields = formFields;
}]];
            </pre>

            <p>Here is the form generated in the example above.</p>
            <img src ="../../img/ios/custom-feedbacks/custom-feedbacks-1.png" height=572 alt="alt">
            <img src ="../../img/ios/custom-feedbacks/custom-feedbacks-2.png" height=572 alt="alt"><br/>
            <img src ="../../img/ios/custom-feedbacks/custom-feedbacks-3.png" height=572 alt="alt">
            <img src ="../../img/ios/custom-feedbacks/custom-feedbacks-4.png" height=572 alt="alt"><br/>

            <h3>Built-in Form Elements</h3>
            <p><code>feedbackFormFields</code> expects a list of <code>TestFairyFeedbackFormField</code> objects, which is a protocol any app developer can implement to inject custom made views into the form hierarchy.</p>
            <p>However, the SDK provides a few, ready to use elements listed below:</p>

            <h4>TestFairyStringFeedbackFormField</h4>
            <p>A single line text input. Mainly used for emails, phone numbers and similar identifiers.</p>

            <h4>TestFairyTextAreaFeedbackFormField</h4>
            <p>A multi line text input. Mainly used for feedback messages and Q/A sections.</p>

            <h4>TestFairySelectFeedbackFormField</h4>
            <p>A single choice picker for choosing from a set of predefined values. Mainly used for area codes, currencies or questions with single, definite answers.</p>
        </div>
        <div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
            <h3>Code Example</h3>
            <pre>
Map<String, String> cities = new HashMap<>();
// cities.put(humanReadableName, machineReadableName)
cities.put("London", "LON");
cities.put("Paris", "PAR");
cities.put("Berlin", "BER");
cities.put("Los Angeles", "LA");
cities.put("Beijing", "BEI");

List<FeedbackFormField> fields = new ArrayList<>();
fields.add(new StringFeedbackFormField(":userId", "Email", "")); // :userId is built-in for emails
fields.add(new TextAreaFeedbackFormField(":text", "Your message", "")); // :text is built-in for feedback messages
fields.add(new SelectFeedbackFormField("city", "City", cities, "Paris" /*default value*/)); // A custom select field

TestFairy.setFeedbackOptions(
    new FeedbackOptions.Builder()
        .setFeedbackFormFields(fields)
        .build()
);
            </pre>

            <p>Here is the form generated in the example above.</p>
            <img src ="../../img/android/custom-feedbacks/custom-feedbacks-1.jpg" alt="alt">
            <img src ="../../img/android/custom-feedbacks/custom-feedbacks-2.jpg" alt="alt">
            <img src ="../../img/android/custom-feedbacks/custom-feedbacks-3.jpg" alt="alt"><br/>
            <img src ="../../img/android/custom-feedbacks/custom-feedbacks-4.jpg" alt="alt">
            <img src ="../../img/android/custom-feedbacks/custom-feedbacks-5.jpg" alt="alt">
            <img src ="../../img/android/custom-feedbacks/custom-feedbacks-6.jpg" alt="alt"><br/>

            <h3>Built-in Form Elements</h3>
            <p><code>setFeedbackFormFields</code> expects a list of <code>FeedbackFormField</code> objects, which is an interface any app developer can implement to inject custom made views into the form hierarchy.</p>
            <p>However, the SDK provides a few, ready to use elements listed below:</p>

            <h4>StringFeedbackFormField</h4>
            <p>A single line text input. Mainly used for emails, phone numbers and similar identifiers.</p>

            <h4>TextAreaFeedbackFormField</h4>
            <p>A multi line text input. Mainly used for feedback messages and Q/A sections.</p>

            <h4>SelectFeedbackFormField</h4>
            <p>A single choice picker for choosing from a set of predefined values. Mainly used for area codes, currencies or questions with single, definite answers.</p>
        </div>
        <div data-w-tab="tab-flutter" class="w-tab-pane w--tab-active">
            <h3>Code Example</h3>
            <pre>
  final List<FeedbackFormField> fields = <FeedbackFormField>[
    StringFeedbackFormField('fullname', 'Your name', ''),
    TextAreaFeedbackFormField('bio', 'Bio', 'Tell us about yourself'),
    SelectFeedbackFormField(
        'country',
        'Country',
        <String, String>{'Turkey': '+90', 'Canada': '+1', 'Israel': '+972'},
        'Canada')
  ];

  await TestFairy.setFeedbackOptions(feedbackFormFields: fields);
  await TestFairy.showFeedbackForm();
            </pre>

            <p>Here is the form generated in the example above.</p>
            <img src ="../../img/android/custom-feedbacks/custom-feedbacks-1.jpg" alt="alt">
            <img src ="../../img/android/custom-feedbacks/custom-feedbacks-2.jpg" alt="alt">
            <img src ="../../img/android/custom-feedbacks/custom-feedbacks-3.jpg" alt="alt"><br/>
            <img src ="../../img/ios/custom-feedbacks/custom-feedbacks-1.png" height=572 alt="alt">
            <img src ="../../img/ios/custom-feedbacks/custom-feedbacks-2.png" height=572 alt="alt">
            <img src ="../../img/ios/custom-feedbacks/custom-feedbacks-3.png" height=572 alt="alt"><br/>

            <h3>Built-in Form Elements</h3>
            <p><code>setFeedbackFormFields</code> expects a list of <code>FeedbackFormField</code> objects. The SDK provides a few, ready to use elements listed below:</p>

            <h4>StringFeedbackFormField</h4>
            <p>A single line text input. Mainly used for emails, phone numbers and similar identifiers.</p>

            <h4>TextAreaFeedbackFormField</h4>
            <p>A multi line text input. Mainly used for feedback messages and Q/A sections.</p>

            <h4>SelectFeedbackFormField</h4>
            <p>A single choice picker for choosing from a set of predefined values. Mainly used for area codes, currencies or questions with single, definite answers.</p>
        </div>
    </div>
</div>

### Automatic Email Detection

The feedback form uses following heuristics to determine how to fill its email field.

- If you provide an email address to `setUserId`, it will be automatically detected by the form.
- If you set an attribute via `setAttribute` with a key of `"email"`, the form will make use of it.
- If the user sends a feedback with a valid email address, it will also be saved for later use in case rules above cannot detect any other addresses.

## Getting Feedback
User/Testers feedback can contain vital and highly relevant information when testing an app.

It can improve your app user experience and make it easier for your testers to communicate with you their thoughts on how to make your app better.

### Using in-app feedback as is
TestFairy provides an easy way to collect this feedback.

If you [added the TestFairy SDK](https://docs.testfairy.com/SDK/Adding_The_SDK_To_Your_App.html) to your app, then all you need to do is enable the **In-App Bug Reporting** feature in your build settings in the TestFairy dashboard and you can start collection feedbacks from your users with `"shake to report"`:

![alt](../../img/sdk/enable_feedback.png)

When your users or testers shake their device, they will be prompted to report a feedback.

This feedback will be added to the existing session of the app they are currently running.

All feedback includes a screenshot, device information, submitter email, and text comments added. the feedback is added to the event timeline so you can easily find it.

### Customizing In-app feedback

In case you wish to use the TestFairy feedback form without having the user shake their device, you can invoke the feedback form programmatically and call the method at your choice. You can do it on any gesture, button click in your app, if the user opened the help menu, or even got an error message theyr didn't expect.

Please note that if you choose to programmatically invoke the feedback form, it will be shown regardless if the in-app feedback is disabled in your build settings.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios">
			<div>iOS</div>
		</a>
		<a data-w-tab="tab-cordova" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#cordova">
			<div>Cordova</div>
		</a>
		<a data-w-tab="tab-react-native" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#react-native">
			<div>React Native</div>
		</a>
		<a data-w-tab="tab-nativescript" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#nativescript">
			<div>Nativescript</div>
		</a>
		<a data-w-tab="tab-xamarin" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#xamarin">
			<div>Xamarin</div>
		</a>
		<a data-w-tab="tab-unity" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#unity">
			<div>Unity</div>
		</a>
		<a data-w-tab="tab-adobe-air" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#adobe-air">
			<div>Adobe Air</div>
		</a>
	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.showFeedbackForm();</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import com.testfairy.TestFairy;

// Can be invoked on a button press
// or after your app passes a given page
TestFairy.showFeedbackForm();
      </pre>
     <h4>Note:</h4> For advanced customization look <a href="https://docs.testfairy.com/reference/android/com/testfairy/FeedbackOptions.Builder.html">here </a>.


		</div>

		<div data-w-tab="tab-ios" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>[TestFairy pushFeedbackController];</b><br />
			</p>

			<h3>Code Example</h3>
			<pre>
// Be sure to import TestFairy
#import "TestFairy.h"

// Can be invoked on a button press
// or after your app passes a given page
[TestFairy pushFeedbackController];
			</pre>


			<h4>Note</h4>
			<p>On iOS, if the <b>In-App Bug Reporting</b> feature is enabled, the feedback form will also be shown when the tester takes a screenshot.</p>

			You can also choose to hide the user email field in the feedback form using the
			<a href="https://docs.testfairy.com/reference/ios/Classes/TestFairy.html#//api/name/setFeedbackEmailVisible:">setFeedbackEmailVisible </a> class.
		</div>

		<div data-w-tab="tab-cordova" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.pushFeedbackController();</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Can be invoked on a button press
// or after your app passes a given page
TestFairy.pushFeedbackController();
      </pre>
		</div>

		<div data-w-tab="tab-react-native" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.pushFeedbackController();</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
const TestFairy = require('react-native-testfairy');

// Can be invoked on a button press
// or after your app passes a given page
TestFairy.pushFeedbackController();
      </pre>
		</div>


		<div data-w-tab="tab-nativescript" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairySDK.pushFeedbackController();</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import { TestFairySDK } from 'nativescript-testfairy';

// Can be invoked on a button press
// or after your app passes a given page
TestFairySDK.pushFeedbackController();
      </pre>
		</div>

		<div data-w-tab="tab-xamarin" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.SetUserId ("&lt;userId&gt;");</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
using TestFairyLib;

// Can be invoked on a button press
// or after your app passes a given page
TestFairy.PushFeedbackController();
      </pre>
		</div>

		<div data-w-tab="tab-unity" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>TestFairy.pushFeedbackController();</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
using TestFairyUnity;

// Can be invoked on a button press
// or after your app passes a given page
TestFairy.pushFeedbackController();
      </pre>
		</div>

		<div data-w-tab="tab-adobe-air" class="w-tab-pane">
			<h3>Syntax</h3>
      <p>
				<b>AirTestFairy.pushFeedbackController();</b><br />
      </p>

      <h3>Code Example</h3>
      <pre>
// Be sure to import TestFairy
import com.testfairy.AirTestFairy;

// Can be invoked on a button press
// or after your app passes a given page
AirTestFairy.pushFeedbackController();
      </pre>
		</div>

	</div>
</div>

## Using map locations
The TestFairy SDK does not require location permissions and does track location out of the box.

In cases where developers whish to send location information to TestFairy, they will need to add location permissions to their app, and use the code below to call TestFairy.updateLocation. After doing that, location will be presented on a map as part of the session page.

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;"  href="#android">
			<div>Android</div>
		</a>
		<a data-w-tab="tab-ios-objc" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#ios-objc">
			<div>iOS - Objective C</div>
		</a>
	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
		<p>To record locations, you must first add the correct permissions to your application. Depending on your application's needs, you may want to add one or both of the following permissions to your <code>AndroidManifest.xml</code></p>
		<pre><code class=" hljs xml"><span class="hljs-tag">&lt;<span class="hljs-title">uses-permission</span> <span class="hljs-attribute">android:name</span>=<span class="hljs-value">"android.permission.ACCESS_COARSE_LOCATION"</span> /&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">uses-permission</span> <span class="hljs-attribute">android:name</span>=<span class="hljs-value">"android.permission.ACCESS_FINE_LOCATION"</span> /&gt;</span>
</code></pre>

			<h3>Syntax</h3>
			<p>
				<b>
				TestFairy.updateLocation(android.location.Location location)
				</b>
			</p>

			<h3>Code Example</h3>
<pre><code class=" hljs java"><span class="hljs-keyword">import</span> android.content.Context;
<span class="hljs-keyword">import</span> android.location.Criteria;
<span class="hljs-keyword">import</span> android.location.Location;
<span class="hljs-keyword">import</span> android.location.LocationListener;
<span class="hljs-keyword">import</span> android.location.LocationManager;
<span class="hljs-keyword">import</span> android.support.v7.app.AppCompatActivity;
<span class="hljs-keyword">import</span> android.os.Bundle;

<span class="hljs-keyword">import</span> com.testfairy.TestFairy;

<span class="hljs-keyword">public</span> <span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">MainActivity</span> <span class="hljs-keyword">extends</span> <span class="hljs-title">AppCompatActivity</span> <span class="hljs-keyword">implements</span> <span class="hljs-title">LocationListener</span> {</span>

    <span class="hljs-keyword">private</span> LocationManager locationManager;

    <span class="hljs-annotation">@Override</span>
    <span class="hljs-keyword">protected</span> <span class="hljs-keyword">void</span> <span class="hljs-title">onCreate</span>(Bundle savedInstanceState) {
        <span class="hljs-keyword">super</span>.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        <span class="hljs-comment">// Get the location manager</span>
        locationManager = (LocationManager) getSystemService(Context.LOCATION_SERVICE);

        Criteria criteria = <span class="hljs-keyword">new</span> Criteria();
        String provider = locationManager.getBestProvider(criteria, <span class="hljs-keyword">false</span>);
        Location location = locationManager.getLastKnownLocation(provider);

        <span class="hljs-comment">// Initialize the location fields</span>
        <span class="hljs-keyword">if</span> (location != <span class="hljs-keyword">null</span>) {
            onLocationChanged(location);
        }
    }

    <span class="hljs-annotation">@Override</span>
    <span class="hljs-keyword">public</span> <span class="hljs-keyword">void</span> <span class="hljs-title">onLocationChanged</span>(Location location) {
        TestFairy.updateLocation(location);
    }
}
</code></pre>
		</div>

		<div data-w-tab="tab-ios-objc" class="w-tab-pane">
			<p>To record locations, all you need to do is call the static instance method <code>updateLocation</code> in the <code>TestFairy</code> class, passing in a collection of <code>CLLocations</code>.</p>
			<h3>Syntax</h3>
			<p>
				<b>
				NSArray&lt;CLLocation *&gt; *locations = ... <br/>
				[TestFairy updateLocation:locations];
				</b>
			</p>

			<h3>Code Example</h3>
<pre><code class=" hljs objectivec"><span class="hljs-preprocessor">#import <span class="hljs-title">"TestFairy.h"</span></span>

<span class="hljs-class"><span class="hljs-keyword">@interface</span> <span class="hljs-title">NewRunViewController</span>: <span class="hljs-title">UIViewController</span> &lt;<span class="hljs-title">CLLocationManagerDelegate</span>&gt;</span>
- (<span class="hljs-keyword">void</span>)viewDidLoad
{
    [<span class="hljs-keyword">super</span> viewDidLoad];

    <span class="hljs-keyword">self</span><span class="hljs-variable">.locationManager</span> = [[CLLocationManager alloc] init];
    <span class="hljs-keyword">self</span><span class="hljs-variable">.locationManager</span><span class="hljs-variable">.delegate</span> = <span class="hljs-keyword">self</span>;
    <span class="hljs-keyword">self</span><span class="hljs-variable">.locationManager</span><span class="hljs-variable">.distanceFilter</span> = kCLDistanceFilterNone;
    <span class="hljs-keyword">self</span><span class="hljs-variable">.locationManager</span><span class="hljs-variable">.desiredAccuracy</span> = kCLLocationAccuracyBest;
    [<span class="hljs-keyword">self</span><span class="hljs-variable">.locationManager</span> startUpdatingLocation];
}

...

-(<span class="hljs-keyword">void</span>)locationManager:(CLLocationManager *)manager didUpdateLocations:(<span class="hljs-built_in">NSArray</span>&lt;CLLocation *&gt; *)locations {
    [TestFairy updateLocation:locations];
}

<span class="hljs-keyword">@end</span>
</code></pre>
		</div>

	</div>


</div>

## TestFairy Crash Handler
In order to use the TestFairy SDK as a crash handler without any other TestFairy feature, please use the code samples below.


<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
    <div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
      <a data-w-tab="tab-android" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#android">
        <div>Android</div>
      </a>
      <a data-w-tab="tab-ios-objc" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-objc">
        <div>iOS-Objc-C</div>
      </a>
      <a data-w-tab="tab-ios-swift" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-swift">
        <div>iOS-Swift</div>
      </a>
    </div>


    <div class="docs-tabs-content w-tab-content">
      <div data-w-tab="tab-android" class="w-tab-pane w--tab-active">
        <h3>Syntax</h3>
        <p>
          <b>TestFairy.installCrashHandler(this, "APP_TOKEN");</b>
        </p>

        <h3>Code Example</h3>

        <pre>
import com.testfairy.TestFairy;

public class MyApplication extends Application {
	@Override
	public void onCreate() {
		super.onCreate();

		TestFairy.installCrashHandler(this, "APP_TOKEN");
	}
}
	</pre>
      </div>
      <div data-w-tab="tab-ios-objc" class="w-tab-pane">
        <h3>Syntax</h3>
        <p>
          <b>[TestFairy installCrashHandler:@"APP_TOKEN"];</b>
        </p>

        <h3>Code Example</h3>

        <pre>
@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	[TestFairy installCrashHandler:@"APP_TOKEN"];
}
	</pre>
      </div>
      <div data-w-tab="tab-ios-swift" class="w-tab-pane">
        <h3>Syntax</h3>
        <p>
          <b>TestFairy.installCrashHandler("APP_TOKEN")</b>
        </p>

        <h3>Code Example</h3>

        <pre>
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey : Any]? = nil) -> Bool {
		TestFairy.installCrashHandler("APP_TOKEN");
	}

}
	</pre>
      </div>


    </div>
  </div>

## How to Test the Crash Handler
<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
		<a data-w-tab="tab-ios-objc" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#ios-objc"><div>iOS - ObjC</div></a>
		<a data-w-tab="tab-ios-swift" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#ios-swift"><div>iOS - Swift</div></a>
	</div>

	<h2>Causing a crash</h2>
	<p>Want to try out TestFairy's world class crash handler? Use the TestFairy library to invoke a crash, in your app, and see the stacktrace in your app's session.</p>
	<div class="docs-tabs-content w-tab-content">

		<div data-w-tab="tab-ios-objc" class="w-tab-pane w--tab-active">
			<h3>Syntax</h3>
			<p>
				<b>[TestFairy crash];</b>
			</p>
			<p><strong>Note</strong>: Available starting iOS SDK version 1.19.8

			<h3>Code Example</h3>
			<pre><code class="objectivec">
#import "ViewController.h"
#import "TestFairy.h"

@implementation ViewController
- (void)viewDidLoad {
    [super viewDidLoad];

    UIButton* button = [UIButton buttonWithType:UIButtonTypeRoundedRect];
    button.frame = CGRectMake(50, 50, 100, 30);
    [button setTitle:@"Crash" forState:UIControlStateNormal];
    [button addTarget:self action:@selector(crashApp:) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
}

- (IBAction)crashApp:(id)sender {
    [TestFairy crash];
}

@end
</code></pre>
		</div>

		<div data-w-tab="tab-ios-swift" class="w-tab-pane">
			<h3>Syntax</h3>
			<p>
				<b>TestFairy.crash()</b>
			</p>
			<p><strong>Note</strong>: Available starting iOS SDK version 1.19.8

			<h3>Code Example</h3>
			<pre><code class="swift">
import UIKit

class ViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()

        let button = UIButton(type: .roundedRect)
        button.frame = CGRect(x: 50, y: 50, width: 100, height: 30)
        button.setTitle("Crash", for: [])
        button.addTarget(self, action: #selector(self.crashApp(_:)), for: .touchUpInside)
        view.addSubview(button)
    }

    @IBAction func crashApp(_ sender: AnyObject) {
        TestFairy.crash()
    }
}
</code></pre>
		</div>

	</div>
</div>

## Supported Platforms
Along with native Android and iOS development, TestFairy supports a number of other platforms. See below for a list of each supported platform, and the supported features on each platform.

## Cordova / PhoneGap
 * [Adding the SDK to your App](../Platforms/Cordova.html)
 * [Private Cloud Integration](Private_Cloud_Integration.html#cordova)
 * [Identifying your Users](Identifying_Your_Users.html#cordova)
 * [Session Attributes](Session_Attributes.html#cordova)
 * [Remote Logging](Remote_Logging.html#cordova)

## Ionic
 * [Adding the SDK to your App](../Platforms/Ionic.html)
 * [Private Cloud Integration](Private_Cloud_Integration.html#cordova)
 * [Identifying your Users](Identifying_Your_Users.html#cordova)
 * [Session Attributes](Session_Attributes.html#cordova)
 * [Remote Logging](Remote_Logging.html#cordova)

## React Native
 * [Adding the SDK to your App](../Platforms/React_Native.html)
 * [Hiding Sensitive Data](Hiding_Sensitive_Data.html#react-native)
 * [Private Cloud Integration](Private_Cloud_Integration.html#react-native)
 * [Identifying your Users](Identifying_Your_Users.html#react-native)
 * [Session Attributes](Session_Attributes.html#react-native)
 * [Remote Logging](Remote_Logging.html#react-native)

## Nativescript
 * [Adding the SDK to your App](../Platforms/Nativescript.html)
 * [Hiding Sensitive Data](Hiding_Sensitive_Data.html#nativescript)
 * [Private Cloud Integration](Private_Cloud_Integration.html#nativescript)
 * [Identifying your Users](Identifying_Your_Users.html#nativescript)
 * [Session Attributes](Session_Attributes.html#nativescript)
 * [Remote Logging](Remote_Logging.html#nativescript)

## Unity
 * [Adding the SDK to your App](../Platforms/Unity.html)
 * [Private Cloud Integration](Private_Cloud_Integration.html#unity)
 * [Identifying your Users](Identifying_Your_Users.html#unity)
 * [Session Attributes](Session_Attributes.html#unity)
 * [Remote Logging](Remote_Logging.html#unity)

## Xamarin
 * [Adding the SDK to your App](../Platforms/Xamarin.html)
 * [Hiding Sensitive Data](Hiding_Sensitive_Data.html#xamarin)
 * [Private Cloud Integration](Private_Cloud_Integration.html#xamarin)
 * [Identifying your Users](Identifying_Your_Users.html#xamarin)
 * [Session Attributes](Session_Attributes.html#xamarin)
 * [Remote Logging](Remote_Logging.html#xamarin)

## Adobe Air
 * [Adding the SDK to your App](../Platforms/Adobe_Air.html)
 * [Private Cloud Integration](Private_Cloud_Integration.html#adobe-air)
 * [Identifying your Users](Identifying_Your_Users.html#adobe-air)
 * [Session Attributes](Session_Attributes.html#adobe-air)
 * [Remote Logging](Remote_Logging.html#adobe-air)

## Titanium
 * [Adding the SDK to your App](../Platforms/Titanium.html)
 * [Private Cloud Integration](Private_Cloud_Integration.html#titanium)
 * [Identifying your Users](Identifying_Your_Users.html#titanium)
 * [Session Attributes](Session_Attributes.html#titanium)
 * [Remote Logging](Remote_Logging.html#titanium)
