BlueCats SDK for Android
====================

[ ![Download](https://api.bintray.com/packages/bluecats/maven/bluecats-android-sdk/images/download.svg) ](https://bintray.com/bluecats/maven/bluecats-android-sdk/\_latestVersion)

The BlueCats' SDKs have been developed for easy integration and to offer flexibility across different use cases. Please email us at <a href="mailto:developers@bluecats.com">developers@bluecats.com</a> if you have any questions!

**See the [BlueCats Developer Portal](https://developer.bluecats.com) for SDK documentation and getting started guides.**

Need some beacons? Check out our online store for a [StarterPack](http://store.bluecats.com/collections/featured-products/products/bluecats-starterpack-with-usb) or email our [sales team](mailto:sales@bluecats.com).

## Change Logs
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
#### a) Using Android
Installing the SDK into your project by adding the following to your build.gradle:
```gradle
compile 'com.bluecats:bluecats-android-sdk:2.0.3'
```

It will automatically add the extra dependencies for you:
```gradle
compile 'com.google.code.gson:gson:2.2.4'
compile 'com.android.support:support-compat:24.2.0'
compile 'com.android.support:support-core-utils:24.2.0'
```

### b) Using Eclipse
Follow the instructions detailed [here](https://gist.github.com/henrybluecats/33d11f7852b2d24157e9820543f88ede).

### Step 2.
Add the following to your ProGuard rules:
```
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

#### Android 6.0+ (Marshmallow) Location Permissions
Android 6.0+ introduces a new permission model which changes the way Location Services permissions are managed. Before scanning for beacons the app is required to request location permissions from the user via a system dialogue. Detailed information on implementing location permission support in Android 6.0 can be found [here](https://developer.bluecats.com/guides/android-6-0-and-location-services-permissions).

#### Android SDK 4.3+ (API Level 18+)
The SDK will still work on lower versions of Android, but Bluetooth Low Energy Scanning will be disabled. You will still be able to make use of the Sites Nearby functionality as this does not involve scanning for beacons.

### Sample Code
See the sample [BlueCats Scratching Post](https://github.com/bluecats/bluecats-scratchingpost-android) app for usage and integration instructions.

## Building Environment of Release v2.0.3
* Android Studio 2.1.3
* Android Gradle Plugin 2.1.3
* Gradle Version 2.14.1
* Android NDK r11
* Android SDK Tools 25.1.7
* Android SDK Platform-Tools 24
* Android SDK Build Tools 24.0.1
* Java Version: 8
* OS: MAC OSX 10.11.5

## Have a Question?
* If you've found a bug, please [open an issue](https://github.com/bluecats/bluecats-android-sdk/issues).
* If you have a general question, see our [support center](support.bluecats.com) for articles on our platform and beacons.
* If you want a particular feature, please [open an issue](https://github.com/bluecats/bluecats-android-sdk/issues).
* If taking a look at our SDK for the first time, please see our [Android SDK documentation](https://developer.bluecats.com/).
