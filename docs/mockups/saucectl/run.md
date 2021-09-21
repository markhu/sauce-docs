---
id: run
title: saucectl run
sidebar_label: saucectl run
---

## Description

Run a test through saucectl.

## Usage

<span className="cli">$ saucectl run [OPTIONS]</span>

## Extended Description

Execute tests according to the environment, framework, and test suite specifications defined in your [configuration file](/testrunner-toolkit/configuration).

## Options

`saucectl run` command supports the following alphabetically ordered options as a means of providing custom job configuration at run-time.

### <span className="cli">--artifacts.download.directory &lt;path&gt;</span>

<p><small>| OPTIONAL | PATH |</small></p>

Specifies the path to the folder location in which to download artifacts. A separate subdirectory is generated in this location for each suite for which artifacts are downloaded.

```bash
saucectl run --artifacts.download.directory ./artifacts
```
---

### <span className="cli">--artifacts.download.match</span>
<p><small>| OPTIONAL | STRING/LIST |</small></p>

Specifies which artifacts to download based on whether they match the name or file type pattern provided. Supports the wildcard character `*`.

```bash
saucectl run --artifacts.download.match console.log,another.log
```
---

### `--artifacts.download.when <string>`
<p><small>| OPTIONAL | STRING |</small></p>

Specifies when and under what circumstances to download artifacts. Valid values are:

* `always`: Always download artifacts.
* `never`: Never download artifacts.
* `pass`: Download artifacts for passing suites only.
* `fail`: Download artifacts for failed suites only.

```bash
saucectl run --artifacts.download.when always
```
---

### `--build <string>`
<p><small>| OPTIONAL | STRING | VIRTUAL ONLY |</small></p>

Associates the tests with a build. This flag is not yet supported for mobile real device tests.

```bash
saucectl run --build myBuildID
```
---

### `--concurrency <int>`
<p><small>| OPTIONAL | INTEGER |</small></p>

Sets the maximum number of suites to execute at the same time. If the test defines more suites than the max, excess suites are queued and run in order as each suite completes.

**Shorthand:** `-ccy`

:::caution
For tests running on Sauce, set this value to equal or less than your Sauce concurrency allowance, as setting a higher value may result in jobs dropped by the server.
:::

```bash
saucectl run --ccy 2
```
---

### `--config <path>`
<p><small>| OPTIONAL | FILEPATH |</small></p>

Specify an alternative configuration file to the default `.sauce/config.yml` for this execution.

**Shorthand:** `-c <path>`

```bash
saucectl run -c ./path/to/{config-file}.yml
```

:::note YAML Required
While you can use multiple files of different names or locations to specify your configurations, each file must be a `*.yml` and follow the `saucectl` syntax. If you are less comfortable with YAML, any of a wide variety of free online YAML/JSON validator tools may be helpful.
:::
---

### `--env <key=value>`
<p><small>| OPTIONAL | KEY=VALUE |</small></p>

An environment variable key value pair that may be referenced in the tests executed by this command. Expanded environment variables are supported.

```bash
saucectl run --env <key1>=value1> --env <key2>=<value2> ...
```
---

### `--region <string>`
<p><small>| REQUIRED | STRING |</small></p>

Specifies the Sauce Labs data center through which tests will run. Valid values are: `us-west-1` (default) or `eu-central-1`.

**Shorthand:** `-r <string>`

```bash
saucectl run --region use-west-1
```
---

### `--select-suite <string>`
<p><small>| OPTIONAL | STRING |</small></p>

Specifies a test suite to execute by name.

```bash
saucectl run --select-suite <suite_name>
```

:::note Formerly `--suite <string>`
Versions of saucectl before v0.52.4 use the flag  `--suite` instead.
:::

---

### `--tags <tag1,tag2,...>`
<p><small>| OPTIONAL | LIST | VIRTUAL ONLY |</small></p>

A keyword that may help you distinguish the test in Sauce Labs, and also helps you apply filters to easily isolate tests based on metrics that are meaningful to you. This flag is not yet supported for mobile real device tests.

```bash
saucectl run --tags e2e,team2
```
---

### `--timeout <duration>`
<p><small>| OPTIONAL | DURATION |</small></p>

Sets a limit (in seconds or minutes) for how long `saucectl` can run this test (no limit by default).

```bash
saucectl run --timeout 10s
saucectl run --timeout 30m
```
---

### `--tunnel-id <string>`
<p><small>| OPTIONAL | STRING | <span class="highlight sauce-cloud">Sauce Cloud only</span> |</small></p>

Specifies an active [Sauce Connect](/testrunner-toolkit/configuration#sauce-connect) tunnel to establish a secure connection to run this test on Sauce Labs.

:::note Choose the Correct Tunnel Identifier
When you launch a tunnel, you can accept the tunnel identifier name that Sauce Labs generates for your account (e.g., `{SL-username}_tunnel_id`) or specify a name in the launch command:

```bash
bin/sc -u {SL-username} -k {SL-access_key} -i {tunnel_identifier}
```

This is the value `saucectl` expects as the `tunnel_id`, even though the Sauce Labs UI refers to this value as the `Tunnel Name`.
:::

```bash
saucectl run --tunnel-id <tunnel-id>
```
---

### `--dry-run`
<p><small>| OPTIONAL | BOOLEAN | <span class="highlight sauce-cloud">Sauce Cloud only</span> |</small></p>

Simulate a test run without actually running any tests. This flag does not require a value; including it inline sets it to `true`.

```bash
saucectl run --dry-run
```
---

### `--verbose`
<p><small>| OPTIONAL | BOOLEAN |</small></p>

Enables detailed output during the test run in order to facilitate troubleshooting potential authentication, connection, and/or container issues. This flag does not require a value; including it inline sets it to `true`.

```bash
saucectl run --verbose
```
