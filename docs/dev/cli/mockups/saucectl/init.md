---
id: init
title: saucectl init
sidebar_label: saucectl init
---

## Description

Generate a configuration file for use in running tests through saucectl.

## Usage

<span className="cli">$ saucectl init [OPTIONS]</span>

## Extended Description

This bootstrapping command generates a configuration file for the framework of your choice in the format required by `saucectl`.

You can run the command with no options to initiate **interactive mode**, where you are iteratively prompted for each relevant property value. Alternatively, you can specify relevant property values by entering them as inline options in the command.

In either case, the command generates a `.sauce/config.yml` folder and file in the location from which the command is run. If you have an existing project directory for your framework, it is advised that you run this command from the project root.

## Options

<table id="table-cli">
  <thead>
    <tr>
      <th width="20%">Key</th>
      <th width="10%">Shorthand</th>
      <th width="10%">Required</th>
      <th width="10%">Format</th>
      <th width="15%">Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
     <td><span className="cli">--accessKey</span></td>
     <td><span className="cli">-a</span></td>
     <td></td>
     <td>string</td>
     <td></td>
     <td>The authentication access key associated with the Sauce Labs user account making this request. If you have not set your authentication credentials as environment parameters or generated a <code>credentials.yml</code> file, this value is required.</td>
    </tr>
    <tr>
     <td><span className="cli">--app</span></td>
     <td></td>
     <td></td>
     <td>string</td>
     <td></td>
     <td><small><span className="sauceDBlue">Espresso/XCUITest Only</span></small><br/>The path to a valid mobile application to test.</td>
    </tr>
    <tr>
     <td><span className="cli">--framework</span></td>
     <td><span className="cli">-f</span></td>
     <td align="center">&#10003;</td>
     <td>string</td>
     <td></td>
     <td>The framework for which this configuration is intended.</td>
    </tr>
  </tbody>
</table>

`saucectl` supports the following configuration flags as inline specifications.


### `--accessKey <string>`
<p><small>| OPTIONAL | STRING |</small></p>

The authentication access key associated with the Sauce Labs user account making this request. If you have not set your authentication credentials as environment parameters or generated a `credentials.yml` file, this value is required.

**Shorthand:** `-a <string>`

---

### `--app <string>`
<p><small>| OPTIONAL | STRING | XCUITEST/ESPRESSO ONLY |</small></p>

The path to a valid mobile application to test.

---

### `--artifacts.download.when <string>`

<p><small>| OPTIONAL | STRING |</small></p>

Specifies when and under what circumstances to download artifacts. Valid values are:

* `always`: Always download artifacts.
* `never`: Never download artifacts.
* `pass`: Download artifacts for passing suites only.
* `fail`: Download artifacts for failed suites only. (default value)

---

### `--browserName <string>`
<p><small>| REQUIRED | STRING | WEB-APP ONLY |</small></p>

The name of the browser in which to run tests.

**Shorthand:** `-b <string>`

---

### `--cypress.config <string>`
<p><small>| REQUIRED | STRING | CYPRESS ONLY |</small></p>

The file path to the Cypress configuration file (typically `cypress.json`).

---

### `--device <string>`
<p><small>| OPTIONAL | STRING | XCUITEST/ESPRESSO ONLY |</small></p>

Find a real device for this test by matching a set of one or more device characteristics:

|Characteristic|Description|Example|
|---|---|---|
|`id`| Specify a device by its ID. Using this selection flag ignores all other characteristics and is not advised because availability of a specific device is uncertain and could cause your test to time out.| ```--device "id=HTC_U11_real_us"```|
|`name`|Find a device based on a partial name in order to increase likelihood of availability of similar devices.|```--device "name=HTC.*"```|
|`platformVersion`|Find a device based on its platform version.|```--device "platformVersion=8.0"```|
|`carrierConnectivity`|The selected device must be connected to a cellular network. |```--device "carrierConnectivity=true"```|
|`deviceType`|The selected device must be a particular type (`PHONE`, `TABLET`, or `ANY`).|```--device "deviceType=PHONE"```|
|`private`|The selected device must be private.|```--device "private=true"```|

You can specify a combination of device characteristics within this flag:

```bash
--device "name=HTC.*,platformVersion=8.0.0,carrierConnectivity=true"
```

---

### `--emulator <string>`
<p><small>| OPTIONAL | STRING | ESPRESSO ONLY |</small></p>

Specify a virtual device for the test by matching a set of one or more emulator characteristics.

|Characteristic|Description|Example|
|---|---|---|
|`name`|Specify all or part of the emulator name. [Supported VMD List](https://app.saucelabs.com/live/web-testing/virtual) |```--emulator "name=Android.*"```|
|`platformVersion`|Specify the emulator platform version.|```--emulator "platformVersion=7.1"```|
|`orientation`|Specify how the emulator should be oriented for the test (`portrait` or `landscape`). |```--emulator "orientation=portrait"```|

You can specify a combination of emulator characteristics within this flag:

```bash
--emulator "name=Samsung Galaxy S8 FHD GoogleAPI Emulator,platformVersion=7.1"
```

---

### `--framework <string>`
<p><small>| REQUIRED | STRING |</small></p>

The framework for which this configuration is intended.

**Shorthand:** `-f <string>`

---

### `--frameworkVersion <string>`
<p><small>| REQUIRED | STRING | WEB APPS ONLY |</small></p>

The version of the framework that is compatible with the tests defined in this configuration.

**Shorthand:** `-v <string>`

---

### `-h, --help`

Usage information for the `init` command.

---

### `--platformName <string>`
<p><small>| OPTIONAL | STRING | WEB APPS ONLY |</small></p>

A specific operating system and version on which to run the specified browser and test suite.

:::note
You can optionally specify `docker` here as the platform.
:::

**Shorthand:** `-p <string>`

---

### `--region <string>`
<p><small>| REQUIRED | STRING |</small></p>

Specifies the Sauce Labs data center through which tests will run. Valid values are: `us-west-1` (default) or `eu-central-1`.

**Shorthand:** `-r <string>`

---

### `--testApp <string>`
<p><small>| REQUIRED | STRING | XCUITEST/ESPRESSO ONLY |</small></p>

The path to the mobile testing application.

**Shorthand:** `-t <string>`

---

### `--username <string>`
<p><small>| OPTIONAL | STRING |</small></p>

A valid Sauce Labs user account. If you have not set your authentication credentials as environment parameters or generated a `credentials.yml` file, this value is required.

**Shorthand:** `-u <string>`

---

## Examples

```bash title="Interactive Example"
$ saucectl init
12:13:20 INF Start Init Command
? Select region: us-west-1
? Select framework:  [Use arrows to move, type to filter]
> cypress
 playwright
 puppeteer
 testcafe
 espresso
 xcuitest
```

```bash title="Batch Example"
$ saucectl init -r us-west-1 -f cypress -b chrome
```
