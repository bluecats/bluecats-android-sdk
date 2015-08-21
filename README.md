BlueCats SDK for Android
====================

The BlueCats' SDKs have been developed for easy integration and to offer flexiblity across different use cases.  Please let us know if you have any questions at developers@bluecats.com.

###**The BlueCats Android SDK documentation is located [here](https://github.com/bluecats/bluecats-android-sdk/wiki).**

Need some beacons? Check out our online store for a [StarterPack](http://store.bluecats.com/collections/featured-products/products/bluecats-starterpack-with-usb) or email our [sales team](mailto:sales@bluecats.com).

##Here's the basics:

####Step 1. 
Copy the com.bluecats_sdk.jar file into your project's /libs folder.

####Step 2. 
Get an appToken from [app.bluecats.com/apps](http://app.bluecats.com/apps)

####Step 3.
See the sample [BlueCats Scratching Post](https://github.com/bluecats/bluecats-scratchingpost-android) app for usage and integration instructions.

## Upgrading to Android SDK Version 1.11.0.

If you are upgrading to Version 1.11.0 you will need to make the following changes to your integration:

1. The Wake Lock permission will need to be added to your app's AndroidManifest.xml ([android.permission.WAKE_LOCK](http://developer.android.com/reference/android/Manifest.permission.html#WAKE_LOCK)).
2. The bluecats_sdk.jar will need to be copied in to the libs folder AS WELL AS the appropriate libbluecats_sdk.so (contained in the various jni build folders). You can copy only the build needed for your app, or all of them if you are unsure exactly which are needed. More info on these builds can be found at the following URLs:  
[http://developer.android.com/reference/android/os/Build.html](http://developer.android.com/reference/android/os/Build.html)  
[https://developer.android.com/ndk/guides/abis.html](https://developer.android.com/ndk/guides/abis.html)

## Requirements

####Android SDK version 4.3 and up  
- The SDK will still work on lower versions of Android, but Bluetooth Low Energy Scanning will be disabled. You will still be able to make use of the Sites Nearby functionality as this does not involve scanning for beacons.  

####Google Play Services
- The required minimum version of Google Play Service is 5.0.77-000 (r18). However we recommend the latest version of Google Play Service to be integrated.

## Have a Question?

* If you've found a bug, please open an issue.
* If you have a general question, see our [support center](support.bluecats.com) for articles on our platform and beacons.
* If you want a particular feature, please open an issue.
* If taking a look at our SDK for the first time, please see our [Android SDK documentation](https://github.com/bluecats/bluecats-android-sdk/wiki).
