---
id: styles
title: Possible CLI Styles
sidebar_label: CLI Styles
description: A few options for how we can style our CLI descriptions.
---

<p style={{fontSize:32, color:"#32b2ed"}}>Option 1 -- saucectl style</p>

## `connect [flags]`

Connect a device that is already engaged in a live session to your local machine so you can conduct the test from within your V-USB environment.

```bash title="Full Example using all flags"
java -jar virtual-usb-client.jar connect \
    --sessionId d03a1b81-158d-4bb4-bcc9-074e43dd8465 \
    --username john.smith \
    --accessKey ab015c1e-xxxx-xxxx-xxxx-xxxxxxxxxxx \
    --serverHost http://127.0.0.1 \
    --serverPort 8080 \
```

<big><b>Flags</b></big>

### `--sessionId`
<p><small>| REQUIRED | STRING | <span className="sauceDBlue">Real Device Only</span></small> |</p>

The unique identifier of an active Sauce Labs live test session to which you want to connect. You can lookup a session ID using the [`session` command](/dev/cli/virtual-usb/find-sessionid).

```bash
java -jar virtual-usb-client.jar connect --sessionId d03a1b81-158d-4bb4-bcc9-074e43dd8465
```

### `--username`
<p><small>| REQUIRED | STRING |</small></p>

Your Sauce Labs [Username](https://app.saucelabs.com/user-settings).


### `--accessKey`
<p><small>| REQUIRED | STRING |</small></p>

Your Sauce Labs [Access Key](https://app.saucelabs.com/user-settings).


### `--serverHost`
<p><small>| OPTIONAL | STRING |</small></p>

Specifies an alternative Virtual USB server host to use instead of the default `http://127.0.0.1`.


### `--serverPort`
<p><small>| OPTIONAL | STRING |</small></p>

Specifies an alternative Virtual USB server port to use instead of the default `33657`.

---


<p style={{fontSize:32, color:"#32b2ed"}}>Option 2 -- api style</p>

## Connect to a Session

<details><summary><code>connect &#91;flags&#93;</code></summary>

Connect a device that is already engaged in a live session to your local machine so you can conduct the test from within your V-USB environment.

#### Flags

<table id="table-api">
  <tbody>
    <tr>
     <td width="20%"><code>--sessionId</code></td>
     <td><p><small>| REQUIRED | STRING |</small></p><p>The unique identifier of an active Sauce Labs live test session to which you want to connect. You can lookup a session ID using the <a href="/dev/cli/virtual-usb/find-sessionid"><code>session</code> command.</a></p></td>
    </tr>
  </tbody>
  <tbody>
    <tr>
     <td><code>--username</code></td>
     <td><p><small>| REQUIRED | STRING |</small></p><p>Your Sauce Labs <a href="https://app.saucelabs.com/user-settings">Username</a>.</p></td>
    </tr>
  </tbody>
  <tbody>
    <tr>
     <td><code>--accessKey</code></td>
     <td><p><small>| REQUIRED | STRING |</small></p><p>Your Sauce Labs <a href="https://app.saucelabs.com/user-settings">Access Key</a>.</p></td>
    </tr>
  </tbody>
  <tbody>
    <tr>
     <td><code>--serverHost</code></td>
     <td><p><small>| OPTIONAL | STRING |</small></p><p>Specifies an alternative Virtual USB server host to use instead of the default <code>http://127.0.0.1</code>.</p></td>
    </tr>
  </tbody>
  <tbody>
    <tr>
     <td><code>--serverPort</code></td>
     <td><p><small>| OPTIONAL | STRING |</small></p><p>Specifies an alternative Virtual USB server port to use instead of the default <code>33657</code>.</p></td>
    </tr>
  </tbody>
</table>


```bash title="Full Example with optional flags"
java -jar virtual-usb-client.jar connect \
    --sessionId d03a1b81-158d-4bb4-bcc9-074e43dd8465 \
    --username john.smith \
    --accessKey ab015c1e-xxxx-xxxx-xxxx-xxxxxxxxxxx \
    --serverHost http://127.0.0.1 \
    --serverPort 8080 \
```

</details>
