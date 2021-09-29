---
id: api
title: API
sidebar_label: API
---
## Upload API
Streamline your build process and upload APKs or IPAs directly to TestFairy.

### Usage
[Command line uploader](https://github.com/testfairy/command-line-uploader/blob/master/testfairy-uploader.sh)

[Jenkins](https://plugins.jenkins.io/TestFairy)

[Gradle](https://github.com/testfairy/testfairy-gradle-plugin)

[Android Studio](http://docs.testfairy.com/Android/Uploading_with_Android_Studio.html)

[fastlane](https://docs.fastlane.tools/actions/testfairy/)

[Travis CI](https://docs.testfairy.com/Continuous_Integration/Travis_CI.html)

[CircleCI](https://circleci.com/docs/2.0/deploying-ios/#uploading-to-testfairy)

[Bitrise](http://devcenter.bitrise.io/tutorials/deploy/deploy-to-testfairy-with-bitrise/)

[Visual Studio Team Services](https://docs.testfairy.com/Continuous_Integration/Visual_Studio_Team_Services.html)

[NetBeans](http://plugins.netbeans.org/plugin/52087/)

[Bamboo](https://docs.testfairy.com/Continuous_Integration/Bamboo.html)

[TeamCity](https://docs.testfairy.com/Continuous_Integration/TeamCity.html)

[GitLab](https://docs.testfairy.com/Continuous_Integration/GitLab.html)

[Lumberyard](https://docs.testfairy.com/Platforms/Lumberyard.html)

### Method
`POST https://upload.testfairy.com/api/upload/`

### Parameters

| Name            |  Required?  | Description  |
|:----------------|:-----------:|:-------------|
| api_key         | Required    | Your API application key. See https://app.testfairy.com/settings for details. |
| file            | Required    | APK (Android), IPA (iOS) or ZIP (MacOS) file data. |
| symbols_file    | Optional    | Symbols mapping file. For iOS this should be a path to the **zipped** symbols file. For Android, this is the path to the mappings.txt file |
| testers_groups  | Optional    | Either a comma-separated list of tester groups to be invited on the new build, or "all" to invite all testers. |
| notify          | Optional    | Send email to all users in tester_groups. The default is "on". |
| release_notes   | Optional    | Release notes for this upload. This text will be added to emails and landing pages. |
| auto_update     | Optional    | Allows an easy upgrade of all users to the current version. The default is "off", to enable set as "on". |
| tags            | Optional    | Set of comma-separated tags to be displayed and search upon. |

### Error Codes

In the case of an error, TestFairy will return a JSON with `status` => `fail` and `code` with one of the values
listed below. An additional human-readable error message is supplied to detail the cause of the specific error.

| Error Code | Reason |
|-----------:|:-------|
| 1          | Parameter 'xxx' is missing |
| 5          | Invalid API key |
| 105        | Invalid file |

### Example 1: (CURL)
```
curl https://upload.testfairy.com/api/upload -F api_key='your_api_key' -F file=@sample.apk
```

### Example 2:
```
curl https://upload.testfairy.com/api/upload \
	-F api_key='your_api_key' \
	-F file=@sample.apk \
	-F symbols_file=@sample_mapping.txt \
	-F testers_groups='friends,beta' \
	-F notify='on' \
	-F release_notes='stabilitty fixes, improvedment in ui' \
	-F tags='production, english'
```

### Example Response:
```
{
	"status": "ok",
	"app_name": "Jigsaw Puzzlers",
	"app_version": "0.9.5",
	"app_url": "https://app.testfairy.com/download/6CWKJCHD60PPVWYJHGM4AADJQYA4SDR0/filename.apk",
	"landing_page_url": "https://tsfr.io/3tajti",
}
```

### Where can I find my API Key?

In order to get your API KEY, open your account preferences at https://app.testfairy.com/settings/ and click on "Upload API Key".

### How can I create a new API Key?

In order to create a new API KEY just click on "Regenerate API Key" in your account preferences page.

### Why is my API Key empty?

In cases where we identify that your API KEY was used by mistake to initialize the SDK instead of using your APP TOKEN, we automatically reset the API KEY in order to protect your privacy. In this case, please change the SDK initialization to use the APP TOKEN and create a new API KEY.

### Can I add custom metadata?

Yes. Any POST parameter that its name is prefixed with "metadata." will be considered custom data and stored along with the upload. For example, consider this command:

```
curl https://upload.testfairy.com/api/upload \
	-F api_key='your_api_key' \
	-F file=@sample.apk \
	-F metadata.branch=master \
	-F metadata.locale=us-en
```

Metadata is displayed and can be searched upon in App Versions page, by clicking on an app from the Dashboard. They can also be viewed in a single version's settings page.

## Rest API
This is the reference document for the TestFairy REST API. This API allows the developer to access and interact with TestFairy data remotely.

#### Getting Started

Getting started with the REST API is easy, and can be done via command line with any programming language. Let's begin with a simple example. We will start by listing all our projects.

A project is either an iOS app or an Android app (two apps with the same package name but on different platforms are considered two projects.)

<pre>
curl -u "john@example.com:00001234cafecafe" "https://api.testfairy.com/api/1/projects/"
</pre>

In the example above, you can see that our user is `john@example.com` and the API key is `0001234cafecafe`. This user authentication token is required for all requests to the REST server.

**Your API key is private**, please do not share it or post it on public code repositories or forums. To find your API key, please refer to [your preferences page](https://app.testfairy.com/settings).

<hr />

<a name="projects"></a>
#### [api/1/projects](#)

<div class="method">
	<span>
		<button class="expand">▶</button> Get all projects
	</span>
	<code>GET /api/1/projects/</code>
</div>
<div class="method-description hidden">
	Returns a list of all projects (iOS and Android apps) in this account.<br />
	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok",
	"projects": [
		{
			"id": "19-groupshot",
			"self": "/projects/19-groupshot",
			"name":"GroupShot",
			"packageName":"com.groupshot",
			"platform":"Android",
			"icon":"[URL TO APP ICON]"
		}
	]
}</pre>
</div>

<hr />

<a name="builds"></a>
#### [api/1/projects/{project-id}/builds/](#)

<div class="method">
	<span>
		<button class="expand">▶</button> Get all builds in a project
	</span>
	<code>GET /api/1/projects/{project-id}/builds/</code>
</div>
<div class="method-description hidden">
	Get all builds in a specific project. Each build is a distinct version that was either uploaded, or created by the TestFairy SDK.<br />
	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok",
	"builds": [
		{
			"id":8830728,
			"self":"/projects/6806100-myapplication/builds/8830728",
			"projectId":"6806100",
			"appName":"My Application",
			"appVersion":"DemoApp",
			"appVersionCode":"20",
			"appDisplayName":"My Application - DemoApp (20)",
			"iconUrl":"[APP ICON URL]",
			"appUrl":"[URL TO APK OR IPA FILE]",
			"sessions":6,
			"crashes":0,
			"testers":0,
			"feedbacks":0,
			"downloads":1,
			"uploadedAt":"2019-04-04 16:03:15",
			"uploadedVia":"[UPLOAD DETAILS]",
			"hasTestFairySdk":true,
			"insightsEnabled":true,
			"videoEnabled":true
		}
	]
}
</pre>
</div>

<hr />

<a name="sessions"></a>
#### [api/1/projects/{project-id}/builds/{build-id}/sessions/](#)

<div class="method">
	<span>
		<button class="expand">▶</button> List all recorded sessions in build
	</span>
	<code>GET /api/1/projects/{project-id}/builds/{build-id}/sessions/</code>
</div>
<div class="method-description hidden">
	Get metadata for all sessions recorded for a specific build.<br />
	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok",
	"sessions": [
		{
			"id": 1,
			"self": "/projects/2197059-demoapp/builds/4867553/sessions/1",
			"startTime": "2017-01-22 16:42:40",
			"duration": "15:01",
			"testerEmail": "john@testfairy.com",
			"device": "Samsung - Samsung Galaxy S8",
			"ipAddress": "23.100.122.175",
			"crashed": false,
			"countryName": "United States",
			"countryCode": "us"
		}
	]
}


</pre>
</div>

<hr />

#### [api/1/projects/{project-id}/builds/{build-id}/sessions/{session-id}/](#)

<div class="method">
	<span>
		<button class="expand">▶</button> Get session data, events and logs
	</span>
	<code>GET /api/1/projects/{project-id}/builds/{build-id}/sessions/{session-id}/</code>
</div>
<div class="method-description hidden">
	Get metadata (and optionally data) for a specific session.<br />

	<table>
	<tr>
		<th style="width: 160px;"><b>parameter</b></th>
		<th style="width: 100px;"><b>type</b></th>
		<th><b>description</b></th>
	</tr>
	<tr>
		<td>fields</td>
		<td><em>string</em></td>
		<td>
			Possible values: "meta", "logs", "events"<br />
			Default value: "meta" <br/>
			Use "events" to load all events, screenshots, touches and other metrices. Use "logs" to fetch
			only logs. When loading logs, response will be application/text.
		</td>
	</tr>
	</table>

	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok",
	"session": {
		"id":4426273741,
		"sessionStartTime":"2019-05-20 09:05:30",
		"duration":"00:27",
		"testerEmail":"blabla@ex.com",
		"device":"Xiaomi - Redmi S2",
		"ipAddress":"84.94.200.136",
		"crashed":false,
		"identity":{
			"correlationId":"blabla@ex.com",
			"attr3":"three",
			"attr4":"four",
			"attr1":"High",
			"attr2":"1.0",
			"attr5":"Version 1.0"
	}
}
</pre>
</div>

<hr />

<a name="testers"></a>
#### [api/1/testers/](#)

<div class="method">
	<span>
		<button class="expand">▶</button> List all testers
	</span>
	<code>GET /api/1/testers/</code>
</div>
<div class="method-description hidden">
	List all testers in this account.<br />
	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok",
	"testers": [
		{
			"email":"james@example.com",
			"groups":[{
				id: 100,
				name: "friends"
			}]
		},
		{
			"email":"alice@testfairy.com",
			"groups":[{
				id: 100,
				name: "friends"
			}, {
				id: 200,
				name: "family"
			}]
		}
	]
}
</pre>
</div>

<div class="method">
	<span>
		<button class="expand">▶</button> Add a new tester
	</span>
	<code>POST /api/1/testers/</code>
</div>
<div class="method-description hidden">
	Add a new tester to account. Optionally can add them to a group.<br />

	<table>
	<tr>
		<th style="width: 160px;"><b>parameter</b></th>
		<th style="width: 100px;"><b>type</b></th>
		<th><b>description</b></th>
	</tr>
	<tr>
		<td>email</td>
		<td><em>string</em></td>
		<td>
			One or more emails, separated by commas, to add to your account.
		</td>
        </tr>
	<tr>
		<td>group</td>
		<td><em>string</em></td>
		<td>
			Assign tester or testers to this tester-group. Will create one if no such group exists.
			Default value: none<br />
		</td>
	</tr>
	<tr>
		<td>notify</td>
		<td><em>string</em></td>
		<td>
			Pass "notify=on" to send out a welcome email when inviting this tester. The email sent is
			the `Tester Welcome Email` template and can be configured.
			Default value: off<br />
		</td>
	</tr>
	</table>

	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok"
}
</pre>
</div>

<!---- -->

<div class="method">
	<span>
		<button class="expand">▶</button> Block a tester
	</span>
	<code>POST /api/1/testers/{tester-id}/block/</code>
</div>
<div class="method-description hidden">
	Blocks a single tester. They cannot download the apps they were invited to. However, the data
	stays. You can later unblock this tester, or delete them completely.

	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok"
}
</pre>
</div>

<!--- --->

<div class="method">
	<span>
		<button class="expand">▶</button> Unblock a tester
	</span>
	<code>DELETE /api/1/testers/{tester-id}/block/</code>
</div>
<div class="method-description hidden">
	Unblocks a single tester. Their invitations are restored. If the user is already unblocked, then
	nothing happens.

	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok"
}
</pre>
</div>


<!--- -->

<div class="method">
	<span>
		<button class="expand">▶</button> Delete a tester
	</span>
	<code>DELETE /api/1/testers/{tester-id}</code>
</div>
<div class="method-description hidden">
	Delete a single tester, remove them from any tester-groups they might be in, and invalidate
	all invitations that were sent.<br />

	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok"
}
</pre>
</div>

<hr />

<a name="feedbacks"></a>
#### [api/1/feedbacks/](#)

<div class="method">
	<span>
		<button class="expand">▶</button> Get latest recorded feedbacks
	</span>
	<code>GET /api/1/feedbacks/</code>
</div>
<div class="method-description hidden">
	Get metadata for 100 of the latest feedbacks recorded. <br />
	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok",
	"feedbacks": [
		{
			"recorded_at": "2018-08-01 04:14:46",
			"text": "Feedback working",
			"feedbackId": "54321",
			"screenshotUrl": "https://s3.amazonaws.com/feedback.jpg",
			"buildId": "1234",
			"projectId": "23456",
			"recordedAt":"2018-08-01 14:14:46",
			"source": "shake",
			"reported_by": "john@testfairy.com",
			"session_id": "8765432"
		}
	]
}
	</pre>
</div>

<hr />

#### [api/1/audits/](#)

<div class="method">
	<span>
		<button class="expand">▶</button> Get recent audit trail items
	</span>
	<code>GET /api/1/audits/</code>
</div>
<div class="method-description hidden">
	Get recent audit trail items<br />
	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok",
	"audits": [
		{
			"id": 23534603,
			"timestamp": "2020-04-21 02:31:54",
			"ipAddress": "54.235.41.91",
			"eventType": "download_app",
			"eventData": {			
				"projectId": 6833287,
				"buildId": 9087976,
				"appName": "MyApp",
				"appVersion": "1.0 (10)",
				"testerEmail": "john@example.com",
				"filesize": 31348
			}
		}
	]
}
	</pre>
</div>

<hr />

<a name="permissions"></a>
#### [api/1/cpanel/permissions/](#)

<div class="method">
	<span>
		<button class="expand">▶</button> Get the list of admins and their permissions
	</span>
	<code>GET /api/1/cpanel/permissions/</code>
</div>
<div class="method-description hidden">
	Get the list of admins in the account and their permissions. <br />
	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok",
	admins:
	[
		{
			email: "joe@example.com",
			role: "account-owner",
			permissions: [
				"*:rw"
			]
		},
		{
			email: "bob@example.com",
			role: "account-manager",
			permissions: [
				"*:rw"
			]
		},
		{
			email: "alice@example.com",
			role: "admin",
			permissions: [
				"*:rw"
			]
		},
		{
			email: "michael@example.com",
			role: "admin",
			permissions: [
				"16527:rw",
				"16517:rw",
				"69237:r"
			]
		},
	]
}
	</pre>
</div>

<hr />

<a name="webhooks"></a>
#### [api/1/webhooks/](#)

<div class="method">
	<span>
		<button class="expand">▶</button> List all webhooks
	</span>
	<code>GET /api/1/webhooks/</code>
</div>
<div class="method-description hidden">
	List all webhooks in this account.<br />
	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status":"ok",
	"webhooks":[
		{
			"id":12,
			"status":"0",
			"name":"Slack Webhook @vijay",
			"url":"https://hooks.slack.com/services/",
			"actions":"crash,feedback,upload,new-udid",
			"projectIds":"12345,45643"
		}
	]
}
</pre>
</div>

<div class="method">
	<span>
		<button class="expand">▶</button> Add a new webhook
	</span>
	<code>POST /api/1/webhook/</code>
</div>
<div class="method-description hidden">
	Add a new webhook to account.<br />

	<table>
	<tr>
		<th style="width: 160px;"><b>parameter</b></th>
		<th style="width: 100px;"><b>type</b></th>
		<th><b>description</b></th>
	</tr>
	<tr>
		<td>webhook-name</td>
		<td><em>string</em></td>
		<td>
			Required. The name of the webhook.
		</td>
	</tr>
	<tr>
		<td>webhook-url</td>
		<td><em>string</em></td>
		<td>
			Required. The url for the webhook.
		</td>
	</tr>
	<tr>
		<td>webhook-status</td>
		<td><em>string</em></td>
		<td>
			Enables or disables the webhook, true or false.<br>
			Default value: false
		</td>
	</tr>
	<tr>
		<td>actions</td>
		<td><em>string</em></td>
		<td>
			Comma separated list of actions. options include
			<ul>
				<li>crash</li>
				<li>feedback</li>
				<li>upload</li>
				<li>new-udid</li>
			</ul>
		</td>
	</tr>
	<tr>
		<td>webhook-project-ids</td>
		<td><em>string</em></td>
		<td>
			Optional. Comma separated list of project IDs.
		</td>
	</tr>
	</table>

	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok"
}
</pre>
</div>

<!---- -->

<div class="method">
	<span>
		<button class="expand">▶</button> GET a single webhook
	</span>
	<code>GET /api/1/webhhook/{webhook-id}/</code>
</div>
<div class="method-description hidden">
	Returns a single webhook.

	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok",
	"webhook": {
		"id":12,
		"status":"0",
		"name":"Slack Webhook @vijay",
		"url":"https://hooks.slack.com/services/",
		"actions":"crash,feedback,upload,new-udid",
		"projectIds":"12345,45643"
	}
}
</pre>
</div>

<!--- --->

<div class="method">
	<span>
		<button class="expand">▶</button> MODIFY a webhook
	</span>
	<code>POST /api/1/webhhook/{webhook-id}/</code>
</div>
<div class="method-description hidden">
	Modifies a single webhook.

<table>
	<tr>
		<th style="width: 160px;"><b>parameter</b></th>
		<th style="width: 100px;"><b>type</b></th>
		<th><b>description</b></th>
	</tr>
	<tr>
		<td>webhook-name</td>
		<td><em>string</em></td>
		<td>
			Required. The name of the webhook.
		</td>
	</tr>
	<tr>
		<td>webhook-url</td>
		<td><em>string</em></td>
		<td>
			Required. The url for the webhook.
		</td>
	</tr>
	<tr>
		<td>webhook-status</td>
		<td><em>string</em></td>
		<td>
			Enables or disables the webhook, true or false.<br>
			Default value: false
		</td>
	</tr>
	<tr>
		<td>actions</td>
		<td><em>string</em></td>
		<td>
			Comma separated list of actions. options include
			<ul>
				<li>crash</li>
				<li>feedback</li>
				<li>upload</li>
				<li>new-udid</li>
			</ul>
		</td>
	</tr>
	<tr>
		<td>webhook-project-ids</td>
		<td><em>string</em></td>
		<td>
			Optional. Comma separated list of project IDs.
		</td>
	</tr>
	</table>

	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok"
}
</pre>
</div>


