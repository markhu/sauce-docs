---
id: ios-sdk
title: iOS SDK
sidebar_label: iOS SDK
---
## Integrating iOS SDK
<iframe width="854" height="480" src="https://www.youtube.com/embed/DhRX5UukvPM" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

Integrating the TestFairy SDK into your app helps you better understand how your app performs on real devices. It tells you when and how people are using your app, and provides you with any metrics you may need to optimize your user experience and code.
You get to:

* Track app use.
* Handle crashes and report to server.
* Record screen video and other metrics.
* Understand user flow, using checkpoints.
* Grab NSLogs from client and report to server.
* Automatically update if a new build is available.

## Add the SDK

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
  <div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
    <a data-w-tab="tab-spm" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#spm">
      <div>Swift Package Manager</div>
    </a>
    <a data-w-tab="tab-cocoapods" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#cocoapods">
      <div>Cocoapods</div>
    </a>
    <a data-w-tab="tab-carthage" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#carthage">
      <div>Carthage</div>
    </a>
    <a data-w-tab="tab-manual" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#manual">
      <div>Manual</div>
    </a>
  </div>

  <div class="docs-tabs-content w-tab-content">
    <div data-w-tab="tab-spm" class="w-tab-pane w--tab-active">
      <p><b>Note: Requires Xcode 12+</b></p>
      <p>
        <ol>
          <li>
            <p>Click "File > Swift Packages > Add Package Dependency..."</p>
            <blockquote>
              <p><img src="https://docs.testfairy.com/img/ios/sdk/xcframework1.png" alt="alt"></p>
            </blockquote>
          </li>
          <li>
            <p>Add the TestFairy package repository URL: <em>https://github.com/testfairy/testfairy-ios-sdk-swift-package</em> </p>
            <blockquote>
              <p><img src="https://docs.testfairy.com/img/ios/sdk/xcframework2.png" alt="alt"></p>
            </blockquote>
          </li>
          <li>
            <p>Select the appropriate package options</p>
            <blockquote>
              <p><img src="https://docs.testfairy.com/img/ios/sdk/xcframework3.png" alt="alt"></p>
            </blockquote>
          </li>
          <li>
            <p>Click "Finish"</p>
            <blockquote>
              <p><img src="https://docs.testfairy.com/img/ios/sdk/xcframework4.png" alt="alt"></p>
            </blockquote>
          </li>
        </ol>
      </p>
    </div>
    <div data-w-tab="tab-manual" class="w-tab-pane">
      <ol>
        <li>Download the framework from our <a href="https://app.testfairy.com/sdk/ios/" target="_blank">Download page</a>.</li>
        <li>
          <p>Unzip files and drag them into your project tree.</p>
          <blockquote>
            <p><img src="https://app.testfairy.com/images/app/sdk/tutorial-unzip-files.png" alt="alt"></p>
          </blockquote>

          <p>Make sure <strong>Copy items if needed</strong> is checked when dragging files to your project.</p>

          <blockquote>
            <p><img src="https://docs.testfairy.com/img/ios/sdk/copy-items-if-needed.png" alt="alt"></p>
          </blockquote>
        </li>
        <li>
          <p>Add the following frameworks:
            <br>
          </p>
          <p>
            <ul>
              <li>In Xcode, select the project file from the project navigator, on the left side of the project window.</li>
              <li>Show Projects and Target List.</li>
              <li>In the project settings editor, select the target to which you would like to add frameworks.</li>
              <li>Select the “Build Phases” tab, and click the small triangle next to “Link Binary With Libraries” to view all of the frameworks in your application.</li>
            </ul>
          </p>
          <ul>
            <li><code>CoreMedia.framework</code></li>
            <li><code>CoreMotion.framework</code></li>
            <li><code>AVFoundation.framework</code></li>
            <li><code>SystemConfiguration.framework</code></li>
            <li><code>OpenGLES.framework</code></li>
          </ul>
          <p>
            <img class="instruction-gif" width="700" src="https://doa2yz3uy4ty4.cloudfront.net/images/app/header/xcode-demo-1.gif"></p>
        </li>
      </ol>
    </div>

    <div data-w-tab="tab-cocoapods" class="w-tab-pane">
      <p>Add the <em>TestFairy</em> pod to your Podfile by inserting the following line where applicable:</p>
      <pre>
				<code class=" hljs bash">pod <span class="hljs-string">'TestFairy'</span></code>
			</pre>
			<p>Run the <em>$ pod install</em> command to install the <em>TestFairy</em> dependency.</p>
    </div>

    <div data-w-tab="tab-carthage" class="w-tab-pane">
      <p>Once you have Carthage installed, you can begin adding frameworks to your project. Note that Carthage only supports dynamic frameworks, which are <strong>only available on iOS 8 or later</strong> (or any version of OS X).
        <br>
      </p>
      <ol>
        <li>Add <code>binary "https://app.testfairy.com/sdk/ios/carthage.json"</code> to your Cartfile.</li>
        <li>Run <code>carthage update</code>. </li>
        <li>On your application targets’ “General” settings tab, in the “Linked Frameworks and Libraries” section, drag and drop the TestFairy framework from the [Carthage/Build][] folder on disk.</li>
      </ol>
      <p><img src="../../img/ios/carthage/carthage_1.png" alt="">
        <br>
      </p>
      <ol>
        <li>
          <p>On your application targets’ “Build Phases” settings tab, click the “+” icon and choose “New Run Script Phase”. Create a Run Script in which you specify your shell (ex: <code>bin/sh</code>), add the following contents to the script area below
            the shell:</p>

          <pre><code class="language-sh hljs perl">/usr/<span class="hljs-keyword">local</span>/bin/carthage copy-frameworks
				</code></pre>

          <p>and add the paths to the TestFairySDK frameworks under “Input Files”, e.g.:</p>

          <pre><code class=" hljs bash"><span class="hljs-variable">${SRCROOT}</span>/Carthage/Build/iOS/TestFairySDK.framework
				</code></pre></li>
      </ol>
      <p><img src="../../img/ios/carthage/carthage_2.png" alt=""></p>
    </div>

  </div>
