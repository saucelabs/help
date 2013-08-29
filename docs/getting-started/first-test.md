---
title: Running Your First Test
layout: en
permalink: docs/getting-started/first-test/
alias: [docs/guides/getting-started/, wiki/display/cf/Getting+Started+Tutorial/index.html]
---

Welcome to TestObject! Get ready to create and run your first automated mobile app test in 4 easy steps.

What you need:

<ul>
	<li>A web browser</li>
	<li>A free <a href="http://app.testobject.com/signup" target="_blank">TestObject account</a></li>
	<li>An app (*.apk file) - <a href="https://docs.google.com/file/d/0ByR0JcAYUAoWdS1faUNJdGxONzg/edit?usp=sharing" target="_blank" rel="nofollow">download a sample app here</a></li>
	<li>5 minutes</li>
</ul>

Let's get started!




<h3 id="project">Step 1: Create a New Project</h3>

After <a href="http://app.testobject.com/signup" target="_blank">signing in</a> to your TestObject account, click the *New Project* button to create your first project.

<img src="/img/getting-started/first-test/first-test-01.png">

Name the project "MyProject" and click *Save*.

<img class="center shadow" src="/img/getting-started/first-test/first-test-02.png">

Your newly created project will then be opened for you.




<h3 id="app">Step 2: Upload Your App</h3>

The screen you will see now allows you to manage versions of your app. <br>
Click the *New Version* button to add the version of your app that you would like to test.

<img class="center shadow" src="/img/getting-started/first-test/first-test-03.png">

Choose whether you are going to test a native Android app or a web app (website). In this tutorial we will test a native app, so choose *Native*.

<img class="center shadow" src="/img/getting-started/first-test/first-test-04.png">

On the next screen, click *Choose APK File* and browse for the app file you want to upload to the system. For the tutorial you can use the provided <a href="https://docs.google.com/file/d/0ByR0JcAYUAoWdS1faUNJdGxONzg/edit?usp=sharing" target="_blank" rel="nofollow">sample app</a>.<br>
Name the app version "My App 1.0" and click *Save*.

<img class="center shadow" src="/img/getting-started/first-test/first-test-05.png">

You will then see the newly uploaded app in the list. It will be marked as "active". Per project you can have one active app version which is going to be used for testing.

<img class="center shadow" src="/img/getting-started/first-test/first-test-06.png">




<h3 id="record">Step 3: Record Your First Test</h3>

Now switch to the *Tests* tab and click *New Test* to set up your first test.

<img class="center shadow" src="/img/getting-started/first-test/first-test-07.png">

Name your test "My first test" and, if you like, select a label for it.<br>
Then choose a device to record your test on and click *Continue*.

<img class="center shadow" src="/img/getting-started/first-test/first-test-08.png">

You will then see the TestObject Recorder. The device that had been selected before will now be booted and your app will be installed on it.

<img class="center shadow" src="/img/getting-started/first-test/first-test-09.png">

As soon as your app has launched, you are ready to start recording. To do so click the *Record* button. Each action you execute on the device will now be added as a line in the script on the right side.

<img src="/img/getting-started/recorder/recorder-02.png">

On the device screen click the 'Continue' button of the sample app and notice that for the click action a new script line is generated.<br>

<img class="center shadow" src="/img/getting-started/first-test/first-test-10.png">

Now click *Stop* to leave the recording mode.




<h3 id="replay">Step 4: Replay the Test</h3>

To immediately check how your test runs on the device, click the *Replay* button.

<img src="/img/getting-started/recorder/recorder-11.png">

You can now sit back and watch how the recorded test gets replayed automatically on the device.

<img class="center shadow" src="/img/getting-started/first-test/first-test-11.png">

Congratulations, you have successfully recorded and replayed a test for your app. Good for you!




<h3 id="next">What's next?</h3>

+ Learn more about some <a href="/docs/getting-started/recorder">advanced recorder functionalities</a>.
+ Run your test on different devices by <a href="/docs/getting-started/batches">creating a batch</a>.

Remember: TestObject CONTINUOUS is made for **continuous integration** and will reach it's fullest potential as a continuous testing solution in the tool chain of your agile development process.