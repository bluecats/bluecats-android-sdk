BlueCats SDK for Android v1.10.3
====================

This release is a workaround for a GPS issue in release 1.10.2 that was causing excessive battery drain on the device if GPS was enabled.

The issue is with Google's LocationServices.FusedLocationApi not releasing a hold on GPS for its location updates. 

##Pre-requisites:

* This issue is independant of whether bluetooth is on or off.
* Location services on - must be high accuracy (GPS enabled).

##Steps to reproduce:

1. Install app with SDK version 1.10.2.
2. Run app for 30 - 60 minutes.
3. Verify the app appears in the Battery Usage list. Appearance in the list will vary depending on the device and what other apps are running, so may need to extend the test time until the app appears. If test time is longer make a note of time taken for the app to appear.
4. Tap into detail and line item for GPS usage duration will show approximiately 50-100% of duraction the app test has been running.

##Steps to verify fix:

1. Uninstall app with SDK version 1.10.2.
2. Install app with SDK version 1.10.3.
3. Run app for the duration used above to verify problem.
4. Verify the app does not appear in the Battery Usage list, or very low in the list (this may still be possible if the device has few other services running).
5. If the app is present viewing details for GPS usage should be 0 or a low number of seconds.