</div>

### Initialize the SDK

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
  <div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">
    <a data-w-tab="tab-ios-objc" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;" href="#ios-objc">
      <div>Objective-C</div>
    </a>
    <a data-w-tab="tab-ios-swift" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;" href="#ios-swift">
      <div>Swift</div>
    </a>
  </div>

  <div class="docs-tabs-content w-tab-content">
    <div data-w-tab="tab-ios-objc" class="w-tab-pane w--tab-active">
      <ol>
        <li>
          <p>Open your <strong>AppDelegate.m</strong> file.</p>
        </li>
        <li>
          <p>Add this code to your app:</p>
          <iframe frameborder="0" width="100%" height="200" src="https://app.testfairy.com/sdk/ios/iframe"></iframe>
        </li>
      </ol>
    </div>

    <div data-w-tab="tab-ios-swift" class="w-tab-pane">
      <ol>
        <li>
          <p>Create an Objective-C bridging header</p>
          <p>Since this process only needs to be done once per project, if you have already done so, just update your bridging header file.</p>

          <ul>
            <li>Right-click on your project, select <code>New File...</code></li>
            <li>Select <code>Header File.h</code></li>
            <li>Save as <code>Bridging.h</code> in your project</li>
            <li>Click on <code>Bridging.h</code> to open it in editor</li>
            <li>Add the following line to the code: </li>
          </ul>

          <pre><code class=" hljs java">#<span class="hljs-keyword">import</span> <span class="hljs-string">"TestFairy.h"</span></code></pre>
	  <p>NOTE: If framework wasn't uploaded manually please try:</p>
	  <pre><code class=" hljs java">#<span class="hljs-keyword">import</span> <span class="hljs-string">"TestFairy/TestFairy.h"</span></code></pre>



          <p>Update Build Settings with the new bridging header:</p>

          <ul>
            <li>Click on your project</li>
            <li>Select <em>Build Settings</em> tab</li>
            <li>Select the "All" filter, in order to find <em>Swift Compiler - General</em>: <em>Objective-C Bridging Header</em></li>
            <li>Edit <em>Swift Compiler - Code Generation</em>: <em>Objective-C Bridging Header</em> (double-click to edit).</li>
            <li>Drag "Bridging.h" from the source tree onto the edit box opened</li>
          </ul>
        </li>
        <li>
          <p>Open your <strong>AppDelegate.swift</strong> file.</p>
        </li>
        <li>
          <p>Add this code to your app:</p>
          <iframe frameborder="0" width="100%" height="200" src="https://app.testfairy.com/sdk/ios-swift/iframe"></iframe>
        </li>
      </ol>
    </div>

  </div>
</div>

### Using PencilKit for Better Feedback

You can give your users a better set of tools to markup any screenshots provided during feedback by adding PencilKit to your project. Simply add the PencilKit.framework to your project.

> **Note**: This requires iOS 13 and Xcode 11 and up in order to add

![alt](/img/ios/sdk/pencilkit.png)

Now, if a screenshot is attached to the feedback, your users can edit the screenshot by tapping on it and using PencilKit to mark it up.

![alt](/img/ios/sdk/pencilkit-feedback.png)

### Class Reference

