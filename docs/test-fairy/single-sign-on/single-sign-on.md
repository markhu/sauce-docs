---
id: single-sign-on
title: Single Sign-On
sidebar_label: Single Sign-On
---
## SSO
Single Sign-on enables you to manage users and testers outside of TestFairy.
TestFairy supports SAML and is fully compatible with Okta, OneLogin, Ping, Oracle, IBM and Azure ADFS.

When SSO is configured into your account, the login page is replaced with a simple login with sso button.

There are several SAML / SSO providers that you can creat integrations to:

| | |
|:-:|-|
|![OKTA](../img/sso/Okta_Logo.png) | [OKTA](OKTA.html)|
|![OneLogin](../img/sso/onelogin-logo.png) | [OneLogin](OneLogin.html)|
|![Azure Active Directory](../img/sso/azure-logo.png) | [Azure Active Directory](Azure_Active_Directory.html)|
|![Google](../img/sso/google-apps-logo.png) | [Google Apps](Google.html)|
|![PingIdentity](../img/sso/pingidentity-logo.png) | [Ping Identity](Ping_Identity.html)|

<style>table thead {display: none;}</style>
<style>img {max-width: 70px !important; border: none !important; box-shadow: none !important;text-align: center !important;}</style>

## OKTA
Single Sign-on enables you to manage users and testers outside of TestFairy. A list of permitted users and testers, as well as their passwords, is stored in OKTA. Therefore onboarding a new developer into the team is an easy task.