<!--- -->

<div class="method">
	<span>
		<button class="expand">▶</button> Delete a webhook
	</span>
	<code>DELETE /api/1/webhhook/{webhook-id}/</code>
</div>
<div class="method-description hidden">
	Delete a single webhook.<br />

	<span class="responses">Responses</span><br />
	<span class="status-green">STATUS 200</span> OK<br />
	<pre>
{
	"status": "ok"
}
</pre>
</div>

<hr />

<style>h4 {margin-bottom: 30px;}</style>

## Webhooks
Webhooks allow simple integration between TestFairy and your backend. Using these webhooks, you can subscribe for specific events, and receive an HTTP POST request whenever such event occurs.

This can be used when, for example, you'd like to receive a notification when a new build has been uploaded, and send it to the development team. Another example may be that you'd like to save the feedbacks received in your own database or backend.

To configure webhooks, simply open the Webhooks tab in your [User Preferences](https://app.testfairy.com/settings/) page. You can configure more than one webhook, and each webhook applies to selected projects and selected events.

TestFairy will automatically detect Slack endpoints, and send a proper payload. Please follow the instructions in the [Slack integration guide](/Integrations/Slack.html).

### Supported Events

| Events   | Description |
|----------|-------------|
| Upload   | Every time a build is uploaded by one of the team members |
| Download | Every time a tester downloads a build via invitation link |
| Crash    | Every time the app crashes |
| Feedback | Every time a tester fills in a feedback, whether it's in-app or web |

### Payload

The payload of the HTTP POST request is always a JSON. The ***event*** field specifies the type of event, and the rest of the fields are specific for that type. Please review the *sample payloads* section blow for more information about fields in each event.

### Sample payload for Upload Event

```json
{
    "event": "upload",
    "timestamp": "2015-07-01 13:37:54",
    "version": "1.0",
    "build": 1,
    "appName": "Demo App",
    "filesize": 563876,
    "iconUrl": "https://testfairy.s3.amazonaws.com/icons/4/68348e8d8265771d64636e2d57bb9a672f812e1a.png",
    "communityUrl": "https://tsfr.io/myapp"
}
```

### Sample payload for Download Event

```json
{
    "event": "download",
    "timestamp": "2015-07-01 13:37:54",
    "version": "1.0",
    "build": 1,
    "appName": "Demo App",
    "filesize": 563876,
    "buildUrl": "https://app.testfairy.com/projects/10-demoapp/builds/584120",
    "iconUrl": "https://testfairy.s3.amazonaws.com/icons/4/68348e8d8265771d64636e2d57bb9a672f812e1a.png",
    "testerEmail": "bob@corporation.com",
    "referer": "http://my.testfairy.com"
}
```

### Sample payload for Crash Event

```json
{
    "event": "crash",
    "timestamp": "2015-07-01 12:01:59",
    "version": "1.0",
    "build": 1,
    "appName": "Demo App",
    "filesize": 563876,
    "buildUrl": "https://app.testfairy.com/projects/10-demoapp/builds/584120",
    "iconUrl": "https://testfairy.s3.amazonaws.com/icons/4/68348e8d8265771d64636e2d57bb9a672f812e1a.png",
    "email": "felix@corporation.com",
    "deviceName": "Samsung Galaxy S2",
    "rawDeviceName": "samsung gt-i9100t",
    "crashMessage": "java.lang.NullPointerException",
    "ipAddress": "54.227.255.225"
}
```

### Sample payload for Feedback Event
```json
{
    "event": "feedback",
    "timestamp": "2015-07-01 17:21:00",
    "version": "1.0",
    "build": 1,
    "appName": "Demo App",
    "filesize": 563876,
    "buildUrl": "https://app.testfairy.com/projects/10-demoapp/builds/584120",
    "iconUrl": "https://testfairy.s3.amazonaws.com/icons/4/68348e8d8265771d64636e2d57bb9a672f812e1a.png",
    "sessionUrl": "https://app.testfairy.com/projects/10-demoapp/builds/584120/sessions/1",
    "screenshotUrl": "https://app.testfairy.com/projects/10-demoapp/builds/584120/sessions/1/screenshots/d64636e2d57672f812e1a348e8.jpg",
    "correlationId": "user-95",
    "email": "alice@corporation.com",
    "rawDeviceName": "samsung gt-i9100t",
    "ipAddress": "54.227.255.225",
    "text": "App doesn't render nicely in landscape"
}
```

## API Reference
## TestFairy SDK

- [Android SDK class reference](https://docs.testfairy.com/reference/android/index.html)
- [iOS SDK class reference](https://docs.testfairy.com/reference/ios/Classes/TestFairy.html)

## TestFairy API

- [Upload API reference](http://docs.testfairy.com/API/Upload_API.html)
- [REST API reference](http://docs.testfairy.com/API/Rest_API.html)
- [Webhooks reference](http://docs.testfairy.com/API/Webhooks.html)
