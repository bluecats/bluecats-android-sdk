BlueCats SDK for Android
====================

After JCenter sunsets, Our SDK is now available on Maven Central, make sure you add `MavenCentral()` in your repositories of build.gradle.

The BlueCats' SDKs have been developed for easy integration and to offer flexibility across different use cases. Please email us at <a href="mailto:developers@bluecats.com">developers@bluecats.com</a> if you have any questions!

**See the [BlueCats Developer Portal](https://developer.bluecats.com) for SDK documentation and getting started guides.**

Need some beacons? Check out our online store for a [StarterPack](http://store.bluecats.com/collections/featured-products/products/bluecats-starterpack-with-usb) or email our [sales team](mailto:sales@bluecats.com).

## Change Logs

### v2.1.4-r5
* Improved background notifications.

### v2.1.4-r4
* Improved startup scanning, more reliable scan results. Fixed bug with beacon region caching.

### v2.1.4-r3
* Added support for beacon settings updates for newer beacon models.

### v2.1.4-r2
* Added additional security features.

### v2.1.4
* Fixed an issue with the Local Storage Manager being null when the SDK is stopped and restarted in the background on Android 8.

### v2.1.3
* Added an embedded BCBeaconManagerCallback instance to enable background scan for the situations when the BlueCatsSDK is running but no app compoments are able to receive beacons list, especially for Android 8+. See Sample Code here in [background-scan branch](https://github.com/henrybluecats/JobServiceSample/tree/background-scan)

### v2.1.2
* Support Android O+ for the background execution limits.
* Stability Update. 

### v2.0.7
* Stability Update. Fix for ANR scenario during SDK shutdown after stopPurring request.

### v2.0.5
* Stability Update. Fix for potential crash scenario during SDK shutdown after stopPurring request.

### v2.0.4
* Stability Update. Fixes sqlite warnings. Adds support for StrictMode during debug. Fixes for potential Local Storage (sqlite) crashes.

### v2.0.3
* Optimised Beacon sync.
* Optimised stability.

### v2.0.2
* A new BCLogManager is introduced to manage SDK logs in scope of App for debug purpose.[See example](https://gist.github.com/henrybluecats/c08d8726d5607cde8cc23b2abac36ae6)
* Optimised beacon scanner for Android 7.

### v2.0.1
* Eddystone formats are supported.
* A new BCBeaconManager is available to filter BlueCats Beacon, iBeacon, Eddystone, etc.
* Google Play Service dependency is removed.

See Release Notes and the [migration guide](https://developer.bluecats.com/guides/android-migrating-from-1-13-8-to-2-0-0-2-0-1) for more details.

## Android SDK Installation  
### Step 1.
#### a) Using Android Studio
Installing the SDK into your project by adding the following to your build.gradle:
```gradle
repositories {
    mavenCentral()
}

implementation 'com.bluecats:bluecats-android-sdk:2.1.4'
```

It will automatically add the extra dependencies for you:
```gradle
compile 'com.google.code.gson:gson:2.4'
compile 'com.android.support:support-compat:24+'
compile 'com.android.support:support-core-utils:24+'
```

If you want to use your own dependencies on Gson and Support with another version, exclude the transitive dependencies like this:
```gradle
compile('com.bluecats:bluecats-android-sdk:2.1.4', {
        exclude group: 'com.google.code.gson', module: 'gson'
        exclude group: 'com.android.support', module: 'support-compat'
        exclude group: 'com.android.support', module: 'support-core-utils'
    })
```
Please **NOTE** that missing Gson or Support dependencies will cause a **runtime crash** due to ClassNotFoundException, so only exclude them from BlueCats SDK if you are sure you've included the correct dependencies in build.gradle.

### b) Using Eclipse
Follow the instructions detailed [here](https://gist.github.com/henrybluecats/33d11f7852b2d24157e9820543f88ede).

### Step 2.
Add the following to your ProGuard rules:
```
-renamesourcefileattribute SourceFile
-keepattributes LineNumberTable, SourceFile

-keep class com.bluecats.sdk.** {*;}
```

### Step 3.
Get an app token from [app.bluecats.com/apps](http://app.bluecats.com/apps) by clicking "Create New App" and giving your new app a name. Once created, your new app should appear in the list and you'll be able to access your app token by clicking the "Show App Token / Secret" button below it.

NOTE: If you don't already have an account on [app.bluecats.com](http://app.bluecats.com/), you will need to create one in order to progress past this point. If you're unsure of what to do, send an email to [sales@bluecats.com](mailto:sales@bluecats.com) and we'll gladly help you out!

### Requirements
#### AndroidManifest.xml
While the following XML isn't vital to add manually (the SDK adds it automatically), it's kept here for the sake of ensuring you understand what is required of the SDK. The permissions and service is the absolute minimum required to allow the SDK to run.
```xml
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />

<application ...>
  ...
  <service android:enabled="true" android:name="com.bluecats.sdk.BlueCatsSDKService" android:permission="android.permission.BIND_JOB_SERVICE"/>
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

#### Android 8.0+ (Oreo) Background Execution Limits
Android 8 imposes limitations on what apps can do while running in the background. If there are no foreground componants running(include Activity or Foreground Service), the system will then shutdowns the app's background services as if the app had had called the services' Service.stopSelf() methods. And calling startService() method with no foreground componants running will cause an IllegalStateException to be thrown. See [more](https://developer.android.com/about/versions/oreo/background)

#### Android 6.0+ (Marshmallow) Location Permissions
Android 6.0+ introduces a new permission model which changes the way Location Services permissions are managed. Before scanning for beacons the app is required to request location permissions from the user via a system dialogue. Detailed information on implementing location permission support in Android 6.0 can be found [here](https://developer.bluecats.com/guides/android-6-0-and-location-services-permissions).

#### Android SDK 4.3+ (API Level 18+)
The SDK will still work on lower versions of Android, but Bluetooth Low Energy Scanning will be disabled. You will still be able to make use of the Sites Nearby functionality as this does not involve scanning for beacons.

### Sample Code
See the sample [BlueCats Scratching Post](https://github.com/bluecats/bluecats-scratchingpost-android) app for usage and integration instructions.

## Building Environment of Release v2.1.4-r2
* Android Studio 3.4.1
* Android Gradle Plugin 3.1.2
* Gradle Version 4.4
* Android NDK r17
* Android SDK Tools 26.1.1
* Android SDK Platform-Tools 28.0.3
* Android SDK Build Tools 28.0.3
* Java Version: 8
* OS: MAC OSX 10.13.6

## Have a Question?
* If you've found a bug, please [open an issue](https://github.com/bluecats/bluecats-android-sdk/issues).
* If you have a general question, see our [support center](support.bluecats.com) for articles on our platform and beacons.
* If you want a particular feature, please [open an issue](https://github.com/bluecats/bluecats-android-sdk/issues).
* If taking a look at our SDK for the first time, please see our [Android SDK documentation](https://developer.bluecats.com/).
