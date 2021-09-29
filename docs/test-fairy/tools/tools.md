---
id: tools
title: Tools
sidebar_label: Tools
---
## TestFairy Fetch Sessions tool
Download link: [TestFairy Fetch Sessions](https://github.com/testfairy/testfairy-fetch-sessions/)

### About

This tool downloads screenshots and/or logs from recorded TestFairy sessions.
Use this to download data you want to analyze with your own toolchain or to import to your own analytics systems.

### Installation

`npm install -g --link git+https://github.com/testfairy/testfairy-fetch-sessions.git`

If you receive the error: "Could not create leading directories", then you should run the same command with `sudo -s` prefix.

### Usage

`testfairy-fetch-sessions --endpoint "acme.testfairy.com" --user "john@example.com" --api-key "0123456789abcdef" --project-id=1000 --logs --screenshots`

The example above would connect to endpoint `acme.testfairy.com` (which can be a private cloud installation, a public cloud installation, or an on-premise installation.) It will use the credentials of `user` and `api-key`.

Since both `--logs` and `--screenshots` are possible, the tool can download all **screenshots** and all **logs** from app's project 1000.

You can create an **MP4 video** using all the downloaded screenshots by passing `--video` along with `--screenshots`.

You can find the id of the project (app) you want to download by examining the url (for example: https://app.testfairy.com/projects/1000/).

TestFairy Fetch Sessions tool is incremental in downloads - this means that you can run the tool multiple times, and it will only download new sessions that were recorded.

For Support we're available at [support@testfairy.com](mailto:support@testfairy.com).

# Downloading Encrypted Logs

If you are encrypting your sessions, and want to download the logs from a given project, you must pass the path to a file containing the private key into the `--rsa-private-key` argument.

`testfairy-fetch-sessions --endpoint "acme.testfairy.com" --user "john@example.com" --api-key "0123456789abcdef" --project-id=1000 --logs --screenshots --rsa-private-key "/path/to/rsa-private.pem"`

### Parameters

| key             | description                                                        | default          |
|-----------------|--------------------------------------------------------------------|------------------|
| help            | Display usage                                                      |                  |
| version         | Display fetch-session version                                      |                  |
| project-id      | Project ID                                                         | * required       |
| user            | TestFairy Account Email                                            | *                |
| api-key         | API key from https://app.testfairy.com/settings/api-key            | *                |
| endpoint        | TestFairy endpoint (private servers only)                          | *                |
| rsa-private-key | Path to RSA private key (only required if sessions are encrypted)  |                  |
| logs            | Fetch logs from sessions of given project                          |                  |
|  screenshots    | Fetch screenshots from sessions of given project                   |                  |
| video           | Fetch screenshots                                                  |                  |
| all-time        | Fetch all sessions for a given project                             | Last 25 sessions |
| json            | Outputs logs as json result along with meta data information       | Only Logs        |
| overwrite       | Overwrites any downloaded                                          | false            |

## TestFairy Video Tutorials
The TestFairy Platform

[Full demo (6:40 mins)](https://youtu.be/K5Ctsh65BCY)

<!---* [Signing up to TestFairy](https://testfairy.fleeq.io/l/1rfum3nb5d-bw5iw8zq2w){target="_blank"}--->

* <a href="https://testfairy.fleeq.io/l/1rfum3nb5d-bw5iw8zq2w" target="_blank">Signing up to TestFairy</a>

* <a href="https://testfairy.fleeq.io/l/wdtj0svxnh-xftb9kmde0" target="_blank">How to upload a new app or version</a>

* <a href="https://testfairy.fleeq.io/l/4vaf26t35u-pd0iztdypt" target="_blank">Insights Tab and session filtering</a>

* <a href="https://testfairy.fleeq.io/l/1tvmj34u5q-r1ck6l9wd6" target="_blank">Getting to know your Dashboard</a>

* <a href="https://testfairy.fleeq.io/l/aftiqrzoh4-b55x03f9fv" target="_blank">Application build settings</a>

* <a href="https://testfairy.fleeq.io/l/9162234x94-qc3qn71j97" target="_blank">How to distribute your app to testers</a>

* <a href="https://youtu.be/INsKsWAV8mo?t=101" target="_blank">How to submit feedback</a>

* <a href="https://youtu.be/INsKsWAV8mo?t=141" target="_blank">How to review your received feedback</a>


# TestFairy for iOS

* [How to integrate TestFairy SDK for iOS](https://youtu.be/DhRX5UukvPM)

* [How to upload iOS .IPA from command line on Mac](https://youtu.be/LpSXACFVIeI)

* [Using TestFairy with React-Native (iOS)](https://youtu.be/HpLOsNwd_FM)

* [How to automatically upload .dSYM from Xcode](https://youtu.be/E64kWHOMgVY)

* [How to add UDIDs to provisioning profile](https://youtu.be/omYf_-KjPE0)


# TestFairy for Android

* [How to Upload Android .APK from Windows](https://youtu.be/7wg07Q7TYbA)

* [How to Upload Android APK from Command Line on Mac](https://youtu.be/_eV-B1HfV8E)


# Integrations

* [TestFairy Connect with on-premise Jira](https://youtu.be/SdEHd8jNsOM)
