---
id: integrations
title: Integrations
sidebar_label: Integrations
---
## SMTP and Gmail
## Email Integrations

In order to increase deliverability and open rates of email messages you send out to users of the system connect your TestFairy account to your **SMTP**, G-suite **Gmail** service or your private Gmail account.

This way your users will get emails from a familiar email address, and will be able to reply directly to you. In addition you will be able to track outgoing messages by checking your `Sent Items` folder in your email account.

This option is recommended for all users and is **included in all packages**.

![Integrations](/img/app/preferences/account-settings-4.png)


In order to integrate your Gmail or SMTP Email account follow these steps:


### SMTP Integration

Press the `Add integration` button next to the **SMTP Email** option.
Add the details in the fields and press `Save SMTP Settings`

![SMTP screen](/img/integrations/SMTP-1.png)


### Gmail Integration
Follow these steps:
- Press the `Add Integration` button next to the **Gmail** option.
- Press the `Authorize Google Apps (Gmail API)` Button:

![gmail integration](/img/integrations/gmail-1.png)

- Select the account you want to use:

![gmail integration](/img/integrations/gmail-2.png)

- **Allow** TestFairy access to the account:

![gmail integration](/img/integrations/gmail-3.png)


You will get a **confirmation messages** instead of the `Authorize Google Apps (Gmail API)` button for a successful integration.
Pressing **revoke** will dissconnect the integration.

![gmail integration](/img/integrations/gmail-4.png)

In the main screen you will see the new Gmail integration in the Active Integrations table:

![gmail integration](/img/integrations/gmail-5.png)

## Slack
## 1. One click integration

TestFairy integrates with Slack seamlessly, providing human-readable, real-time notifications for your selected events.