Talk to us! Visit here to [Request a Demo](https://www.testfairy.com/contact_us.php).

#### Setting up OKTA in your account

- Login to OKTA, click on 'Admin' and pick 'Add Applications' from the right sidebar:
  ![](https://docs.testfairy.com/img/sso/okta/okta-1.png)

- Type "TestFairy" into the search form:
  ![](https://docs.testfairy.com/img/sso/okta/okta-2.png)

- And click "Add" on the TestFairy app:
  ![](https://docs.testfairy.com/img/sso/okta/okta-3.png)

- Now type in the name of the team in TestFairy (it is also the name of the subdomain):
  ![](https://docs.testfairy.com/img/sso/okta/okta-4.png)

- Next, select authorized users. When done, click "Next":
  ![](https://docs.testfairy.com/img/sso/okta/okta-5.png)

- OKTA-side configuration is done. Now click "Next":
  ![](https://docs.testfairy.com/img/sso/okta/okta-6.png)

- In the "Sign On" menu, click on "View Setup Instructions":
  ![](https://docs.testfairy.com/img/sso/okta/okta-7.png)

- Copy "ID Provided Metadata" from section 4 into your clipboard:
  ![](https://docs.testfairy.com/img/sso/okta/okta-8.png)

- Now login to https://app.testfairy.com, and open the "Preferences" page:
  ![](https://docs.testfairy.com/img/sso/okta/okta-9.png)

- In the 'Security' manu item "SAML/Single Sign-on" section, paste the copied 'ID Provided Metadata' into the text area:
  ![](/img/sso/okta/security-saml-okta-xml.png)

- TestFairy-side configuration is also done:
  ![](https://docs.testfairy.com/img/sso/okta/okta-11.png)

Now, please logout and if SSO is configured into your account, the login page is replaced with a simple `login with sso` button.

![login screenshot](https://docs.testfairy.com/img/sso/sso-login-screenshot.png)


#### [Optional:] Automatically importing groups from OKTA

When managing large teams with OKTA, it is most likely that people are already associated with groups.

For example, say Alice is associated with the following groups in OKTA: ["QA", "QA San Francisco"]. With auto-import of groups, she will be automatically be associated with the following groups in TestFairy next time she signs in: "okta", "okta-qa", and "okta-qa-san-francisco". If she was removed from group "QA", she will be automatically be removed from "okta-qa" group in TestFairy, the next time she signs in.

To import groups each time a user signs into TestFairy, please follow these instructions.

- Open the TestFairy app in your OKTA account, select `General` tab, and click `Edit`. In `SAML Settings` section, under `Group Attribute Statements`, add a rule with name: "groups", (LOWERCASE!!!) and filter "Matches regex" with value `.*`. (dot asterisk) See screenshot:
  ![](/img/sso/okta/okta-groups-2.png)

- When done, please click on `Update Now` so OKTA updates caches. See screenshot:
  ![](/img/sso/okta/okta-groups-1.png)

That's it!
Need our assistance? Don't hesitate to [contact support](https://www.testfairy.com/contact_us.php).

## OneLogin
Single Sign-on enables you to manage users and testers outside of TestFairy. A list of permitted users and testers, as well as their passwords, is stored in OneLogin. Therefore onboarding a new developer into the team is an easy task.

When SSO is configured into your account, the login page is replaced with a simple login with sso button.

Talk to us! Request a demo at https://testfairy.com/products/solutions/enterprise#request-a-demo

#### Setting up OneLogin in your account

- Login to OneLogin, click on the 'NEW APP' button on the right:
  ![](https://docs.testfairy.com/img/sso/onelogin/onelogin-1.png)

- Type in "TestFairy" in the search box, and select the application:
  ![](https://docs.testfairy.com/img/sso/onelogin/onelogin-2.png)

- Click 'Save', no need to change configuration:
  ![](https://docs.testfairy.com/img/sso/onelogin/onelogin-3.png)

- Type in your TestFairy subdomain (for example, acme), under the 'Configuration' tab. Then, click "Save":
  ![](https://docs.testfairy.com/img/sso/onelogin/onelogin-4.png)

- Click on "More Actions" and select "SAML Metadata". This will download a file to your computer:
  ![](https://docs.testfairy.com/img/sso/onelogin/onelogin-5.png)

- Now login to TestFairy, and select "Preferences":
  ![](https://docs.testfairy.com/img/sso/onelogin/onelogin-6.png)

- Copy the contents of the file you've just downloaded, and paste it into the textbox. Click on "Update":
  ![](https://docs.testfairy.com/img/sso/onelogin/onelogin-7.png)

- TestFairy-side configuration is now done.
  ![](https://docs.testfairy.com/img/sso/onelogin/onelogin-8.png)

Now please logout, and make sure you see the "Login with SSO" button.

## Ping Identity
Single Sign-on enables you to manage users and testers outside of TestFairy. A list of permitted users and testers, as well as their passwords, is stored in PingIdentity. Therefore onboarding a new developer into the team is an easy task.

When SSO is configured into your account, the login page is replaced with a simple `login with sso` button.

Talk to us! Request a demo at https://testfairy.com/products/solutions/enterprise#request-a-demo

#### Setting up Ping Identity in your account

- Login to Ping Identity's admin dashboard. Click on 'Add Application' and select 'Search Application Catalog':
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-1.png)

- Type "TestFairy" into the search box, and select the application. Click on the "expand" arrow.
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-2.png)

- Click on 'Setup'. There is no need to change configuration:
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-3.png)

- Click on "Continue to Next Step"
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-4.png)

- Type in the ACS URL and Entity ID. For *ACS URL*, please use the following format `https://acme.testfairy.com/login/sso`, and replace 'acme' with your own subdomain.

For *Entity ID*, please use the same format `https://acme.testfairy.com`. and again, replace 'acme' with your own subdomain.
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-5.png)

- Click on "Continue to Next Step", no other configuration need to be changed.
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-6.png)
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-7.png)

- Click on "Save & Publish", and then click on "Finish"
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-8.png)
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-9.png)

- Next, download "SAML Metadata".
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-10.png)

- Now login to TestFairy, and select Preferences.
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-11.png)

- Copy the contents of the file you just downloaded, and paste it into the textbox. Click on "Update":
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-12.png)

- TestFairy-side configuration is now done!
  ![](https://docs.testfairy.com/img/sso/pingidentity/ping-identity-13.png)

Now please logout, and makre sure you see the "Login with SSO" button.

## Azure Active Directory
Setting up Azure Active Directory in your account


Single Sign-on enables you to manage users and testers outside of TestFairy.
A list of permitted users and testers, as well as their passwords, is stored in Azure Active Directory.

Therefore onboarding a new developer into the team is an easy task.

When SSO is configured into your account, the login page is replaced with a simple `login with sso` button.

Talk to us! Request a demo at [https://testfairy.com/products/solutions/enterprise#request-a-demo](https://testfairy.com/products/solutions/enterprise#request-a-demo)

#### Adding an enterprise app


- In your Home screen press the **Azure Active Directory** icon to open the **Directory overview**.

  ![](/img/sso/azure/azure-ad-1.png)

- From the menu options select the **`Enterprise Application`** option.

  ![](/img/sso/azure/azure-ad-2.png)

- Press the **`+Add application`** button.

  ![](/img/sso/azure/azure-ad-3.png)

- Select the **Non-gallery application**, add an app name (TestFairy) and press the **`Add`** button.

  ![](/img/sso/azure/azure-ad-4.png)


#### Adding an SSO login option


- Go back to the menu and select the **`Single sign-on`** menu option.

  ![](/img/sso/azure/azure-ad-5.png)

- Select the **`SAML`** option.

  ![](/img/sso/azure/azure-ad-6.png)

- Press the pencil icon to edit the __`Basic SAML Configuration`__  - `Identifier` and `Reply URL` fields.
  Add `https://acme.testfairy.com/` to the `Identifier` field and `https://acme.testfairy.com/login/sso` to the `Reply URL`.

  Change `acme` to your own __TestFairy__ subdomain.

  Now download the XML file in the `Federation Data`. You will need it later for uploading to your [TestFairy Dashboard Security settings](https://app.testfairy.com/settings/security/).

  ![](/img/sso/azure/azure-ad-17.png)  


#### Adding users to the application


Now lets add an Azure AD user to your application.

- Go to **`Users and Groups`** and press the `+Add User` button.

  ![](/img/sso/azure/azure-ad-8.png)

- In the **`Add assignment`** column press the `Users and groups` line and select the user/users you want to add from the **`Users and groups`** column.

  Once all users are added to the **`Selected items`** press the `Select` Button.

  ![](/img/sso/azure/azure-ad-9.png)

- To finish the action press the **`Assign`** button.

  ![](/img/sso/azure/azure-ad-10.png)

- The users are all now part of the application.

  ![](/img/sso/azure/azure-ad-11.png)

#### Adding the SAML details to TestFairy

- Now, please go to your TestFairy account preferences, and select the Security menu item.
Open the XML file previously saved and copy its content to the **ID Provider metadata** field.

  Click on `Update SAML ID Provider Metadata` when done.

  ![](/img/sso/azure/azure-tf-1.png)

- After configuration has been saved, you will see a success message.

 ![](/img/sso/azure/azure-tf-2.png)

Now, please log out and make sure you can see the `Login with Azure` button when trying to log in to the [TestFairy Dashboard](https://app.testfairy.com)

## Google
Single Sign-on enables you to manage users and testers outside of TestFairy. A list of permitted users and testers, as well as their passwords, is stored in Google Apps. Therefore onboarding a new developer into the team is an easy task.

When SSO is configured into your account, the login page is replaced with a simple `Login with Google` button.

Talk to us! Request a demo at [https://testfairy.com/products/solutions/enterprise#request-a-demo](https://testfairy.com/products/solutions/enterprise#request-a-demo)

Sections:
- [Installation](#installation)
- [Troubleshooting](#troubleshooting)

<a name="installation"></a>

#### Setting up Login With Google in your account

- Login to Google Apps as admin, go to the admin console and select `Apps`, click on `SAML apps`, and click on bottom-right "Add" button.
  ![](https://docs.testfairy.com/img/sso/google/google-1.png)
  ![](https://docs.testfairy.com/img/sso/google/google-2.png)
  ![](https://docs.testfairy.com/img/sso/google/google-3.png)

- In the popup window, select `Setup my own custom app` at the bottom.
  ![](https://docs.testfairy.com/img/sso/google/google-4.png)

- In step 2, please click on "Option 2: IDP metadata" to download an xml file, and click next
  ![](https://docs.testfairy.com/img/sso/google/google-5.png)

- In step 3, enter "TestFairy" as the name of the application, and click next
  ![](https://docs.testfairy.com/img/sso/google/google-6.png)

- In step 4, we will add the service provider details. Please change `acme` to your enterprise subdomain name on TestFairy.com in the ACS URL: `https://acme.testfairy.com/login/sso`

  Entity ID: `https://acme.testfairy.com`

(please remember to change to your subdomain!)

  ![](https://docs.testfairy.com/img/sso/google/google-7.png)

- Please review and then click `next` and in the next screen click `Finish` when done.
  ![](https://docs.testfairy.com/img/sso/google/google-8.png)

  - you will see a message confirming the setup.
  ![](/img/sso/google/google41.png)

- To finish the setup please make sure the service is on:
![](/img/sso/google/google-100-1.png)

- If not then go to EDIT SERVICE and change it to ON for everyonw :
![](/img/sso/google/google-101.png)

- Now, go to your TestFairy account, click on "Account Preferences" in the topright menu, and select `security` from the left menu. Paste the contents of the file you saved previosuly in the ID Provider metadata field. Click on `Update SAML ID Provider metadata` button when done.

  ![](https://docs.testfairy.com/img/sso/google/google-9.png)

Now, please log out and make sure you can see the "Login with Google" button.

<a name="troubleshooting"></a>

#### Troubleshooting

- `Error: app_not_configured_for_user`. If you are seeing this error message on Google, then it means that you:
  - Didn't enable this app for the current user or for all users. Please see in installation section above, how to enable the newly created app for all users.
  - Accidentally provided wrong **ACS URL** or **Entity ID**. Please see installation section above for the correct values. Notice that every single character matters as values *MUST* be identical for verification.
