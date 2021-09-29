---
id: bug-tracking
title: Bug Tracking
sidebar_label: Bug Tracking
---
## Overview
Connect TestFairy to your Bug Tracking software
Before we start, make sure to connect TestFairy to your bug tracking account:

- [Connect TestFairy to JIRA Cloud](https://docs.testfairy.com/Bug_Tracking/JIRA_Cloud.html)
- [Connect TestFairy to JIRA Server](https://docs.testfairy.com/Bug_Tracking/JIRA_Server.html)
- [Connect TestFairy to Github](https://docs.testfairy.com/Bug_Tracking/Github.html)
- [Connect TestFairy to Trello](https://docs.testfairy.com/Bug_Tracking/Trello.html)
- [Connect to TFC (TestFairy Connect)](https://docs.testfairy.com/Bug_Tracking/TestFairy_Connect.html)
- [Connect TestFairy to Micro Focus ALM Octane](https://docs.testfairy.com/Bug_Tracking/Micro_Focus_ALM_Octane.html)

# Shake to Feedback

TestFairy makes feedback as easy and effortless as a simple shake of your device.

<iframe width="854" height="480" src="https://www.youtube.com/embed/lVlXx01jrU8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

When using your app with "In-app Feedback" enabled, your users can post comprehensive feedback at any time by shaking their device.
An email will pop up on screen, ready for filling in a report. It also comes with an attahched screenshot your tester can scribble on.
Once they send this email, a feedback message is sent to all the relevant destinations (such as your developer's dashboard, JIRA, Slack, etc.) along with their input, the video recording of the session and all the data collected throughout it.

# Enabling Shake to Feedback in your Build Settings

- Choose the app and Build in which you'd like to enable Shake to Feedback

![ alt upload](../../img/bug-tracking/build-settings.png)

- Go to the "Bug Reporting" section of the build and make sure to check the box for __In-App Bug Reporting__ and then `Save changes`.

![ alt upload](../../img/bug-tracking/bug-report-enabled.png)

## JIRA Cloud
Connect TestFairy to JIRA Cloud

## 1. Create a JIRA API token

1.1 log in to [https://id.atlassian.com/manage/api-tokens#](https://id.atlassian.com/manage/api-tokens#) and click on "Create API token"

  ![Create JIRA API](/img/bug-tracking/jira-create-api.png)

1.2 Label the new token "TestFairy".

  ![Set TEstFairy JIRA Key](/img/bug-tracking/jira-label.png)

1.3 Copy the API Token.

  ![Copy token](/img/bug-tracking/jira-token.png)

## 2. Configure JIRA in your TestFairy settings:

2.1. Open your TestFairy account Preferences

  ![Open TestFairy preferences](/img/bug-tracking/jira-cloud-1.png)

2.2 Choose "Integrations" -> and scroll to "JIRA" and press the `Add integration` Button.

  ![](/img/bug-tracking/jira-cloud-1-1.png)


2.3 In the next screen enter your JIRA Username, API Token and JIRA URL. Press the `Update Jira Settings` button when done.

  ![Configure JIRA cloud](/img/bug-tracking/jira-cloud-2.png)


## 3. (optional) Install the TestFairy Chrome Extension

The TestFairy Chrome Extension is available [here](https://chrome.google.com/webstore/detail/testfairy-for-jira/joaafaemekbkgekhjbaldlllcnjifcee). With this Chrome extension, every JIRA issue that has a link to a TestFairy session will contain the right TestFairy session, timeline, logs, and crash reports enbedded in the JIRA issue.

## 4. (optional, if you didn't install the Chrome extension) Add The TestFairy JIRA Add-on to your JIRA account

The TestFairy JIRA Add-on adds TestFairy videos to JIRA issues.

In order to install it please follow these steps:

4.1. Open JIRA Settings

  ![JIRA-settings](/img/bug-tracking/jira-settings.png)

4.2 Open Apps

  ![JIRA-settings](/img/bug-tracking/jira-settings1.png)

4.3 In the Apps manu press 'Find new apps'

  ![JIRA-apps](/img/bug-tracking/jira-find-apps.png)

4.4 Add "TestFairy for Jira" to your account.

  ![JIRA-testfairy app](/img/bug-tracking/jira-discover.png)

4.5 On the first issue that is created, click on the "3 dots" icon and choose "TestFairy Session"

  ![JIRA-testfairy app](/img/bug-tracking/jira-3-dots.png)


## This is how JIRA issues look After the installation

  ![JIRA-setup](/img/bug-tracking/hira6a.png)
  ![JIRA-setup](/img/bug-tracking/jira5b.png)
  ![JIRA-setup](/img/bug-tracking/jira6c.png)

## 5. (optional ,highly recommended) Map JIRA Custom Fields.

The TEstFairy JIRA integration allows you to automatically populate any field in JIRA when creating a new issue.
You can do that with standard TestFairy data like app name, version, user, device etc. or with your own seesion attributes, any key and value you push to our SDK in real time.
In order to map [follow these steps](How_To_Map_JIRA_Custom_Fields.html)

## JIRA Server
## Before you start

In order to connect TestFairy to JIRA Server that is installed on-prem, start by [installing TestFairy Connect](/Bug_Tracking/TestFairy_Connect.html)

## Configuring TestFairy Connect with JIRA Server

This guide explains how to configure the TestFairy Connect agent to work with an on-premise JIRA using basic-authentication (user/password-token) or OAuth.

#### Using the wizard

Start the wizard by typing the following command in your terminal or command prompt:

```sh
$ testfairy-connect configure
```

**Welcome to TestFairy Connect configuration wizard.**

- **What is your TestFairy API Key?**

  Please put your Upload API key here, you can access it via the [Settings Page](https://app.testfairy.com/settings/#api-key)

- **What kind of issue tracking system will you use with TestFairy Connect?**

  Choose "JIRA"

- **What is your JIRA URL (e.g. https://example.atlassian.net)?**

  Please provide the url address of your JIRA server. Don't forget to include the http:// or https:// prefix.

- **How shall TestFairy Connect authenticate to JIRA?**

  Please choose "basic"

- **What is the type of JIRA issues to be created using TestFairy Connect?**

  Please choose to appropriate issuetype used in your JIRA. By default, JIRA uses "Bug", but it varys on project type. Other examples are "Defect" or "Task".

- **JIRA username:**

  Please enter your JIRA login username

- **JIRA password:**

  And your JIRA login password

  	- Somtimes, depending on your user definitions in JIRA, you may need to use an API token as your password. You can creat one here: <a hfer="https://id.atlassian.com/manage/api-tokens" target="_blank">https://id.atlassian.com/manage/api-tokens</a>

- **Please enter HTTP proxy server address, leave empty if none:**

  If you require HTTP proxy to access this JIRA server, please send it here. For example, http://user@10.0.0.1:8080.

#### Congratulations!

When done, the configuration wizard will display the success message: **Successfully connected to issue tracker.**

Congratulations, you have successfully configured TestFairy Connect with JIRA using basic authentication. Next, [start the agent from command line](https://docs.testfairy.com/Bug_Tracking/TestFairy_Connect.html)


---------------------------------

## Configure JIRA with OAuth

#### Access token & secret generation:

1. Obtain a keypair:

	```
	openssl genrsa -out jira_rsa 2048
	openssl rsa -in jira_rsa -pubout > jira_rsa.pub
	```

2. Configure JIRA the Application Link for TestFairy Connect integration.
In your browser, go to your JIRA Admin page, like http://localhost:2990/jira/plugins/servlet/applinks/listApplicationLinks.
Enter 'url' or any string to use for Application Link identification.

  ![Create an Application Link](https://docs.testfairy.com/img/testfairy-connect/1-create-application-link.png)

  In the next screen, click 'Continue'.

  ![Continue](https://docs.testfairy.com/img/testfairy-connect/2-continue.png)

  ![Setup Application Link](https://docs.testfairy.com/img/testfairy-connect/3-setup-application-link.png)

  - Application Name: TestFairy
  - Application Type: Generic Application
  - Service Provider Name: TestFairy
  - Consumer Key: testfairy-connect
  - Shared Secret: [paste public key contents here]
  - Request Token URL: /plugins/servlet/oauth/request-token
  - Request Token URL: /plugins/servlet/oauth/access-token
  - Request Token URL: /plugins/servlet/oauth/authorize

  ![Verify Access Token](https://docs.testfairy.com/img/testfairy-connect/4-verify-access-token.png)

3. Run the token generation script found [here](https://docs.testfairy.com/js/download/oauth.js). Right-click to copy .js file path.

	```
	wget [paste file path here]
	npm install oauth
	node oauth.js
	```

4. Update your config.json with `access_token` and `access_token_secret`.


5. (optional) Install the TestFairy Chrome Extension

The TestFairy Chrome Extension is available [here](https://chrome.google.com/webstore/detail/testfairy-for-jira/joaafaemekbkgekhjbaldlllcnjifcee). With this Chrome extension, every JIRA issue that has a link to a TestFairy session will contain the right TestFairy session, timeline, logs, and crash reports enbedded in the JIRA issue.





## Github
Connetcing your GitHub issues

1. Go to your account **Preferences** under your account email (right side of screen) - select **Integrations**.

  ![alt](../../img/bug-tracking/Github1.png)

2. Scroll to **GitHub Issues** and press the `Add integration` button to start the **OAuth** process

  ![](../../img/bug-tracking/Github2_1.png)

3. Press the `Authorize GitHub via OAuth` Button and wait for the __OAuth__ process to finish.

  ![alt](../../img/bug-tracking/Github2.png)

3. After connecting to your Github account, for each app, you can select a repository:

  ![alt](../../img/bug-tracking/Github3.png)

* Make sure to press the _**Update GitHub Settings**_ button when you choose or update a repository.

## Trello
Connect TestFairy to Trello

1. Open your TestFairy account Preferences


  ![Menu](/img/bug-tracking/jira-cloud-1.png)

2. Click on "Integhrations" and scrolle down to choose "Trello", and press the `Add Integrations` button.


  ![JIRA-setup](/img/bug-tracking/trello1.png)

3. In this screen add the Trello __API Key__ and __Token__ and then prss `Update Trello Settings` :


  ![](/img/bug-tracking/trello2.png)


## TestFairy Connect
What is TestFairy Connect?

TestFairy Connect is a proxy server installed on-premise, designed to help companies connect their bug tracking systems running behind a firewall (JIRA Server), with the TestFairy cloud.

Test Fairy Connect is installed using a Docker image.

## How does it work?

The key part of TestFairy Connect is the agent service that runs on a system, within your firewall, connecting to TestFairy's web app and to your bug tracking system.

![Overview](/img/testfairy-connect/0-overview.png)

## How to Install TestFairy Connect (video tutorial)

<iframe width="560" height="315" src="https://www.youtube.com/embed/SdEHd8jNsOM" frameborder="0" allowfullscreen></iframe>

## Installation

Let's configure TestFairy Connect.

This is needed only once. Docker will automatically download the latest version.

```sh
docker run -i -t -v $PWD:/etc/testfairy-connect testfairy/testfairy-connect:latest configure
```

Note: you can replace `$PWD` with a directory of your choice to store your TestFairy Connect configuration.

If there are no issues, you can now follow the interactive configuration wizard that is displayed on the screen.

## Configuration

To configure TestFairy Connect you will need the following data:

* TestFairy API key (found at [https://[your-subdomain].testfairy.com/settings/api-key/](https://[your-subdomain].testfairy.com/settings/api-key/)
* The URL to your bug system.
* In the case of a JIRA basic authentication - valid credentials (UserName/API Token) for the JIRA user.
* In the case of a JIRA oauth authentication - admin access to JIRA/the ability to manage Application Links (as described in the configuration wizard script).

By default, your configuration file `config.json` is saved to `.testfairy-connect` under the Dockers Image home directory: `~/.testfairy-connect/config.json`

## Running

Now that you have TestFairy Connect configured, run it with:

```sh
docker run -d -v $PWD:/etc/testfairy-connect --restart=always testfairy/testfairy-connect:latest run
```

Note: you can replace `$PWD` with a directory of your choice to store your TestFairy Connect configuration.

TestFairy Connect will be running in the background, and it is safe to close the ssh connection. Please remember that stopping docker or rebooting the server, will require you to run the 'start' command again.

## Troubleshooting

#### SELinux
If you are having permission errors related to your docker volume, you can either try attaching volume in relaxed SELinux mode or disable SELinux enforcement entirely.

  - Use these commands to attach volume in relaxed SELinux mode:


```sh
docker run -i -t -v $PWD:/etc/testfairy-connect:z testfairy/testfairy-connect:latest configure
docker run -d -v $PWD:/etc/testfairy-connect:z --restart=always testfairy/testfairy-connect:latest run
```

  - Alternatively, you can disable SELinux altogether by running:

```sh
sudo setenforce 0
```

## Micro Focus ALM Octane
Connecting Micro Focus ALM Octane to TestFairy

1. Go to your [__Integrations__](https://app.testfairy.com/settings/integrations/) page.


2. Scoll the list to the __Micro Focus ALM Octane__ line and press the `Add Integration` button.
![](/img/bug-tracking/ALM-1.png)


3. Now, go to your __ALM Octane__ workspace and navigate to the __API ACCESS__ tab.
You can use an existing Api Access if you have its `API key(Client ID)` and `API password (Client secret)` or create a new one.
![](/img/bug-tracking/ALM-2.png)


4. Copy the `API key(Client ID)` and `API password (Client secret)` from your workspace to the fields in the __Bug System Configuration__ screen.
![](/img/bug-tracking/ALM-2_1.png)

5. Copy your workspace number (you can find it in the URL of the workspace after `?admin&p=`.
The link in the URL field should be: `https://almoctane-eur.saas.microfocus.com/api/shared_spaces/[INSERT WORKSPACE NUMBER HERE]/`.


6. Press `Save` to save the configuration.
![](/img/bug-tracking/ALM-3.png)


7. Scroll down and press `Actviate` for the app you want to connect to a workspace.


8. In the window select the target workspace for your issues in the __Project Key__ field and `Save Changes`.
![](/img/bug-tracking/ALM-4.png)


9. When you returne to the apps screen the workspace is mapped to the app.
![](/img/bug-tracking/ALM-5.png)

## How To Map JIRA Custom FieldsHow to map JIRA custom fields?

First you will need to connect a JIRA account. Follow the [instructions here](https://docs.testfairy.com/Bug_Tracking/JIRA_Cloud.html)

Choose one of your apps you want to connect and press the `Activate` button.

![jira projects](/img/bug-tracking/jira-connect-proj-map1.png)

Here you can configure the JIRA fields:

![fields configuration](/img/bug-tracking/jira-proj-fileds-config.png)

In the JIRA configuration screen choose the project (**Project Key**) you want to connect:

![jira project](/img/bug-tracking/jira-project-select.png)

Once the project is selected, select the issue type you want to configure:

![jiras issue](/img/bug-tracking/issue-type-select.png)

If you want to first test the connection to the JIRA project you can Press the `TEST` button to validate the JIRA issue creation.

You will get a pop-up window with the response. Make sure you get a valid JIRA link.
In case you get a **PENDING** response check the connection configuration.

![test success](/img/bug-tracking/jira-connect-test-ok.png)

Each **Issue type** has different fields associated with it:

* **Name** - the field name.
* **Type** - the type of field as defined in the JIRA system.
* **Value** - the values from the JIRA system (* in addition to predefined fixed values and  -Dynamic value-, see below)
* **Required?** - is the field required or optional.

<!---[jira values](/img/bug-tracking/jira-values-drop-down1.png)--->

![](/img/bug-tracking/jira-requiered-fildes-mark.png)

When defining fields in the Configure Fields window follow the below conventions:
- When you choose a field from a drop down this field as is (text) will be populated in the corresponding JIRA field in the issue opened.

![values drop down](/img/bug-tracking/jira-values-drop-down.png)

- You can also choose from the fixed predefined values in the list below:
  * `{user.id}` - the UserId of the session running.
  * `{session.timestamp}` - the timestamp of the session.
  * `{session.url}` - the url of the session on the TestFairy dashboard.
  * `{session.ipAddress}` - the IP address of the device running the session.
  * `{device.os}` - the running device OS
  * `{device.model}` - the device model of the handset
  * `{device.osVersion}` - the OS version on the device (if the iPhone is running version IOS 12 value=12)
  * `{app.name}` - the app name.
  * `{app.version}`  - the _versionName_ or _CFBundleShortVersionString_ of the build. example: 1.7.0
  * `{app.fullVersion}` - the _versionName_ + (_versionCode_ or _CFBundleVersion_) of the build. example: 1.7.0 (1700)
  * `{feedback.text}` - the feedback message
  * `{feedback.timestamp}` - the timestamp of the feedback (absolute)
  * `{feedback.relTimestamp}` - relative timestamp of the feedback (mm:ss) since session started

In order to use these values add them to the `-Dynamic value-` field that opens when you select the **-Dynamic value-** option like so:

![fixed values](/img/bug-tracking/jira-fixed-attr-popup.png)

- You can also add attributes that are defined in your apps code to the `-Dynamic value-` field. The structure of a dynamic field is as follows: `{attr.[attribute_name]||[default_value]}`
  * `attribite_name` - is the name of the Teasfairy attribute set in the code by the `TestFairy.setAttribute` function. What passes to the JIRA is the value of this attribute.
  * `default_value` -  for each attribute you can set a default value so if you receive a null or wrong attribute value from the code (not possible in this field in JIRA) the default value will instead be passed to JIRA.

![attribute setting](/img/bug-tracking/jira-dynamic-attr-setattr.png)
