BlueCats SDK for Android v1.10.3
====================

This release is a workaround for a GPS issue in release 1.10.2 that was causing excessive battery drain on the device if GPS was enabled.

The issue is with Google's LocationServices.FusedLocationApi not releasing a hold on GPS for its location updates. 
