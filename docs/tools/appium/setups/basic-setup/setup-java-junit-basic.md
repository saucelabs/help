---
title: Basic Setup on TestObject using JUnit
layout: en
permalink: docs/tools/appium/setups/basic-setup/junit/
---

Whether you are starting from scratch or you have an already existing Appium test written, adapting it to run on TestObject is a matter of minutes. A first basic test setup with JUnit could look like this:

{% highlight java %}
public class BasicTestSetup {

    private AppiumDriver driver;

    @Before
    public void setUp() throws Exception {

        DesiredCapabilities capabilities = new DesiredCapabilities();

        /* These are the capabilities we must provide to run our test on TestObject */
        capabilities.setCapability("testobject_api_key", "YOUR_API_KEY");
        capabilities.setCapability("testobject_device", "Motorola_Moto_G_2nd_gen_real");

        /* The driver will take care of establishing the connection, so we must provide
        * it with the correct endpoint and the requested capabilities. */
        driver = new AndroidDriver(new URL("http://appium.testobject.com/wd/hub"), capabilities);

    }

    /* We disable the driver after EACH test has been executed. */
    @After
    public void tearDown(){
        driver.quit();
    }

    @Test
    public void testMethod() {
        /* Your test. */
    }

}
{% endhighlight %}

Along with the mandatory capabilities we have specified, you can send over some optional ones to customize your test runs:

* <strong>testobject_app_id</strong>, if you want to use an app version other than the active one.
* <strong>testobject_appium_version</strong>, if you want to run your tests against an Appium version other than the default one.
* <strong>testobject_suite_name</strong>, if you want to apply a label to your tests so that they are easier to group / find later on.
* <strong>testobject_test_name</strong>, if you want to specify a name for your test that will be displayed in place of the default one.

The only needed dependencies for running such a test would be the [Appium Java Client](https://github.com/appium/java-client) and the [Selenium Standalone Server](http://www.seleniumhq.org/download/). In case you are building your project with Gradle, your dependencies in your build.gradle file should look something like this:

{% highlight bash %}
  dependencies {
      testCompile group: 'junit', name: 'junit', version: '4.11'

      testCompile 'io.appium:java-client:4.1.2'
      testCompile 'org.seleniumhq.selenium:selenium-server:2.53.0'

  }
{% endhighlight %}

With this kind of barebones setup you will be able to run tests on the TestObject platform, but you will not be using it to its fullest potential, as the results of the tests won't be registered in the test reports on TestObject. Don't panic though! All you need to do is upgrade to a [Watcher Setup](/docs/tools/appium/setups/watcher-setups). If you want to run tests on multiple devices, use [Suite setups](/docs/tools/appium/setups/suite-setups).