[https://docs.testfairy.com/reference/ios/Classes/TestFairy.html](https://docs.testfairy.com/reference/ios/Classes/TestFairy.html)

### Troubleshooting

For more information about common problems when integrating the iOS SDK, please visit
our [FAQ page](https://docs.testfairy.com/FAQ.html)

### Related documentation

* [Upload iOS dSYM files to TestFairy](/iOS_SDK/Uploading_dSyms_to_TestFairy.html)


## Uploading dSyms to TestFairy
TestFairy can show you crash reports to help you identify the place in the code that is causing a problem. TestFairy crash reports are easier to understand when they show actual debug symbols instead of addresses.

TestFairy requires your app's debug symbols (dSYMs) to clearly show you the names of the methods in your code. DSYM files are created by Xcode when you build your app. There are a couple of ways to upload them to TestFairy (see below).

* [Generate Symbols in Xcode](#generate-symbols)
* [Uploading Symbols to TestFairy](#upload-symbols)
	* [How to upload multiple dSYMs](#multiple-symbols)
	* [Fatal: Can't find .dSYM folder!](#fatal-dsym)
* [Handling missing DSYMs](#missing-symbols)
	* [Locating dSYMs on your hard-drive](#locate-missing-dsym)
	* [Locating dSYMs for Bitcode builds](#bitcode-dsym)

#  <a name="generate-symbols"></a>Generate Symbols in Xcode

First, make sure your Xcode project is configured to generate the debug symbols:

1. Click on your project and select Build-Settings.
2. In the search box, type "Debug Information Format".
3. Click on "Debug Information Format" and select "DWARF with dSYM File"
![alt dsym](https://docs.testfairy.com/img/ios/dsym-upload/dsym.png)

#  <a name="upload-symbols"></a>Uploading Symbols to TestFairy

<p>In order to upload symbols to TestFairy, you'll need to have your <strong>UPLOAD_API_KEY</strong> ready, which can be found from your <a href="https://app.testfairy.com/settings/api-key/" target="_blank">user preferences page</a>.</p>

<div data-duration-in="300" data-duration-out="100" class="docs-tabs w-tabs">
	<div class="docs-tabs-menu w-tab-menu" style="flex-wrap: wrap;">

		<a data-w-tab="tab-xcode" class="docs-tab w-inline-block w-tab-link w--current" style="margin: 2px;"  href="#xcode">
			<div>Xcode</div>
		</a>

		<a data-w-tab="tab-upload-api" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#upload-api">
			<div>Upload API</div>
		</a>

		<a data-w-tab="tab-upload-script" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#upload-script">
			<div>Upload Script</div>
		</a>

		<a data-w-tab="tab-build-settings" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#build-settings">
			<div>Build Settings</div>
		</a>

		<a data-w-tab="tab-jenkins" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#jenkins">
			<div>Jenkins</div>
		</a>

		<a data-w-tab="tab-xamarin-studio" class="docs-tab w-inline-block w-tab-link" style="margin: 2px;"  href="#xamarin-studio">
			<div>Xamarin Studio</div>
		</a>
	</div>

	<div class="docs-tabs-content w-tab-content">
		<div data-w-tab="tab-xcode" class="w-tab-pane w--tab-active">
			<p>A simple Build Phase script can automatically upload the compressed .dSYM file for future symbolication</p>

			<ol>
				<li>
					<div>
						<div>In Xcode, click on your project in the left sidebar, then click on <strong>Build Phases</strong>.</div>
						<p><img src="../../img/ios/dsym-upload/step1.png" alt="alt"><br></p>
					</div>
				</li>

				<li>
					<div>
						<div>
							Click on <strong><em>plus sign</em></strong> on the left and select <strong>New Run Script Build Phase</strong>
						</div>
						<p><img src="../../img/ios/dsym-upload/step2.png" alt="alt"><br></p>
					</div>
				</li>

				<li>
					<div>
						<div>
							Open the newly added <strong>Run Script</strong> and add this line at the bottom:
						</div>

						<pre><code class="language-sh hljs bash">sh <span class="hljs-string">"<span class="hljs-variable">${SRCROOT}</span>/TestFairy/upload-dsym.sh"</span> UPLOAD_API_KEY
						</code></pre>

						<p>If you're using <strong>Cocoapods</strong>, you will have to use a different path to <code>upload-dsym.sh</code> You can use either:</p>

						<pre><code class="language-sh hljs bash">sh <span class="hljs-string">"<span class="hljs-variable">${SRCROOT}</span>/Pods/TestFairy/upload-dsym.sh"</span> UPLOAD_API_KEY
						</code></pre>

						<p>or</p>

						<pre><code class="language-sh hljs bash">sh <span class="hljs-string">"<span class="hljs-variable">${PODS_ROOT}</span>/TestFairy/upload-dsym.sh"</span> UPLOAD_API_KEY
						</code></pre>

						<p>If you're using <strong>Carthage</strong>, you will have to use a different path to <code>upload-dsym.sh</code></p>

						<pre><code class="language-sh hljs bash">sh <span class="hljs-string">"<span class="hljs-variable">${SRCROOT}</span>/Carthage/Build/iOS/TestFairySDK.framework/upload-dsym.sh"</span> UPLOAD_API_KEY
						</code></pre>

						<p>If you're using <strong>Swift Package Manager</strong>, you will have to use a different path to <code>upload-dsym.sh</code></p>

						<pre><code class="language-sh hljs bash">sh <span class="hljs-string">"<span class="hljs-variable">${TARGET_BUILD_DIR}</span>/TestFairy.framework/upload-dsym.sh"</span> UPLOAD_API_KEY
						</code></pre>

						<div>
							<p>Make sure the specified path includes the upload-dsym.sh file.</p>
							<p>Make sure to replace <strong>UPLOAD_API_KEY</strong> with the your secret upload API key, found in the <a href="https://app.testfairy.com/settings/api-key/">Settings</a> page.</p>
							<p><img src="../../img/ios/dsym-upload/step3.png" alt="alt"></p>
						</div>
					</div>
				</li>
			</ol>

		</div>

		<div data-w-tab="tab-upload-api" class="w-tab-pane">
			<p>We recommend uploading dSYM files together with the app build files.<br>
			Use our upload API and add the dSYM files when the app is ready for distribution and testing.<br>
			</p>
			<ol>
				<li>
					<p>Create a zip file from the contents of your symbols directory. The best way to locate this path can be found <a href="#missing-symbols">here</a>.</p>

					<p>For example, the following command creates a zip file called <code>symbols.zip</code> from the symbols of my ‘Hi’ app and stores it in the <code>/tmp</code> directory.</p>

					<p><code>zip -r /tmp/symbols.zip<br>
					~/Library/Developer/Xcode/DerivedData/Hi/Build/Products/Debug-iphoneos/Hi.app.dSYM/*</code></p>
				</li>
				<li>
					<p>Run the upload command:
					</p>

					<p><code>curl https://app.testfairy.com/api/upload \<br>
					 &nbsp;&nbsp;&nbsp;-F api_key='UPLOAD_API_KEY' \ <br>
					 &nbsp;&nbsp;&nbsp;-F file='YOUR IPA FILE GOES HERE' \ <br>
					 &nbsp;&nbsp;&nbsp;-F symbols_file='YOUR ZIPPED SYMBOLS FILE GOES HERE' \ <br>
					&nbsp;&nbsp;&nbsp;-F testers_groups='friends,beta' \ <br>
					&nbsp;&nbsp;&nbsp;-F notify='on'</code></p>
				</li>
			</ol>
			<p></p>
			<p>If you need further instructions regarding our upload API, <a href="/API/Upload_API.html">read about it here</a></p>
		</div>

		<div data-w-tab="tab-upload-script" class="w-tab-pane">
			<p>If you are not planning to upload your app to TestFairy and you are not using Xcode, follow these instrucitons to upload your debug symbols:<br></p>
			<ol>
				<li>
					<p>Locate your DSYM_PATH directory. The best way to locate this path can be found <a href="#missing-symbols">here</a>.</p>
				</li>
				<li>
					Download the upload dSYM script from <a href="https://s3.amazonaws.com/testfairy/sdk/upload-dsym.sh">here</a>
				</li>
				<li>
					<p>Run this script:</p>
					<p><code>./upload-dsym.sh -f UPLOAD_API_KEY -p DSYM_PATH</code></p>
				</li>
			</ol>

			<p>Once you run the script it will compress the symbols directory and upload the symbols to TestFairy.</p>
		</div>

		<div data-w-tab="tab-build-settings" class="w-tab-pane">
			<p>If you upload apps straight from the TestFairy dashboard, upload your debug symbols from the build-settings page. Here is how you do it:</p>
			<ol>
				<li>
					<p>Create a zip file from the contents of your symbols directory. The best way to locate this path can be found <a href="#missing-symbols">here</a>.</p>

					<p>For example, the following command creates a zip file called <code>symbols.zip</code> from the symbols of my ‘Hi’ app and stores it in the <code>/tmp</code> directory.</p>

					<p><code>zip -r /tmp/symbols.zip<br>
					~/Library/Developer/Xcode/DerivedData/Hi/Build/Products/Debug-iphoneos/Hi.app.dSYM/*</code></p>
				</li>
				<li>
					<p>Login to TestFairy and go to the "App Overview" page by clicking the name of your app.</p>
				</li>
				<li>
					<p>Enter the build overview page by clicking on the build you wish to upload symbols for
				(If you only have one build, you will not see a list of builds, but rather land directly on the correct build overview page).
					</p>
				</li>
				<li>
					<p>Click on 'Build-Settings' from the top menu, then select the 'Symbolication' section.</p>
				</li>
				<li>
					<p>Select the zip files with the dSYM you just created and click "Upload"</p>
				</li>
			</ol>
		</div>

		<div data-w-tab="tab-jenkins" class="w-tab-pane">
			<p>If you have never used the TestFairy Jenkins plugin before, see the <a href="https://wiki.jenkins-ci.org/display/JENKINS/TestFairy+Plugin" target="_blank">installation instructions.</a>. Once set up, Xcode will build your app on the Jenkins server, and upload the app's symbols.</p>

			<ol>
				<li>
					<div>
						<div>Open Xcode on the machine that runs on Jenkins, click on your project in the left sidebar, then click on <strong>Build Phases</strong>.</div>
						<p><img src="../../img/ios/dsym-upload/step1.png" alt="alt"><br></p>
					</div>
				</li>

				<li>
					<div>
						<div>
							Click on <strong><em>plus sign</em></strong> on the left and select <strong>New Run Script Build Phase</strong>
						</div>
						<p><img src="../../img/ios/dsym-upload/step2.png" alt="alt"><br></p>
					</div>
				</li>

				<li>
					<div>
						<div>
							Open the newly added <strong>Run Script</strong> and add this line at the bottom:
						</div>
						<pre><code class="language-sh hljs bash">sh <span class="hljs-string">"<span class="hljs-variable">$SRCROOT</span>/TestFairy/upload-dsym.sh"</span> UPLOAD_API_KEY
						</code></pre>
						<div>
							<p>Make sure the specified path includes the upload-dsym.sh file.</p>
							<p>Make sure to replace <strong>UPLOAD_API_KEY</strong> with the your secret upload API key, found in the <a href="https://app.testfairy.com/settings/#apikey">Settings</a> page.</p>
							<p><img src="../../img/ios/dsym-upload/step3.png" alt="alt"></p>
						</div>
					</div>
				</li>
			</ol>
		</div>

		<div data-w-tab="tab-xamarin-studio" class="w-tab-pane">
			<p>If you are using Xamarin, please refer to instructions in <a href="/Platforms/Xamarin.html">this page</a>.</p>
		</div>

	</div>

</div>

##  <a name="multiple-symbols"></a>How to upload multiple dSYMs

You can upload multiple dSYMs per build. Some developers have frameworks developed in-house, and these frameworks make it to the final .IPA file. In order to upload dSYM in your framework project, just repeat the above steps using pointing to your framework's settings.

##  <a name="fatal-dsym"></a>Fatal: Can't find .dSYM folder!

If while compiling you get the error `Fatal: Can't find .dSYM folder!`, your project is not configured to [generate debug symbols](#generate-symbols).

#  <a name="missing-symbols"></a>Handling missing DSYMs

If you see a message in TestFairy about missing DSYMs or if you've published your app to the AppStore with Bitcode enabled, follow these instructions to locate and upload DSYMs.

##  <a name="locate-missing-dsym"></a>Locating dSYMs on your hard-drive

If your build is missing dSYMs, you can find them and upload them manually to TestFairy.

1. Login to TestFairy and go to the App overview page by clicking the name of your app.
2. Click on the name of your app build to reach the build overview page.
3. Click on 'Settings' from the Build menu, then select the 'Symbolication' section.
4. This section lists several required UUIDs (representing binary app builds for different device architecture or binary builds for frameworks you're using). To see crash reports with your classes and method names, you'll need to upload dSYMs for each UUID that is specified as required.
5. Open a command line terminal and run the following command to locate the DSYMs folder name for one of the listed required UUIDs (replace '<UUID>' with the actual UUID string):
    ```sh
    mdfind "com_apple_xcode_dsym_uuids == <UUID>" | grep dSYM
    ```
6. Create a zip file with the content of the DSYM directory (you can call the zip file any name you like)
	```
	zip -r /tmp/symbols.zip <YOUR_DSYM_LOCATION>/*
	 ```
7. Proceed to upload the zip as described [here](#upload-symbols).

If you can't locate your dSYMS using `mfind`, follow these instructions:

1. In Xcode, open the organizer window.
2. Control-Click the relevant build, and select "Show in Finder".
3. In Finder, Control-Click the archive and select "Show Package Contents".
4. The archive will contain a folder called dSYM.
5. Create a zip with the contents of the folder and proceed to upload the zip to TestFairy as explained [here](#upload-symbols).

##  <a name="bitcode-dsym"></a>Locating dSYMs for Bitcode builds.

If you enabled Bitcode for your build and released it to the store or submitted to TestFlight, take note that Apple will generate new dSYMs for your app and you'll need to download the new dSYMs from Xcode, and then upload them to TestFairy.

1. In Xcode, open the organizer window.
2. Click on the relevant build.
3. From the right side menu, click "download dSYMs".
4. Manually upload the dSYMs to TestFairy, [as described here](#upload-symbols)

## Logs on iOS 10
## Sending NSLog to TestFairy
The TestFairy SDK records your app being used so you can watch recorded sessions to solve problems faster. The SDK can record videos, screenshots, custom events, logs and device metrics.

This page explains how to set iOS apps to send NSLog to TestFairy (this applies to iOS 10 and future versions).

### Objective-C

See the [SDK Documentation](https://docs.testfairy.com/SDK/Remote_Logging.html#ios) for more information.

### Swift

See the [SDK Documentation](https://docs.testfairy.com/SDK/Remote_Logging.html#ios-swift) for more information.

## Adding UDIDs to iOS development profile
<iframe width="560" height="315" src="https://www.youtube.com/embed/omYf_-KjPE0" frameborder="0" allowfullscreen></iframe>

There are two ways to sign iOS apps.

There is the enterprise certificate that technically allows you to send your app to any iOS device, and there is the Ad-Hoc certificate that requires you to get the user's device ID before sending them an ipa file.

This document refers to ad-hoc certificates and explains how to add a testers' UDID to your app development profile in the Apple developer portal.

We warmly recommend any company to apply to Apple's [iOS Developer Enterprise Program](https://developer.apple.com/programs/ios/enterprise/), and sign iOS apps for internal use with an Enterprise certificate. Please note that this is not a legal document, and refer to Apple's website for the exact terms of service for any Apple service.

In order to add a UDID to your Ad-Hoc certificate please follow the following instructions:

1. Open your TestFairy [testers page](https://app.testfairy.com/testers) and invite new testers. You can add multiple addresses, one per line.
Your testers will get an email asking them to register their device. Once they register, you will get an email with your tester's UDID and their device details will be listed in https://app.testfairy.com/testers

2. Once you have all your testers' UDIDs [export their details](https://app.testfairy.com/testers/export/).

3. Log into the Apple Developer Portal and go to the [Devices area](https://developer.apple.com/account/resources/devices/list).

4. Click on the + icon
![alt](/img/app/apple-dev-plus.png)

5. You may register one or multiple devices.

    5.1 For adding one device add the device details in the **Register a Device** form.

    5.2 Use **Register multiple devices** for registering devices from a file, choose your file and continue.
  ![alt](/img/app/apple-dev-import.png)

6. Follow the on screen instructions.

7. Click on **profiles** [distribution section](https://developer.apple.com/account/resources/profiles/list)
![alt](/img/app/apple-dev-profile-create.png)

8. Follow the on screen process to generate the profile.

9. Generate the new profile and download the file.

11. Make sure to delete the previous profile files.

## Install Custom Enterprise Apps On iOS
### Manually install and trust an enterprise app
When you first open an enterprise app that you've manually installed, you see a notification that the developer of the app isn't trusted on your device. You can dismiss this message, but then you can't open the app.

![](/img/ios/sdk/trust-app-1.png)

To establish trust for the app developer tap Settings → General → Profiles or Profiles & Device Management.
Under the "Enterprise App" heading, you see a profile for the developer of the app you want to trust.

![](/img/ios/sdk/trust-app-2.png)

Tap the name of the developer profile under the Enterprise App heading to establish trust for this developer.

![](/img/ios/sdk/trust-app-3.png)

You will get a prompt to confirm your choice.

![](/img/ios/sdk/trust-message.png)

Once you trust this profile, you can install and run any other apps from the same developer. This developer will remain trusted until you remove all apps of this developer.

## Log Network
With TestFairy, you can log all your network requests. This gives you an easy way to monitor network access your app is doing.

A common issue our users discovered while monitoring their apps, is **slow** requests or **4xx** error code. These problems are usually hard to discover manually. TestFairy will list all network requests in the session page. Fixing these issues will greatly improve the experience for your users.

![see example](https://raw.githubusercontent.com/testfairy/docs/master/img/app/logHttp.png)

### Code Samples

[Android](https://docs.testfairy.com/SDK/Network_Logging.html#android)

[iOS Objective-C](https://docs.testfairy.com/SDK/Network_Logging.html#ios-objc)

[iOS Swift](https://docs.testfairy.com/SDK/Network_Logging.html#ios-swift)

## Hiding webview elements from video
TestFairy enables developers to hide specific HTML elements from a recorded video in any `UIWebView` or `WKWebView` within their application. As the developer, you may choose to hide one or more elements from the video for security and privacy reasons.

For example, you might want to prevent all information related to credit card data from appearing in the session.

### Syntax

To hide an element from video, all you need to do is call the static instance method `hideWebViewElements` in the `TestFairy` class passing in a CSS selector to target your element:

**`[TestFairy hideWebViewElements:@"body"];`**  
**`[TestFairy hideWebViewElements:@"div#username,div#password"];`**  
**`[TestFairy hideWebViewElements:@".col-12,h1 .header"];`**

TestFairy will find any `UIWebView` or `WKWebView` in the view hierarchy, and hide a given HTML element based on a valid CSS selector.

### Sample video

Below is a sample screen taken from a demo video. On the left, you can see what an app looks like normally. On the right is a screenshot taken with the HTML elements hidden.

<div>
<img style="float:left" src="../../img/ios/hidden_views/iphone-with-fields.png" width="400" />
<img style="float:left" src="../../img/ios/hidden_views/iphone-no-fields.png" width="400" />
</div>

<br style="clear: both" />

### Notes

* Elements are hidden from screenshots before they are uploaded.
* You may use `hideWebViewElements` with multiple comma separated selectors.
* You may add more selectors at any time by calling `hideWebViewElements` again.


### Related Articles

* [Hiding views in iOS](https://docs.testfairy.com/iOS_SDK/Hiding_views_from_video.html)
* [Hiding views in Android](https://docs.testfairy.com/iOS_SDK/Hiding_views_from_video.html)

## Exporting Ad Hoc IPA
Apple allows app distribution for testing on registered devices using an **Ad-Hoc** or **Enterprise** provisioning profile.

The output file you create is an iOS App file (a file with an `.ipa` filename extension) that is then used to install your app on registered devices.

Following are the steps to export your app for testing:

1. Register all test devices using the instructions <a href="https://docs.testfairy.com/Testers/Registering_Your_iOS_Device_UDID_Number.html" target="_blank">here</a>.
2. Archive your app (see instructions below).
3. Export the archive to an IPA file using either an Ad Hoc or Enterprise provisioning profile to code sign your app.
4. Install the app on test devices.

## About Ad Hoc Provisioning Profiles

An ad hoc provisioning profile is a distribution provisioning profile that allows your app to be installed on designated devices and to use app services without the assistance of Xcode.

There are 4 types of distribution provisioning profiles you can create for apps:


  - iOS App Store - for distributing through the apple app store.

  - Ad Hoc - for installing on **[designated devices](https://docs.testfairy.com/iOS_SDK/Adding_UDIDs_to_iOS_development_profile.html)**.

  - <a href="https://developer.apple.com/programs/enterprise/" target="_blank">Enterprise</a> - for distributing an app within your organization.

  - <a href="https://developer.apple.com/support/certificates/" target="_blank">Development</a> - For distributing within members of your team.


Make sure you have created an Ad Hoc provisioning profile specifying an `App ID` that matches one or more of your apps, a set of **test devices**, and a single **distribution certificate** at the [developer portal](https://idmsa.apple.com/IDMSWebAuth/login?&appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&path=%2F%2Fmembercenter%2Findex.action).

We warmly recommend any company to apply to Apple's iOS Developer [Enterprise Program](https://developer.apple.com/programs/enterprise/), and sign iOS apps for internal use with an Enterprise certificate.
* Please note that this is not a legal document, and refer to Apple's website for the exact terms of service for any Apple service.


## Archiving Your App

Create an archive of your app. Xcode stores this archive in the **Archives organizer**.

In the Xcode project editor, choose `Generic iOS Device` — or your device name from the Scheme toolbar menu. (You can’t create an archive of a simulator build).

If a device is connected to your Mac, the device name appears in the Scheme toolbar menu. When you disconnect the device, the menu item changes to the `Generic iOS Device`.

![alt](../../img/ios/export_ipa/01_device.png)

Choose **Product** --> **Archive**.

The Archives organizer appears and displays the new archive.

Xcode runs preliminary validation tests on the archive. To create an IPA file press the `Distribute App` button.

![alt](../../img/ios/export_ipa/02_archive.png)

## Exporting Your App to an IPA (**Ad Hoc** provisioning profile)

To create an iOS App file for testing, select an archive in the **Archives organizer**.

![alt](../../img/ios/export_ipa/03_archive_organizer.png)

Click the **Distribute App** button. Select an export option, and click Next.

To distribute your app to users with designated devices, choose the  `Save for Ad Hoc Deployment`. The app will be code signed with the distribution certificate.

![alt](../../img/ios/export_ipa/04_select_dist_method.png)

In the dialog that appears, choose a signing method and click Next.

![alt](../../img/ios/export_ipa/05_export_choose_options.png)

In the distributions options screen, choose the options you prefer and click Next.

![alt](../../img/ios/export_ipa/055_export_choose_signing_options.png)

After you choose the signing options click **Next**.

![alt](../../img/ios/export_ipa/06_export_to_file.png)

In the dialog that appears, review the app, its entitlements, and the provisioning profile.
Click **Export** and finally the Finder shows the exported files. Save it to your desired location.

## Installing Your App on Test Devices Using Xcode

You can install iOS App files on devices using Xcode.

To install an app on a device using Xcode

1. Connect the device to your Mac.

2. In Xcode, choose Window > Devices and select the device under Devices.

3. In the Installed Apps table, click the Add button (+) below the table.

 ![install_an_app](/img/ios/export_ipa/device-and-install.png)

4. In the dialog that appears, choose the iOS App file and click Open.

 ![chose file](/img/ios/export_ipa/choose-ipa-file.png)

5. The app is now added to the list of installed app end is installed n the device.

 ![](/img/ios/export_ipa/app-is-installed.png)

##  <a name="xcode-system-logs"></a>Accessing Logs from Xcode

Accessing raw logs on an iOS device requires hooking up that device via a USB cable to a computer. System logs often help a lot in debugging vague problems around app installation.

Many times, the error displayed on an iOS device screen is too generic, but the system logs explain more thoroughly the reason for the problem. In order to get the logs, complete the following:

* Open Xcode.
* Open menu Window -> Devices.
* Select the device which you want to inspect.
* Click on the `View Device Logs` button.
* A new window will open up with up-to-date logs from the device.

![How to access device logs](/img/ios/export_ipa/view-device-logs.png)

# References

1. [Apple developer site](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/TestingYouriOSApp/TestingYouriOSApp.html)



## Customizing feedback dialog
See the [SDK Documentation](https://docs.testfairy.com/SDK/Customizing_feedback_dialog.html) for more information.

### Class Reference

For more information, please refer to the [iOS SDK class reference](https://app.testfairy.com/reference/ios/).

## Class Reference
TestFairy iOS SDK class reference has [moved](https://docs.testfairy.com/reference/ios/Classes/TestFairy.html).

## FAQ
<a name="top"></a>

* [My app crashes while offline, will I get the report?](#crashes-offline)
* [Will crashes be caught even after a session stopped recording?](#crashes-after-stop)
* [Which architectures are supported?](#ios-archs)
* [Which iOS platforms are supported?](#ios-platforms)
* [Am I required to use the TestFairy SDK?](#ios-sdk-required)
* [How do I fix "App could not be installed at this time"?](#ios-app-could-not-be-installed)
* [Why do I see sessions by "User-1"?](#ios-whats-user-1)
* [Why does an app icon disappear right after download?](#ios-app-icon-disappears)
* [Why linking fails with `ld: symbol(s) not found for architecture arm64`?](#ios-symbol-not-found)
* [What's the error "You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE)"?](#ios-bitcode-error)
* [Push notifications work when installed from Xcode, but not with TestFairy. Why?](#ios-push-notificatios-xcode)
* [What is the difference between in-house and enterprise certificates?](#ios-in-house-or-enterprise)
* [Main Thread Checker: UI API called on a background thread: -\[UIView drawViewHierarchyInRect:afterScreenUpdates:\]](#main-thread-checker)

### <a name="crashes-offline"></a>My app crashes while offline, will I get the report?

Yes.

TestFairy keeps crashes on disk if it can't send them immediately. The next time the app runs, TestFairy will send out the saved crash reports and attach them to the appropriate sessions.

### <a name="crashes-after-stop"></a>Will crashes be caught even after a session stopped recording?

Yes.

Session max-duration controls how much of the session will be recorded. Many developers won't be interested in video recording beyond the initial 10 minutes. Crashes are caught regardless of the max-duration limit.

In cases where a crash happens beyond the max-duration limit, the report will be attached to the session, along with the part that was recorded.

[Back to top](#top)

### <a name="ios-archs"></a>Which architectures are supported?

TestFairy iOS SDK supports the following architectures (CPUs):

* ARMv7
* ARMv7s
* ARM64
* i386 (simulator)
* x86_64 (simulator)
* BITCODE

[Back to top](#top)

### <a name="ios-platforms"></a>Which iOS platforms are supported?

TestFairy SDK is a static library, therefore it runs on any platform that uses XCode for compilation. For ease of integration, TestFairy is also available as:

* Cocoapods
* Xamarin binding (both 32-bit and 64-bit)
* .NET assembly (.DLL)
* .NET assembly via NuGET package
* Xamarin binding through Xamarin Component Store
* Unity plugin
* Adobe Air Extension (.ANE)
* PhoneGap / Cordova plugin
* Titanium
* React-Native

[Back to top](#top)

### <a name="ios-sdk-required"></a>Am I required to use the TestFairy SDK?

The TestFairy platform is used for both distribution and for analytics. You can use either both, or just one of them.

App distribution does not require integration of the TestFairy SDK and provides an easy-to-use platform for sending iOS IPA files to testers and colleagues in your enterprise. Simply upload an Ad Hoc or Enterprise signed IPA files and send e-mail invitation to the selected testers.

Using analytics requires integration of the SDK. This is a 2-minute task that involves adding just a single line of code to your project. With analytics enabled, you will able to see a video recording of your app being used, as well as receive logs from the device, analyse usage with checkpoints or loading view controllers and much much more. For more information, please follow the [integration manual](http://docs.testfairy.com/iOS_SDK/Integrating_iOS_SDK.html).

[Back to top](#top)

### <a name="ios-app-could-not-be-installed"></a>How do I fix "App could not be installed at this time"?

**"App could not be installed at this time"** is a generic error when iOS cannot install the download app on the device. The reasons vary, and may be one of these:

* The device's UDID is not included in the provisioning profile.
* Not enough disk space for installation on device.
* The device's architecture (eg. ARMv7) is not supported by the app.
* The device's operating system version (eg. 7.0) is too low for the app.
* The device's platform mismatches (eg. iPad app on an iPhone.)
* Enterprise team is not included in prefix in embedded.mobileprovision file.
* App is not signed with an Ad Hoc or Enterprise (in-house) certificate.

TestFairy has a **Troubleshooting** tool to guide the tester or developer through the debugging of such problems. Simply visit https://my.testfairy.com/my/troubleshooting using Safari on your iOS device and follow the instructions.

If all this fails, please contact support by click on the **Support** button in your account page. Try to get the [system logs](/iOS_SDK/Exporting_Ad_Hoc_IPA.html#xcode-system-logs) from the device if possible as this makes debugging this sorts of problems a lot easier. We do our best to help debug causes and improve our one-of-a-kind Troubleshooting tool.

[Back to top](#top)

### <a name="ios-whats-user-1"></a>Why do I see sessions by "User-1"?

When using the TestFairy iOS SDK, all sessions are anonymous. Without access to device information, TestFairy cannot tell what's the email address of the tester.

It *does* know how to associate sessions by the same testers to the same "User-1". Using a token that is stored when the first session is created, TestFairy can identify sessions by the same tester.

Furthermore, TestFairy supports ***correlationId***. This identifier is any string that makes sense to the developer (you). It can be an email address of the tester, their Facebook id number, or an identifier in your own database. Using the SDK, simply call `[TestFairy setCorrelationId:@"my-id-00000000"];`, and this identifier will show in all reports, instead of the generic User-1 values. Use this correlationId as you see fit.

[Back to top](#top)

### <a name="ios-app-icon-disappears"></a>Why does an app icon disappear right after download?

When downloading an iOS app, the iOS operating system will show a progress during downloading and installation. This progress looks like an analog clock, an empty circle becoming full.

After installation completes, the system then checks if the app is alread installed on the device. If it does, it replaces the old app with the version recently downloaded. You may have this app icon in a different screen tab, or maybe inside a folder.

Tip: Pull down the view to reveal the Spotlight search dialog. You can type the name of the app, and it will locate it on your device, regardless of screen tab or folder.

[Back to top](#top)

### <a name="ios-symbol-not-found"></a>Why does linking fail with `ld: symbol(s) not found for architecture arm64`?</a>

On various Xcode project configurations, you might receive the following error when linking with TestFairy:

```
"_OBJC_CLASS_$_TestFairy", referenced from:
ld: symbol(s) not found for architecture arm64
```

For those projects, please add `libTestFairy.a` as a framework in your Build Settings.

[Back to top](#top)

### <a name="ios-bitcode-error"></a>What's the error "You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE)"?

Xcode7 introduced a new feature (virtual architecture) called `Bitcode`. This is a short for LLVM Bitcode, which is a virtual machine architecture Xcode uses as an intermediate platform for compilation. Instead of compiling apps to armv7, armv7s, arm64 - Xcode can now create a single architecture and the AppStore will generate optimized binaries for mobiles. This will greatly reduce the IPA filesize as an iPhone6+ user won't be downloading the binaries needed for iPhone4, etc.

To compile an app with `bitcode`, it is required that all libraries and frameworks used will have bitcode enabled as well. Alternatively, you can disable ENABLE_BITCODE in your Xcode project. As of October 2015, it is not required by Apple for app submittion, but might be required in the future.

TestFairy iOS SDK version 1.5.0 has bitcode flag enabled, which solves this problem. Simply upgrading the SDK will resolve this error in compilation.

[Back to top](#top)

### <a name="ios-push-notificatios-xcode"></a>Push notifications work when installed from Xcode, but not with TestFairy.
Why?

TestFairy's SDK does not make any changes to your executable or IPA. A very common problem we have been seeing, is that developers make a mistake and develop using sandbox, and release using a production app's environment. Please make sure your configuration is the same for production and adhoc/in-house releases.

[Back to top](#top)

### <a name="ios-in-house-or-enterprise"></a>What is the difference between in-house and enterprise certificates?

These two are the same. When exporting an IPA from within Xcode, you export for Enterprise Development, but in some cases on iTunes Connect, this is refered as In-House.

[Back to top](#top)

### <a name="main-thread-checker"></a>Main Thread Checker: UI API called on a background thread: -[UIView drawViewHierarchyInRect:afterScreenUpdates:]

Xcode introduced a runtime checker to catch calls to UI method that are only meant to be called from the main thread. Our iOS SDK currently heavily leverages some APIs that fall under this category. If this checker is enabled, you will see a warning in the Console not unlike the one you can see below.

```
Main Thread Checker: UI API called on a background thread: -[UIView drawViewHierarchyInRect:afterScreenUpdates:]
PID: 7067, TID: 6554424, Thread name: (none), Queue name: com.apple.root.utility-qos, QoS: 17
Backtrace:
4   TestApp                             0x0000000104aa70bf -[TFScreenRecorder render:] + 3727
5   TestApp                             0x0000000104aa5a28 __65-[TFScreenRecorder performCreateSavableImageSingleTime:callback:]_block_invoke + 168
6   libdispatch.dylib                   0x000000010c21e7ab _dispatch_call_block_and_release + 12
7   libdispatch.dylib                   0x000000010c21f7ec _dispatch_client_callout + 8
8   libdispatch.dylib                   0x000000010c22b61d _dispatch_root_queue_drain + 1353
9   libdispatch.dylib                   0x000000010c22b076 _dispatch_worker_thread3 + 132
10  libsystem_pthread.dylib             0x000000010c743169 _pthread_wqthread + 1387
11  libsystem_pthread.dylib             0x000000010c742be9 start_wqthread + 13
```

In some cases, developers have enabled the `Pause on issues` option which causes either tests to fail, or Xcode to breakpoint on the line in question. Currently the only workaround is to turn off the `Pause on issues` option in Xcode under the scheme's Run configuration on the Diagnostics tab. You can see the option below.

![alt](/img/ios/sdk/disable-pause-on-issue.png)

[Back to top](#top)
