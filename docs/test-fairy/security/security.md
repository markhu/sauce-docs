---
id: security
title: Security
sidebar_label: Security
---
## Private Cloud
TestFairy for enterprise is available in a Private Cloud architecture.

It includes the following features:

- Single Tenant database

- Dedicated Firewall, can be configured to allow access only from specific addresses such as your office or your subnet

- VPN access.

- [SAML Single Sign On](https://docs.testfairy.com/Single_Sign_On/SSO.html).



![ alt upload](/img/cloud-map.png)

## End to End Data Encryption
TestFairy provides a mechanism to encrypt the logs and the screenshots that are recorded from the mobile device. This way, the data that is kept on the cloud is encrypted and nobody can read it other than the people in your team who have the private key.
In order to use this capability, you will need to  create a public key and a private key. The public key will be used to initialize the TestFairy SDK in your app. The private key, which should not be shared with anybody, will be used by you, when you log in to your TestFairy dashboard.

This encryption is done with a randomly generated 256-bit AES key. This AES key is random and is only used in a single session recording. The AES key is then protected with an RSA key, where the public key is provided when constructing the SDK.

#### Generating public/private key pair

Generating a pair is done using openssl tool:

```
openssl genrsa -out testfairy-private-key.pem 2048
openssl rsa -in testfairy-private-key.pem -outform DER -pubout | base64 - > testfairy-public-key.txt
```

This will create two files called `testfairy-private-key.pem` and `testfairy-public-key.txt` containing your private and public keys.

The file `testfairy-private-key.pem` is sensitive and should not be shared with anyone that is not part of your team.

The content of `testfairy-public-key.txt` will be used to initialize the SDK. Please paste this value into the first parameter of `TestFairy.setPublicKey` method.

#### Using in Android

Enable end-to-end encryption for your Android apps by calling `setPublicKey` before calling the `begin` method.

```
TestFairy.setPublicKey("<PUBLIC KEY>");
TestFairy.begin("<APP TOKEN>");
```

#### Using in iOS

Enable end-to-end encryption for your iOS apps by calling `setPublicKey` before calling the `begin` method.

```
[TestFairy setPublicKey:@"<PUBLIC KEY>"];
[TestFairy begin:@"<APP TOKEN>"];
```

#### Viewing encrypted sessions

Since the data is encrypted using RSA, viewing a session requires the private key. Simply visiting a recorded session will prompt a dialog for entry of the RSA Private Key. Just paste the private key text and click "OK". Your private keys are never sent to the server and are only kept within the browser session.

**Important note:** it's crucial that you keep the private key safe. If lost, these sessions cannot be recovered and the recorded data will become useless.

<a name="technical-details"></a>
#### Technical details (How does it work?)

As a developer who wants to encrypt their sessions, you generate a private key and derive a public key from it.

You put your public key in your app, and this key is not a secret. This key can be only used to encrypt data, but not decrypt it back.

When a new session starts (calling TestFairy.begin after TestFairy.setPublicKey), the SDK generates a random AES key and encrypts it with the RSA public key you provided.

This means that every session has a different AES key (in CBC mode), and is not shared between sessions. The AES key is 128 bit, and the encrypted data may be decrypted if you have the key. The random key is encrypted by the public key by itself. This means that a 3rd party wants to view the session, they need to run 2^128 brute force combinations to find one session. AES is used to encrypt the data, as it is so much faster than RSA, and is not limited by length of cleartext value.

Notice that the data that is encrypted includes the logs and the screenshots. If encryption is enabled, certain features are automatically disabled, such as showing values entered in EditText fields, or the text of a button that was clicked.


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

## Single Sign On
Single Sign-on enables you to manage users and testers outside of TestFairy.
TestFairy supports SAML and is fully compatible with Okta, OneLogin, Ping, Oracle, IBM and Azure ADFS.


Here are the [SSO](https://docs.testfairy.com/Single_Sign_On/SSO.html) connection options available.


Talk to us! [Request a demo](https://testfairy.com/products/solutions/enterprise#request-a-demo)

## GDPR
The EU General Data Protection Regulation (GDPR) was designed to harmonize data privacy laws across Europe, to protect and empower all EU citizens data privacy and to reshape the way organizations across the region approach data privacy.

Following these regulations, here are some answers to your questions:

### Can TestFairy provide a GDPR Compliant service?

Yes. TestFairy can provide a GDPR compliant service to customers on a Private Cloud or On Premise instalaltions. Please contact us for more details.

### Can TestFairy Provide full Transparency?

Yes. TestFairy end-users are ensured that their personal data is only used by TestFairy for legitimate purposes, meaning for the purpose intended by the developers who use our platform. We do not and will never sell, transfer or otherwise harm your personal data, and make sure it is only used via our services.

### Can TestFairy end-users see their sessions?

Yes. On a Private cloud or on an on-prem installation, it is possible for companies to allow their end-users to see their recorded sessions. This requires the developer to identify the sessions, by using the SDK function [setUserId](https://docs.testfairy.com/SDK/Identifying_Your_Users.html).
Users will only be able see their sessions by logging into TestFairy via their desktop browser. At the moment mobile view is not supportd.

### Can TestFairy Users request to delete their sessions?

Yes. On a Private cloud or on an on-prem installation, it is possible for companies to allow their end end-users to request to the delete their sessions. Deletion request is done by clicking on the delete button at the top right corner of every session.
The deletion request will be sent to the account owner, who will confirm the deletion.
It is important to mention that the deletion of data is done by the account owner and under his responsibility.

![ alt create-bug](../../img/app/delete-btn.png)

### Can TestFairy end-users see a notifiction explaining what is going to be recorded?

TestFairy requires customers to notify users that they are recorded. This can be done in the app TOS that must be easily accesible and easy to read and understand, and also possible to display a visual dialong (pop up) when the app starts, explaining the user that they are recorded for quality assurance purposes and how they can request to delete their data.
In case of a showing a visual disclaimer, this should be done before calling the function TestFairy.begin.

### Can TestFairy data can be automatically deleted after 30 days?

Yes. TestFairy can automatically delete sessions older than 30 days or any other time perioud required by your company. Deletion is permanent and can not be undone.

### Can the service be hosted in Europe?

Yes. In addition to the US, Private Clouds can be also hosted on AWS in the UK, Germany and France.
