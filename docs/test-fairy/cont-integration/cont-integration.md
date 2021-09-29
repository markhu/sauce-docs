---
id: cont-integration
title: Continuous Integration
sidebar_label: Continuous Integration
---
## Continuous Integration
Continuous Integration plays an important role in delivering faster and better apps.

The following platforms are officially supported. We also offer an [Upload API](../API/Upload_API.html), making it easier and available for any platform and build script.

| | |
|:-:|-|
|![jenkins](../img/continuous-integration/jenkins-logo.png) | [Jenkins](Jenkins.html)|
|![Travis CI](../img/continuous-integration/travis-ci-logo.png) | [Travis CI](Travis_CI.html)|
|![Bitbucket Pipelines](../img/continuous-integration/bitbucket-pipelines-logo.png) | [Bitbucket Pipelines](Bitbucket_Pipelines.html)|
|![Gradle](../img/continuous-integration/gradle-logo.png) | [Gradle](Gradle.html)|
|![CircleCI](../img/continuous-integration/circleci-logo.png) | [CircleCI](CircleCI.html)|
|![Bamboo](../img/continuous-integration/bamboo-logo.png) | [Bamboo](Bamboo.html)|
|![Upload API](../img/continuous-integration/cloud-icon.png) | [Upload API](../API/Upload_API.html)|
|![Fastlane](../img/continuous-integration/fastlane-logo.png) | [Fastlane](Fastlane.html)|
|![Command line interface](../img/continuous-integration/command-line-icon.png) | [Command line interface](https://github.com/testfairy/command-line-uploader/blob/master/testfairy-uploader.sh)|
|![VSTS](https://github.com/testfairy/docs/blob/master/img/integrations/vsts/VSTS-icon.png?raw=true) | [VSTS](https://docs.testfairy.com/Continuous_Integration/Visual_Studio_Team_Services.html)|
|![GitLab](../img/continuous-integration/gitlab.jpg) | [GitLab](GitLab.html)|
|![TeamCity](../img/continuous-integration/teamcity.png) | [TeamCity](TeamCity.html)|

<style>table thead {display: none; text-align: center;}</style>
<style>img {max-height: 70px !important; border: none !important; box-shadow: none !important;}</style>

## Jenkins
Jenkins documentation is available [here](https://plugins.jenkins.io/TestFairy)
## Gradle
Page moved to [https://github.com/testfairy/testfairy-gradle-plugin](https://github.com/testfairy/testfairy-gradle-plugin)
## Travis CI
Travis CI can automatically deploy your Android and iOS Apps to TestFairy.

Travis documentation is available [here](https://docs.travis-ci.com/user/deployment/testfairy)
## CircleCI
[circleCI](https://circleci.com) is a cloud based CI/CD service that helps developers automate their development process with CI hosted in the cloud or on a private server.

TestFairy has a CircleCI "ORB" that allows you to easily upload builds to TestFairy.

In order to use the ORB, add the following line to the `orbs` section of your `.circleci/config.yml`:

```yml
orbs:
 testfairy: testfairy/uploader@2.0.1
```

Then, in order to upload your IPA or APK, you'll have to call `testfairy/uploader` providing the path to the file and your API key. As an example of creating add the following command:

```yml
jobs:
  build:
    # ...
    steps:
      # ... steps to build IPA or APK
      - testfairy/uploader:
          api-key: TESTFAIRY_API_KEY
          file: app.apk
```

Where TESTFAIRY_API_KEY is name environment variable that contains your API key. Environment variables is the best practice so you don't commit secret values into your code repository.

You can see the full list of supported commands by visiting the [CircleCI TestFairy ORB Repository](https://circleci.com/orbs/registry/orb/testfairy/uploader).


## Bitbucket Pipelines
Set up Bitbucket Pipelines to upload your build artifacts (IPA or APK) directly to TestFairy for distribution.

## Setting up

1. Open your Bitbucket repository, and select *Settings* -> *Pipelines* -> *Environment Variables*

  ![Screenshot of Bitbucket Pipelines](https://docs.testfairy.com/img/integrations/pipelines/bitbucket-pipelines-0.png)

2. Fill in variable, value fields:

  - **Variable**: TESTFAIRY_API_KEY
  - **Value**: *Your API application key. See https://app.testfairy.com/settings for details.*
  - **Secured**: Y

  When done, click the *Add* button.

  ![Screenshot of Bitbucket Pipelines](https://docs.testfairy.com/img/integrations/pipelines/bitbucket-pipelines-1.png)

3. Edit your `bitbucket-pipelines.yml` and add this command to your `script` section:

  ```
  curl https://app.testfairy.com/api/upload -F api_key=${TESTFAIRY_API_KEY} -F file=@MyApplicationFile.apk -F format=readable
  ```

  **NOTE:** Do not forget to replace `MyApplicationFile.apk` with path to your APK or IPA files.

  Additional optional parameters such as `testers-groups`, `notify` and `comment` can be added to this line. Please refer to the [TestFairy Upload API reference guide](https://docs.testfairy.com/API/Upload_API.html) for more information and examples.

  Here, for example, is a screenshot of a sample `bitbucket-pipelines.yml` file:

  ![Screenshot of Bitbucket Pipelines](https://docs.testfairy.com/img/integrations/pipelines/bitbucket-pipelines-2.png)

## Bamboo
Continious integration with Bamboo is easy to set up, and when ready, allows you to deliver up-to-date releases to your beta-testers and co-workers.

### Installation

1. Log in to your Bamboo server
2. Click on the **cogs icon** and select `Add-ons`
3. Click `find new add-ons` link, and install the *TestFairy Uploader* add-on.

![Alt](https://docs.testfairy.com/img/integrations/bamboo/bamboo_00.png)

Now that you have the add-on installed on your server, we will configure it with our `upload API key`. You can find this API key in your **Preferences Page** at [https://app.testfairy.com/settings/](https://app.testfairy.com/settings/).

In your Android or iOS job, create a new task, and pick `TestFairy Uploader` from *Deployment* category.
![Alt](https://docs.testfairy.com/img/integrations/bamboo/bamboo_01.png)

Now configure the API key as so:
![Alt](https://docs.testfairy.com/img/integrations/bamboo/bamboo_02.png)

Notice you must provide the path to the compiled .IPA or .APK file, and optionally list group names of testers for sending out email invitations.

Vôila!

## Fastlane
Page moved [here](https://docs.fastlane.tools/actions/testfairy/)
## GitLab
GitLab can automatically deploy your Android or iOS Apps to [TestFairy](https://www.testfairy.com/).

* On the TestFairy dashboard, navigate to the __Preferences --> [Upload API Key](https://app.testfairy.com/settings/api-key)__ page.
  ![](https://docs.testfairy.com/img/continuous-integration/testfairy_upload_key.png)


* Copy your API key and go to your application's project __Settings --> CI/CD -- Variables__ in GitLab. Add a variable called `TESTFAIRY_API_KEY` to the list with the value of your __Upload API key__.
  ![](https://docs.testfairy.com/img/continuous-integration/gitlab_secret_keys.png)


* To deploy, add a job to your `.gitlab-ci.yml` configuration using [fastlane](https://docs.fastlane.tools/getting-started/ios/beta-deployment/) or `curl` (example below).
``` yaml
stages:
  - deploy

deploy:
  stage: deploy
  only:
  - master
  script:
  - |
    curl \
      -A "GitLab CI" \
      -F api_key="${TESTFAIRY_API_KEY}" \
      -F comment="GitLab Pipeline build ${CI_COMMIT_SHA}" \
      -F file=@android.apk \
      https://upload.testfairy.com/api/upload/
```

**Note** Be sure to replace the `-F file=@android.apk` argument with a path to your own APK or IPA.

For a complete list of available options, please visit the [TestFairy Upload API documentation](https://docs.testfairy.com/API/Upload_API.html)

## TeamCity
TeamCity can automatically deploy your Android and iOS Apps to [TestFairy](https://www.testfairy.com/).

* On the TestFairy dashboard, navigate to the Preferences page.
  ![](https://docs.testfairy.com/img/continuous-integration/testfairy-open-preferences.png)

* On the Preferences page, go to the API Key section and copy the API key.
  ![](https://docs.testfairy.com/img/continuous-integration/testfairy_upload_key.png)

* In TeamCity, add a environment variable as a **New Parameter** in to the **Build Configuration**
  ![](https://docs.testfairy.com/img/continuous-integration/teamcity-configuration-4.png)

* Name the parameter `env.TESTFAIRY_API_KEY` and give it the value you copied from the TestFairy preferences page, and Save.
  ![](https://docs.testfairy.com/img/continuous-integration/teamcity-configuration-5.png)

* Add a **Build Step** to the **Build Configuration** you wish to deploy from.
  ![](https://docs.testfairy.com/img/continuous-integration/teamcity-configuration-1.png)

* Make sure to select a **Command Line** build step.
  ![](https://docs.testfairy.com/img/continuous-integration/teamcity-configuration-2.png)

Copy the following command into **Custom script** text field

```
curl https://upload.testfairy.com/api/upload -F api_key=${env.TESTFAIRY_API_KEY} -F comment="TeamCity build" -F file=@android.apk
```

**Note** Be sure to replace the `-F file=@android.apk` argument with a path to your own APK or IPA.

For a complete list of available options, please visit the [TestFairy Upload API documentation](https://docs.testfairy.com/API/Upload_API.html)

## Visual Studio Team Services
This doc will help VSTS users to upload apps (*.apk/*.ipa) to TestFairy.

Adding UploadToTestFairy (or any other task name) to your existing build:

* Go to "Edit Build Definitions"
  ![](https://docs.testfairy.com/img/integrations/vsts/Edit%20Build%20Definitions.png)

* Add Commmand Line tool task
  ![](https://docs.testfairy.com/img/integrations/vsts/add%20command%20line%20task.png)

* Configure the task and add the following line to arguments:

```
https://upload.testfairy.com/api/upload -F api_key=abcdabcdgfdsgfds56 -F file=@sample.apk
```

**Note** Make sure you replace the api_key to yours

![](https://docs.testfairy.com/img/integrations/vsts/Configure%20the%20task.png?raw=true)

## Microsoft App Center
In order to upload apps from Microsoft App Center to TestFairy, please do the following:

## 1. Create an upload script.

Create a new file, call it `appcenter-post-build.sh` and add it next to the project file in your repository.

```
#!/usr/bin/env bash

TESTFAIRY_UPLOAD_API_KEY=1234356

if [[ "$APPCENTER_XCODE_PROJECT" ]]; then
  curl https://upload.testfairy.com/api/upload \
  -F "api_key=$TESTFAIRY_UPLOAD_API_KEY" \
  -F "file=@$APPCENTER_OUTPUT_DIRECTORY/example.ipa"
fi

if [[ -z "$APPCENTER_XCODE_PROJECT" ]]; then
  curl https://upload.testfairy.com/api/upload \
  -F "api_key=$TESTFAIRY_UPLOAD_API_KEY" \
  -F "file=@$APPCENTER_OUTPUT_DIRECTORY/example.apk"
fi

```


## 2. Verify a Post Build Step exists.


App-center will use this file as a `post build script` for your project, so your app gets uploaded aytomatically.


![](/img/continuous-integration/appcntr-1.png)
