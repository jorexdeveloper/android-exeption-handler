<h1 align="center">ANDROID EH</h1>

<p align="center">
	<a href="https://github.com/jorexdeveloper/android-eh/stargazers">
		<img
			src="https://img.shields.io/github/stars/jorexdeveloper/android-eh?colorA=23272a&colorB=007bff&style=for-the-badge">
	</a>
	<a href="https://github.com/jorexdeveloper/android-eh/issues">
		<img
			src="https://img.shields.io/github/issues/jorexdeveloper/android-eh?colorA=23272a&colorB=ff4500&style=for-the-badge">
	</a>
	<a href="https://github.com/jorexdeveloper/android-eh/contributors">
		<img
			src="https://img.shields.io/github/contributors/jorexdeveloper/android-eh?colorA=23272a&colorB=28a745&style=for-the-badge">
	</a>
</p>

User friendly tool to handle and view details of all uncaught exceptions in android applications. An easy way to handle, view, share, and report app crashes quickly on android, with or without any prior developer knowledge.

### FEATURES

- Instantly view crash log
- Share crash log.
- Copy crash log.
- Save crash log.
- User friendly.
- Detailed information in crash log.
- Add developer emails added to the **Intent** when sending crash log to developers.

### CRASH LOG INFO

- Device Information
- App Information
- Crash date and time
- Activity lifecycle traces
- Stack trace with suppressed exceptions

### SCREENSHOTS

<div style="overflow-x: auto; white-space: nowrap; text-align: center;">
	<img src="./img/screenshot.png" width="300" height="600" style="margin: 5px;" alt="image could not be loaded" style="color:red;background-color:black;font-weight:bold">
	<img src="./img/screenshotx.png" width="300" height="600" style="margin: 5px;" alt="image could not be loaded" style="color:red;background-color:black;font-weight:bold">
</div>

You can download the test apk used above from [here](https://github.com/jorexdeveloper/EH/raw/root/test/EHTest-1.0.apk).

### INSTALLATION

All you have to do is download and extract the zip, then follow the steps below to add the library to your project.

Extract the zip and copy the folder **EH** (or **EH-[version]**) to your project's **libs** directory (`.../YourProject/app/libs`), then add the library as a dependency in your application/module `build.gradle` file (`.../YourProject/app/build.gradle`).

```groovy
dependencies {
	// import the project
	api project(':app:libs:EH:eh')
}
```

### USAGE

Initialize **EH** in your **Application** with a new **EH.Builder** instance, passing to it the application **Context**...

```java
// import the class
import com.jorexdeveloper.eh.EH;

public class MyApplication extends Application {

	@Override
	public void onCreate () {

		// Create new Builder instance passing to
		// it the application context
		new EH.Builder (this)
			.init (); // Initialize EH

		super.onCreate ();
	}
}
```

or in **Activity** as...

```java
// import the class
import com.jorexdeveloper.eh.EH;

public class MyActivity extends Activity {

	@Override
	public void onCreate (Bundle savedInstanceState) {

		// Create new Builder instance passing to
		// it the application context
		new EH.Builder (getApplicationContext ())
			.init (); // Initialize EH

		super.onCreate (savedInstanceState);
	}
}
```

### CONSTRUCTOR

```java
public EH.Builder (Context appContext)
```

### METHODS

Use these methods to set configurations for **EH** before call to `init ()`.

```java
public EH.Builder enable (boolean enable)
```

> Default Value : true

Enable/disable **EH**. If disabled, exceptions are forwarded to the **Default Uncaught Exception Handler** that was present before call to `init ()`.

```java
public EH.Builder runInBackground (boolean runInBackground)
```

> Default Value : true

Whether **EH** should run when app is stopped i.e after call to `onStop ()`.

```java
public EH.Builder addSuppressed (boolean add)
```

> Default Value : true

Whether to include suppressed exceptions in the crash log.

```java
public EH.Builder setMaxActivityLogs (int max)
```

> Default Value : 100

Set the maximum number of activity lifecycle logs/traces to include in the crash log. The last **max** logs are included in the log.

```java
public EH.Builder setMaxStackTraceSize (int size)
```

> Default Value : 100

Set the maximum number of stack traces to include in the crash log. The first **size** stack traces are included in the log.

```java
public EH.Builder addEmailAddresses (String... emailAddresses)
```

> Default Value : none

Add email addresses included in the **Intent** used to forward/send crash log to developers.

```java
public void init ()
```

Initialize/set up **EH** with the configurations above.

**Tip :** You can change the configurations for **EH** after call to `init ()` by creating a new **EH.Builder** instance or use the old one, then initializing it with the new configurations and making another call to `init ()`.

### EXAMPLE

```java
// import the class
import com.jorexdeveloper.eh.EH;

public class MyApplication extends Application {
	@Override public void onCreate() {

	// Create new Builder passing application context,
	// then setting configurations and initializing EH
	new EH.Builder (this)
		.enable (true)
		.runInBackground (true)
		.setMaxActivityLogs (50)
		.setMaxStackTraceSize (50)
		.addEmailAddresses ("email0@gmail.com", "email1@gmail.com", "email2@gmail.com")
		.init ();
	}
}
```

**CAUTION : DO NOT FORGET** to make a call to the method `init ()` or **EH** will not run and your applications will crash normally.

#### LICENSE

```
	Copyright © 2021 Jore

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

	http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
