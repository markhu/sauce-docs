---
id: selenium
title: Selenium on Sauce Labs
sidebar_label: Getting Started
description: An introduction to web app automation testing using Selenium.
---

import useBaseUrl from '@docusaurus/useBaseUrl';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

The Selenium browser automation tool allows you to write test code that runs through all the possible actions in your web application faster and more effectively that manual testing. This section of the Sauce Labs documentation provides an overview of how to use Selenium with Sauce Labs to achieve efficient and consistent test results to ensure your web application works on every operating system and browser.


## What You’ll Need

* A Sauce Labs account ([Log in](https://accounts.saucelabs.com/am/XUI/#login/) or sign up for a [free trial license](https://saucelabs.com/sign-up))
* Your Sauce Labs [Username](https://app.saucelabs.com/user-settings)


## Architecture

Selenium is built on a **client-server architecture**, which includes both client and server components.

The API used by Selenium servers and browser drivers is defined in the W3C WebDriver specification and communicated
between the components using http commands.
* The client code, specifically the Remote WebDriver class contains the methods that implement the API for automating the browser.
  Selenium translates this code into the https commands defined by the W3C, and sends
  this information to a server.
* The Selenium Server receives the http commands that were sent by the Selenium client.
  This server can be in standalone mode, or in a grid mode with different servers set as hubs and nodes.
  The server forwards the commands to the browser driver, which ultimately controls how the browser is automated.

#### For Sauce Labs, it looks like this:
<img src={useBaseUrl('img/selenium/selenium-diagram.png')} alt="Diagram of Selenium and Sauce Labs"/>

## Seven Steps of Selenium Tests

There are seven basic elements of a Selenium test script, which apply to any test case and any application under test (AUT):

1. [Create a WebDriver session](#step-1-create-a-remote-session).
2. [Navigate to a Web page](#step-2-navigate-to-a-web-page).
3. [Locate an HTML element on the Web page](#step-3-locate-an-html-element-on-a-web-page).
4. [Perform an action on the located element](#step-4-perform-actions-on-located-elements).
5. [Assert the performed action did the correct thing](#step-5-assert-a-result).
6. [Report the result of the assertion](#step-6-report-the-results).
7. [End the session](#step-7-end-the-session).

The following sections walk through each of these steps using a basic test case example -- logging into a website. This example ensures that a specific user can successfully log into https://www.swaglabs.com.

### Step 1: Create a Remote Session.

Create an instance of Selenium's Remote WebDriver class so you can invoke methods of the Selenium WebDriver API on Sauce Labs infrastructure.

#### Direct Tests to Sauce Labs

Remote WebDriver classes are instantiated with the URL of the server or service you want for your tests. For Sauce Labs, choose a URL from our [Data Center Endpoints](/basics/data-center-endpoints/data-center-endpoints/#endpoints).

#### Define Capabilities

The way to define capabilities in recent versions of Selenium is with browser options classes. The configurations set on these classes do one of two things:
* Ensure you have the session you want (e.g., browser name, browser version, operating system).
* Set the behavior you want in your session. There are three types of options that set behavior:
  * [Common options](/dev/test-configuration-options/#browser-w3c-capabilities--optional):
    these include things such as page load timeouts, and insecure certificate behavior.
  * [Browser options](/dev/test-configuration-options/#browser-vendor-capabilities)
  * Sauce Labs options: see [Test Configuration](/dev/test-configuration-options)
    for a complete guide to our available capabilities.

:::note
`DesiredCapabilities` is used in earlier versions of Selenium, but interactions with this class have been deprecated. Use the browser options classes instead.
:::

The following example shows the instantiation of the RemoteWebDriver (assigned the variable name `driver`), authentication values, and the OS/Browser targets for a test written in Selenium 3.141.59:

```java reference title="Configuring a Driver"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SeleniumLoginTest.java#L32-L42
```

:::tip Use Credential Environment Variables
Set your Sauce Labs account credentials as [environment variables](/basics/environment-variables) rather than hard-coding them into all your scripts for efficiency and to protect them from unintended exposure.
:::


### Step 2: Navigate to a Web Page

Invoke the `get` method on your WedDriver instance, using the variable name you assigned, and pass the URL of the web page containing the element you wish to test as an argument. The following gets our Swag Labs login page:

```java reference title="Selenium Navigation"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SeleniumLoginTest.java#L48
```

To view code snippets in JavaScript, Python, Ruby, and C#, see the [Selenium documentation on Browser Navigation](https://www.selenium.dev/documentation/webdriver/browser_manipulation/#browser-navigation).


### Step 3: Locate an HTML Element on a Web Page

Once the test script accesses the page to test, it needs to find the elements that an end user would interact with. In this case, the login fields and **Submit** button.

To find an element we need to right-click on the elements we are interested in and select "Inspect" from the context menu. The form elements look like this:

```html title="Login Form"
<html>
 <body>
 ...
  <form>
    <div class="form_group">
      <input class="input_error form_input" placeholder="Username" type="text" data-test="username" id="user-name" name="user-name" autocorrect="off" autocapitalize="none" value="">
    </div>
    <div class="form_group">
      <input class="input_error form_input" placeholder="Password" type="password" data-test="password" id="password" name="password" autocorrect="off" autocapitalize="none" value="">
    </div>
    <div class="error-message-container"></div>
      <input type="submit" class="submit-button btn_action" data-test="login-button" id="login-button" name="login-button" value="Login">
  </form> ...
 </body>
</html>
```

#### Selector Strategies

Selenium provides multiple [element selection strategies](https://www.selenium.dev/documentation/en/webdriver/locating_elements/#element-selection-strategies),
which include determining an element by:

* A specific **attribute** value, such as the value of `name` or `id`
* The **tag name** of the element, such as `div` or `button`
* **Visible text**; this only applies to anchoxr elements, such as `Sauce Labs`
  in `<a href="https://www.saucelabs.com">Sauce Labs</a>`
* A [**CSS** selector](https://www.w3.org/TR/selectors-3/#selectors),
  such as `[placeholder="Username"]`
* An [**XPath** expression](https://www.w3.org/TR/1999/REC-xpath-19991116/#location-paths),
  such as `//input[@placeholder="Username"]`  

:::tip Identifying Elements in HTML

In your Selenium test scripts, identify test elements by their `name` or `id` attribute value, since those are often the simplest way to uniquely identify the element.
:::

#### Locator Methods

You can use any of the WebDriver API _locator methods_ to form locator expressions that find an element based on a specified locator type and value. In Java and .NET, locators are managed with a `By` class instance - `By.id("user-name")`.

In Python, the locator method is merged with the [_finder method_](#finder-methods) (i.e.,  `find_element_by_id("user-name")`), whereas Ruby uses key value pairs, typically as Hash values (i.e., `{id: "user-name"}`).

Most of the elements in our Swag Labs example have multiple unique attributes that make it easy to identify them. For this example we can identify them as follows:


```java reference title="Selenium Locator Definitions"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SeleniumLoginTest.java#L50-L52
```

To view code snippets in JavaScript, Python, Ruby, and C#, see the [Selenium documentation on Locating Elements](https://www.selenium.dev/documentation/en/webdriver/locating_elements).


#### Finder Methods

To find an element, pass your locator method as an argument of a WebDriver API _finder method_.

The find element method for the given language will search the DOM (Document Object Model) of the current web page until it finds a matching element and returns it. Regardless of the language, changing the method name with "element" to "elements" will search the entire DOM, and return a collection of all matching elements rather than just the first one.

The following example invokes `findElement` on our `driver` instance to locate the elements for which we defined locators in the last section:

```java reference title="Finding Selenium WebElements"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SeleniumLoginTest.java#L57-L59
```


To view code snippets in JavaScript, Python, Ruby, and C#, see the [Selenium documentation on the Find Element](https://www.selenium.dev/documentation/en/webdriver/web_element/#find-element).


#### Synchronization Strategies

Synchronization is an advanced topic, but it is essential when locating an element that the application is ready for the element to be located. There are two main approaches to synchronization: implicit and explicit.

#### Implicit Waits

When Selenium executes a find element call and the driver can not find the element, an exception is thrown immediately. An implicit wait is set telling the driver how long to wait before throwing the exception. If the element is located right away, the value of the implicit wait does not matter.

:::note
Implicit waits are generally not recommended. It's a one-line code change that can potentially reduce the number of failed tests in your suite, but it is often more of a crutch than a successful long term solution. Should you decide to set an implicit wait, do it once when you create the session and keep it to a small value.
:::

#### Explicit Waits

An explicit wait handles the synchronization in the code itself, typically with some form of while loop. When the desired condition is met, the test can continue, and only if the condition is not met after the maximum wait time will the code throw an exception.

:::caution Do Not Mix Explicit and Implicit Waits
Mixing implicit and explicit waits can cause unpredictable outcomes, which is another reason to avoid implicit waits.
:::

Each language implements this slightly differently. Java and .NET have `ExpectedConditions` classes, but the recommended approach in all languages at this point is to use a lambda, like so:

```java reference title="Selenium Waits"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SeleniumLoginTest.java#L54-L55
```

To view code snippets in JavaScript, Python, Ruby, and C#, see the [Selenium documentation on Waits](https://www.selenium.dev/documentation/en/webdriver/waits/).

### Step 4: Perform Actions on Located Elements

Invoke an interaction method on an instance of the WebElement interface to simulate the user's interaction with
the website elements you have located. The basic interactions include:

* The "send keys" method to enter text into an input field
* The "clear" method to clear entered text from an input field
* The "click" method to simulate a mouse down action on any element
* The "submit" method will submit a form

:::caution
The "submit" method does not simulate how a user would submit the form, so it is recommended to click the **Submit** button instead.
:::

The following example automates a user login by sending keys to the username and password text fields, and clicking the **Submit** button:

```java reference title="Selenium Actions"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SeleniumLoginTest.java#L61-L63
```

### Step 5: Assert a Result

You do not have a test without an assertion. Each test should have something specific it is checking for and have an explicit line of code to ensure that this functionality is working as intended. What makes a test successful and how to evaluate success requires domain knowledge and can be more art than science. Here's an example of an assertion with JUnit 5:

```java reference title="Assertions"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SeleniumLoginTest.java#L65
```

### Step 6: Report the Results

Keeping track of the success and failure of your tests is essential.
Testers record their results in many different ways and with various amounts of information. Sauce Labs is a good resource for recording failures because with the videos and screenshots and logs it is much easier to determine the reason for the failures.

To see your results on Sauce Labs, navigate to the [**AUTOMATED** > **Test Results**](https://app.saucelabs.com/dashboard/tests) page where you can watch your test run live or review the video or screenshot assets of the test.

Since Sauce Labs doesn't know what you are asserting in your code, though,
we rely on users to send us the information. One approach is with JavaScript before you end
your session. Here's an example using JUnit 5 with a Test Watcher class:

```java reference title="Report Passing Test to Sauce Labs"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SeleniumLoginTest.java#L74
```
or
```java reference title="Report Failing Test to Sauce Labs"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SeleniumLoginTest.java#L80
```

### Step 7: End the Session

It is important to remember to close the browser when you are done with it by calling the quit method on the Remote WebDriver instance.

* quits the browser, closing all web pages
* ends the Sauce session allowing timely processing of results and storage of artifacts.

The following examples invokes the quit method on the driver variable:


```java reference title="Quit Selenium Session"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SeleniumLoginTest.java#L75
```


### Complete Example  

The following example shows the Java code for all seven steps described in this document, implemented with JUnit 5.

```java reference title="Complete Selenium Example"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SeleniumLoginTest.java#
```

### Sauce Bindings Example

The [Sauce Bindings](https://opensource.saucelabs.com/sauce_bindings/) are designed to minimize the complexity of
working with Sauce Labs. Toward that end, the previous example can be written using saucebindings-junit5 package
with the setup and teardown methods handled for you. You can see how much less code there is here:

```java reference title="Simplify With Sauce Bindings"
https://github.com/saucelabs-training/demo-java/blob/docs-1.0/selenium-examples/src/test/java/com/saucedemo/selenium/login/SauceBindingsLoginTest.java
```

## Scaling Tests

The example is a simple one, and only creating a number of files just like it one would not be very efficient.

Scaling up tests requires at a minimum a test runner, and even better a more fully featured testing library. These tools allow for better abstractions and less code duplication in your tests, as well as the ability to run tests in parallel instead of just sequentially.

Test Runners include:
* Java - JUnit 5, JUnit 4, TestNG
* Python - pyTest, unittest
* Ruby - RSpec, Cucumber
* .NET - NUnit, MSTest

Testing Libraries include:
* Java - Selenide, FluentLenium, QAF
* Python - Nerodia, Helium, SeleniumBase
* Ruby - Capybara, Watir
* JavaScript - WebdriverIO, Nightwatch.js, CodeceptJS

The [Sauce Labs Training Repo](https://github.com/saucelabs-training) contains an extensive selection of demonstration scripts illustrating parallel testing in different frameworks and programming language combinations.


## Selenium Resources

* [Selenium HQ](http://www.seleniumhq.org): official Selenium website and documentation
* [How to Run a Selenium Test on Sauce Labs](https://www.youtube.com/watch?v=qq1WCsAMZsk): Automated testing guru Joe Colantonio demonstrates how to run a Selenium Test with Sauce Labs
