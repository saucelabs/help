---
title: Reference
layout: en
permalink: docs/tools/appium/reference/
---

<ul>
	<li><a href="#appium-capabilities">Appium Capabilities</a></li>
	<li><a href="#run-with-any-language">Run with Any Language</a></li>
	<li><a href="#live-view-and-report-urls">Live-View and Report URLs</a></li>
	<li><a href="#device-caching">Device Caching</a></li>
	<li><a href="#session-creation-timeout">Session Creation Timeout</a></li>
  	<li><a href="#accessing-testobject-via-proxy">Accessing TestObject Via Proxy</a></li>
	<li><a href="#cordova-app-testing">Cordova App Testing</a></li>
</ul>

<h3 id="appium-capabilities">Appium Capabilities</h3>
When you are running an Appium test on TestObject, the Appium server on TestObject's side receives all the capabilities you set on the client side. This means you can theoretically set all the capabilities allowed by the Appium version you are running against. Due to the nature of our service though, setting some capabilities may produce a different outcome than you would expect from just running an Appium server locally. For example:

- all the emulator-only capabilities will not work on TestObject, as we only provide access to real devices;
- the 'app' capability is always overwritten to point the server to the app file you uploaded to our system;
- the 'platformName' capability is overwritten because we select the platform your test will run on based on the kind of project you are pointing to with your API key;
- the 'noReset' capability only works if [device caching](#device-caching) is enabled. By default, 'noReset' will be set to false;
- for test suite runs, the 'testobject_suite_name' and "testobject_test_name' capabilities are ignored;
- the 'deviceName' capability is always overwritten.

Different setups might have slightly different ways of handling capabilities and/or different requirements. Please make sure you also check the guide relative to your [specific setup](/docs/tools/appium/setups/) to make sure you are providing everything that is required.

<h3 id="run-with-any-language">Run with Any Language</h3>

Appium tests can be run on TestObject no matter what language you're using. You will only need to specify the following capabilities:

- `testobject_api_key`: Indicates the project that you are testing on.
- `testobject_device`: Specifies which device you are testing on

Additionally, you will need to change your appium endpoint to `http://appium.testobject.com/wd/hub`.

<h3 id="live-view-and-report-urls">Live-View and Report URLs</h3>

When starting an Appium session we enhance the default capabilities returned by the session by two properties:


<h5>testobject_test_live_view_url</h5>

The URL to the live-view your test execution (available only while the Appium session is ongoing)


<h5>testobject_test_report_url</h5>

The URL to the final Appium Test Report (available after the test has finished executing)


This is an example of how to access the capabilities:

{% highlight java %}

private AndroidDriver driver;

@Before
public void setup() throws MalformedURLException {
	...

	AppiumDriver driver = new AppiumDriver(new URL("http://appium.testobject.com/wd/hub"), capabilities);
	driver.getCapabilities().getCapability("testobject_test_report_url");
	driver.getCapabilities().getCapability("testobject_test_live_view_url");

	...
}
{% endhighlight %}

<h3 id="device-caching">Device Caching</h3>

By default, the TestObject platform uninstalls the application, performs device cleaning, and de-allocates the device between every Appium session. This means that if you have multiple test methods, you will by default wait for this cleaning process between every test method.

To speed up test execution, you can set the desired capability `testobject_cache_device` to `true`. This will leave the device allocated to you for a short time after each Appium session. If you immediately start another test on the device, you won't need to wait for the allocation and device cleaning process to be repeated.

The `testobject_cache_device` capability can be used in conjunction with the standard `noReset` Appium capability. In the default case, where `noReset` is set to false, your application will be uninstalled and reinstalled after every test, as per normal Appium behaviour. If `noReset` is set to true, the application you are testing won't be uninstalled after every test run. This might save you further time, but it won't be suitable for test setups which require the application's state to be reset between tests. Note that while `testobject_cache_device` is set to true, no device cleaning will take place in between sessions, regardless of `noReset` value.

<h3 id="session-creation-timeout">Session Creation Timeout</h3>

When creating an Appium session on the TestObject public cloud, it may be the case that the device is "in use" and not currently available for testing. When this happens, the tests will by default wait for 15 minutes to create a session on the device. If you would like to set a custom timeout for session creation, you can do so using the desired capability `testobject_session_creation_timeout`. The value for this capability should be a string containing the desired timeout in milliseconds. The maximum allowed timeout is 30 minutes.

<h3 id="accessing-testobject-via-proxy">Accessing TestObject Via Proxy</h3>

If you're running your tests in a network that requires a proxy to communicate with TestObject, there is some configuration
necessary if you're using the [TestObject Appium API](https://github.com/testobject/testobject-appium-java-api).

<h4>Proxy Configuration</h4>

To communicate with your proxy, you must provide the address and credentials (if necessary) for it. This can be done using
the following system properties:

* `https.proxyHost` - e.g. www.example.com
* `https.proxyPort` - e.g. 8888; default is 8080
* `https.proxyUser`
* `https.proxyPassword`

If your proxy has no authentication, you don't need to set `proxyUser` and `proxyPassword`.

<h4>Setting System Properties</h4>

[System properties](https://docs.oracle.com/javase/tutorial/essential/environment/sysprop.html) can be set in code, or
passed in via the command line.

To set properties in code, use `System.getProperties().put()` such as this:

* `System.getProperties().put("http.proxyHost", proxyHost);`

Or, to set them via the command line, which may be more useful if you are triggering your tests via a CI such as Jenkins,
prepend the system property with -D, for example:

* `-Dhttps.proxyHost=www.example.com -Dhttps.proxyPort=8888`

<h3 id="cordova-app-testing">Cordova App Testing</h3>

When testing Hybrid applications using Appium, it's important to have access to the application's webview for interacting with the application. For Hybrid applications built for Android using Cordova or Crosswalk, Appium may have issues connecting to the webview. This issue is currently being resolved by the open source community, but you can already avoid this issue when testing on TestObject. 

To avoid this issue, simply use our patched Appium version and set your Appium version to `1.5.2-patched-chromedriver`. You can specify this Appium version by setting the `testobject_appium_version` desired capability or by editing your test suite's settings if you're using the [Suite Setup](/docs/tools/appium/setups/suite-setups). This Appium version uses our patched Chromedriver version, and will allow you to access the webview for Cordova applications on Android.