* Head over to your [TestFairy Dashboard](https://app.testfairy.com), and select **"Account Preferences"** from the top-right menu.
![preferences](/img/app/preferences-link.png)


* Select _Integrations_ from the menu, then click the _Add integration_ button.
![Slack Integration](/img/app/preferences/account-settings-4.png)


* Enter the domain of your slack account:
![slack domain](/img/integrations/slack/slack-domain-1.png)


* This determines where your notifications will appear. You may select an existing channel, or create a new channel. Choose your channel and select **"Authorize"**.
![Authorize channel](http://docs.testfairy.com/img/integrations/slack/slack-1c.png)


* You will be returned to your TestFairy page with the _URL_ and _Events_ already filled in and selected.
Press the `Test URL` to test the webhook.
Select _Save webhook_ to add and confirm the slack integration.
![result](/img/integrations/slack/slack-1d.png)


* Success! You will now receive notifications in your Slack channel.
![slack message](/img/integrations/slack/slack-message-preview.png)


**Note** Integrations require a paid account, click [here](https://www.testfairy.com/pricing) for more information.

## 2. Manual Integration


In case you need to create a manual integration with slack follow these steps:


* Open the Slack [Incoming WebHooks](https://slack.com/apps/A0F7XDUAZ-incoming-webhooks) app


* If you do not have the app installed in your workspace then press `Add to Slack` to add it.
![](/img/integrations/slack/slack-manualint-1.png)


* After adding the app choose the slack channel you want to post the messages in and press the `Add Incoming Webhooks Integration` button.
![](/img/integrations/slack/slack-manualint-2.png)


* In the next screen you will need the __Webhook URL__ link.
![](/img/integrations/slack/slack-manualint-3.png)


* Copy this link and go to the Integrations menu and press the `Add Integration` button for __Slack__.

* Open your TestFairy preferences, go to _Integrations_ and next to WEBHOOK click on _Add integration_ .
![Slack Integration](/img/app/preferences/account-settings-4.png)


* Paste the Webhook URL into the URL field and then `Save webhook`.
![](/img/integrations/slack/slack-manualint-5.png)


* Success! You will now receive notifications in your Slack channel.

## Microsoft Teams
TestFairy integrates with Microsoft Teams seamlessly, providing human-readable, real-time notifications for your selected events.

* Create a new channel, or use an existing channel where notifications will be delivered to. In the image below, a new channel named _TestFairy-Notifications_ is created.
![Alt](/img/integrations/teams/01-create-channel.png)

* Add a Connector to the channel from the dropdown menu.
![Alt](/img/integrations/teams/02-add-connector.png)

* Select _Configure_ or _Add_ the **Incoming Webhook** from the dialog.
![Alt](/img/integrations/teams/03-select-incoming-webhook.png)

* Give the webhook a name, in this case, the webhook will be named _TestFairy Webhook_. Optionally, you can also give the webhook an image.
![Alt](/img/integrations/teams/04-name-webhook.png)

* Copy the webhook endpoint from the dialog.
![Alt](/img/integrations/teams/04-copy-webhook-endpoint.png)

* From your account at [TestFairy](http://app.testfairy.com), go to preferences.
![Alt](/img/integrations/teams/05-go-to-preferences.png)

* From the preferences page, select **Webhooks** and choose **+ Add Webhook**
![Alt](/img/app/preferences/account-settings-4.png)

* Paste the endpoint into the URL field. Give the webhook a name, and select the notifications you wish to receive.
![Alt](/img/integrations/teams/07-edit-webhook.png)

* Optionally, test the integration. Go back to your Teams channel to verify that a notifications was sent.
![Alt](/img/integrations/teams/08-test-webhook.png)

* Save the webhook, and verify that you have a successful message.
![Alt](/img/integrations/teams/09-save-webhook.png)

## Splunk
TestFairy can integrate with Splunk to provide better insights into your mobile apps. This document explains how to export the app logs from TestFairy and import them into your Splunk installation.

#### Exporting logs

Use the [TestFairy Fetch Session Tool](https://github.com/testfairy/testfairy-fetch-sessions) tool to download log files for a specific project.

```
npm install -g --link git+https://github.com/testfairy/testfairy-fetch-sessions.git

testfairy-fetch-sessions --endpoint "acme.testfairy.com" --user "john@example.com" --api-key "0123456789abcdef" --project-id=1000 --logs
```

The logs are downloaded to a folder named `testfairy-sessions` with a directory structure as follows:

![Alt](/img/integrations/splunk/splunk-1.png)

Note that the directory which contains the `session.log` file is also the session identifier. You can use this value to set the _Host_ value later on.

#### Importing logs into Splunk

In your Splunk forwarder, under the settings menu, select _Add Data_:

![Alt](/img/integrations/splunk/splunk-2.png)

Select the _Monitor_ option:

![Alt](/img/integrations/splunk/splunk-3.png)

Select _Files & Directories_:

![Alt](/img/integrations/splunk/splunk-4.png)

With _Files & Directories_ selected, browse to the directory where the log files were downloaded. It's best to point to the top-level `testfairy-sessions` incase you have multiple projects that you'd like to monitor.

![Alt](/img/integrations/splunk/splunk-5.png)

After clicking _Next_, on the _Input Settings_ page, set the _Host_ using the _Segment in path_. Use the directory segment which contains the `session.log` file.

![Alt](/img/integrations/splunk/splunk-6.png)

This will help you search and create search queries based on a specific session.

Create a query where the `host=<session id>` to see logs related to a given session.

![Alt](/img/integrations/splunk/splunk-7.png)

## Zendesk
1. Login to Zendesk, go to [SUBDOMAIN]zendesk.com/agent/admin/api/settings/tokens and create an API KEY.

2. Login to TestFairy -> Preferences -> Integrations -> Zendesk and enter your Zendesk info.

![](/img/integrations/zendesk/zendest-integration-01.png)

3. (optional) Install the [TestFairy Chrome Extension](https://chrome.google.com/webstore/detail/testfairy-for-jira/joaafaemekbkgekhjbaldlllcnjifcee)

## Intercom
1. Login to [Intercom Developer Hub](https://app.intercom.com/a/apps/_/developer-hub), create a new app.

    ![](/img/integrations/intercom/intercom_1.png)

    - Select "New App"
    - Enter an "App Name"
    - Select a your *workspace*. Create one if you needed.
    - Select "Internal app" (Optional)

2. Select your newly created app

    ![](/img/integrations/intercom/intercom_3.png)

    - Go into Authentication.
    - Copy your Access Token. You'll need it for the next step
    - You only need 2 Permissions for the integration: "Write users and companies", and "Write Conversations"

3. In TestFairy, from the Preferences page, select [Integrations](https://app.testfairy.com/settings/integrations/)

    ![](/img/integrations/intercom/intercom_4.png)

    - Click the "Add integration" next to the Intercom row

4. Paste the copied Intercom Access Token into the input field and click "Save Settings".

    ![](/img/integrations/intercom/intercom_5.png)


5. (optional) Install the [TestFairy Chrome Extension](https://chrome.google.com/webstore/detail/testfairy-for-jira/joaafaemekbkgekhjbaldlllcnjifcee)

Congratulations! You've successfully added the Intercom integration to TestFairy. You'll now receive new feedbacks directly in Intercom.

## How to connect TestFairy to Centercode

### 1. Create a Centercode API Key

(Centercode docs available [here](https://help.centercode.com/send-testfairy-feedback-to-centercode))

Open the Centercode Community Homepage, and go to Community Tools > Configuration > API Keys (under Advanced Configuration)   > Create an API Key. Name the new API KEY "TestFairy".

  ![Create API KEY](/img/bug-tracking/centercode1.png)

### 2. Name the new API KEY "TestFairy" and generate the new API Key.

  ![Set Generate Key](/img/bug-tracking/centercode2.png)

### 3. Configure a Centercode externnal feedback source:

  ![Centercode extenrnal feedback source](/img/bug-tracking/centercode3a.png)

  3.1 Click Project Tools

  3.2 Click Feedback Types

  3.3 Hover over your desired Feedback Type (Bug Reports) & click Modify

  3.4 Click External Sources

  3.5 Click "Create an External Source"

  3.6 From the External Sources creation page Create an (internally-facing) Name

  3.7 Provide a simple Key to help identify this External Source  (ex: “appcrashlog” - detailed below)

  3.8 Select the appropriate Workflow state (typically “New”)

  3.9 Configure your Incoming Fields

  3.10 Copy / Save your API Endpoint URL and click Submit

### 4. Configure a new Cetercode integration in your TestFairy dashboard:

  4.1. Open your TestFairy account **Preferences** --> **Integrations** menu. Press the `Add Integration` button.

  ![Create webhook](/img/integrations/centercode/centercode-int-1.png)

  4.2 Name the integration `Centercode`, enter the Centercode endpoint URL, check the `User feedback` checkbox and press `Add webhook`.

  ![Create webhook](/img/integrations/centercode/centercode-int-2.png)




## Coralogix
[Coralogix](https://coralogix.com/) is a machine-learning powered logging platform built for companies performing CI/CD at scale.

In order to integrate TestFairy with Coralogix, and automatically push all the logs collected from
your mobile devices to your Coralogix account, please do the following:

## 1. Install the TestFairy Logs Client on your server:

Install the [TestFairy fetch sessions](https://github.com/testfairy/testfairy-fetch-sessions) logs client on your server by running the following command:
```
npm install -g --link git+https://github.com/testfairy/testfairy-fetch-sessions.git
```

## 2. Configure a cron job that will run the TestFairy client

Create a cron job that will run this command every 15 minutes.

```
testfairy-fetch-sessions --endpoint "your_subdomain.testfairy.com" --user "john@example.com" --api-key "YOUR_API_KEY" --project-id=1000 --logs --json
```

Please make sure to replace the following params:

* Replace **your_subdomain.testfairy.com** with your server address

* Replace **john@example.com** with your admin username

* Replance **YOUR_API_KEY** with your API KEY (found under User preferences --> Upload API key)

* Replace **1000** with your project ID

* Optional: add **--json** to have log line as a json with all session attributes.

* Optional: add **--all-time** flag to get logs from all time. If not used, tool will fetch logs from the last 24 hours only. Do not use this option unless this is the first time you are debugging the service. Logs older than 24 hours are usually a pure waste of good disk space.

* Optional: if your logs are encrypted with RSA public key, then please use --rsa-private-key with your private key for decryption.


## 3. Install Coralogix shipper

1. Download the preconfigured [fluentd.conf](/img/coralogix/fluentd.conf)
2. Edit `fluentd.conf`, and update `CORALOGIX_PRIVATEKEY` and `CORALOGIX_APPNAME`

## 4. Run FluentD

Type this command in your terminal:
```
docker run -d -v `pwd`/fluentd.conf:/fluentd/etc/fluent.conf -v `pwd`:/opt coralogixrepo/fluentd-coralogix-image:latest
```

Fluentd will loop endlessly, looking for new logs files on disk. Make sure you keep this docker container running, while the cron job fetches sessions from TestFairy every now and then.

Congratulations!
You have integrated TestFairy with Coralogix, you can now analyze and monitor mobile app logs in production.




## Bug Tracking systems
To see how you integrate different __Bug tracking__ systems to your TestFairy account look [here](https://docs.testfairy.com/Bug_Tracking/Overview.html).
