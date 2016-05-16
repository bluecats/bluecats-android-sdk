BlueCats SDK for Android
====================

[ ![Download](https://api.bintray.com/packages/bluecats/maven/bluecats-android-sdk/images/download.svg) ](https://bintray.com/bluecats/maven/bluecats-android-sdk/\_latestVersion)

The BlueCats' SDKs have been developed for easy integration and to offer flexiblity across different use cases.  Please let us know if you have any questions at developers@bluecats.com.

**See the [BlueCats Developer Portal](https://developer.bluecats.com) for SDK documentaiton and getting started guides.**

Need some beacons? Check out our online store for a [StarterPack](http://store.bluecats.com/collections/featured-products/products/bluecats-starterpack-with-usb) or email our [sales team](mailto:sales@bluecats.com).

## Android SDK Installation  
### Step 1.
Installing the SDK into your project.

#### a) Using Eclipse
Copy the bluecats_sdk.jar and rest of the [ABI](https://developer.android.com/ndk/guides/abis.html) folders (armeabi, armeabi-v7a, etc) from this git repository into your project's libs folder.

The bluecats_sdk.jar will need to be copied in to the libs folder AS WELL AS the appropriate libbluecats_sdk.so (contained in the various jni build folders). You may copy only the build needed for your app, or all of them if you are unsure exactly which are needed. More info on these builds can be found at the following URLs:  
[http://developer.android.com/reference/android/os/Build.html](http://developer.android.com/reference/android/os/Build.html)  
[https://developer.android.com/ndk/guides/abis.html](https://developer.android.com/ndk/guides/abis.html)

Two extra dependencies will be required if you take this path:
- [Google Play Services](https://developers.google.com/android/guides/setup) (Required version is 8.1 or above. Location and ads services are required. Either the full services library or these specific services can be added)
- [Gson](https://github.com/google/gson)

#### b) Using Android Studio
Add the following to your build.gradle:
```gradle
compile 'com.bluecats:bluecats-android-sdk:1.13.8'
```
### Step 2.
Add the following to your proguard rules:
```
-keep class com.bluecats.sdk.** {*;}
```
### Step 3.
Get an app token from [app.bluecats.com/apps](http://app.bluecats.com/apps) by clicking "Create New App" and giving your new app a name. Once created, your new app should appear in the list and you'll be able to access your app token by clicking the "Show App Token / Secret" button below it.

NOTE: If you don't already have an account on [app.bluecats.com](http://app.bluecats.com/), you will need to create one in order to progress past this point. If you're unsure of what to do, send an email to [sales@bluecats.com](mailto:sales@bluecats.com) and we'll gladly help you out!

### Requirements
#### AndroidManifest.xml
Update your AndroidManifest.xml file to add the following snippet which gives the SDK the permissions necessary to search for beacons efficiently, as well as allowing the `BlueCatsSDKService` to run.
```xml
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />

<application ...>
  ...
  <service android:name="com.bluecats.sdk.BlueCatsSDKService" />
</application>
```

If you want the SDK to start when the device starts, you may add this to your xml:
```xml
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

<application ...>
	...

	<receiver android:name="com.bluecats.sdk.BlueCatsSDKServiceReceiver" >
	    <intent-filter>
	        <action android:name="android.intent.action.BOOT_COMPLETED" />
	    </intent-filter>
	</receiver>
</application>
```
#### Android SDK 4.3+ (API Level 18+)
The SDK will still work on lower versions of Android, but Bluetooth Low Energy Scanning will be disabled. You will still be able to make use of the Sites Nearby functionality as this does not involve scanning for beacons.

### Sample Code
See the sample [BlueCats Scratching Post](https://github.com/bluecats/bluecats-scratchingpost-android) app for usage and integration instructions.

## Building Environment of Release v1.13.8

* Eclipse: 4.4.1 (20140925-1800)
* Android SDK tools: 24.4
* Android SDK platorm-tools: 23.1
* Android SDK build tools: 23.0.1
* Project target: android-23
* Google play Services: 8.4 (8487000 or r29)

## Have a Question?
* If you've found a bug, please [open an issue](https://github.com/bluecats/bluecats-android-sdk/issues).
* If you have a general question, see our [support center](support.bluecats.com) for articles on our platform and beacons.
* If you want a particular feature, please [open an issue](https://github.com/bluecats/bluecats-android-sdk/issues).
* If taking a look at our SDK for the first time, please see our [Android SDK documentation](https://developer.bluecats.com/).
