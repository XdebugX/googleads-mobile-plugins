About
=====

Copyright 2013 Google Inc. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

Features
--------=
This is the AdMob Unity Plugin for Android.  It provides a way to request
AdMob ads from a Unity project.  This plugin was written and tested with
the Google AdMob SDK version 6.4.1 for Android, and Unity 4.1.5.

The AdMob Unity plugin contains a .unitypackage file for those that want to
easily import the plugin, as well as the source code.

Requirements:
--------------
* Unity Pro 4.1.5 (untested on previous versions)
* Google AdMob SDK for Android
* AdMob publisher ID

Directions for importing the plugin:
--------------------------------------
1. Open your project in the Unity editor.
2. On the top toolbar, select "Assets" -> "Import Package" -> "Custom Package".
3. Select the AdMobUnityPlugin.unitypackage file.
4. Import all of the files for the plugins by selecting "Import". Make sure
   to check for any conflicts with files.
5. Drag the AdMobPlugin prefab from the Plugins/AdMobPlugin/ folder into
   your Unity scene.

Plugin integrations steps - Android:

1. If you don't already have an AndroidManifest.xml in Plugins/Android/, copy
   the AndroidManifest.xml from Temp/StagingArea into Plugins/Android/.
2. Update Plugins/Android/AndroidManifest.xml and add the necessary AdMob
   activities and permissions as explained in
   https://developers.google.com/mobile-ads-sdk/docs#android
3. Add the Google AdMob SDK jar into Plugins/Android.

The plugin also comes with an example plugin usage script, which is already
attached to the AdMobPlugin component for convenience. Simply edit
Plugins/AdMobPlugin/AdMobPluginDemoScript.cs and include your ad unit ID
and run your project to see AdMob working.


AdMob Unity Plugin API
-----------------------
The plugin provides the following AdMob methods:

1. CreateBannerView

   Takes in a publisherId string as well as a constant for the ad size. The
   last boolean parameter denotes whether the ad should be shown at the top
   or bottom of the screen.

   An example call placing the ad at the top of the screen is provided below:

   AdMobPlugin.CreateBannerView ("INSERT_YOUR_AD_UNIT_ID_HERE",
                                 AdMobPlugin.AdSize.Banner,
                                 true);
2. RequestBannerAd

   Takes in a testing flag as well as an optional string representing a list
   of extras. If you don't have any extras, you can request a live ad with:

   AdMobPlugin.RequestBannerAd(false);

   An example call requesting a test ad with some extras is shown below:

   string extras = "{\"color_bg\":\"AAAAFF\", \"color_text\":\"FFFFFF\"}";
   AdMobPlugin.RequestBannerAd(true, extras);

   NOTE: Make sure to use correctly formed JSON when passing an extras string.

3. HideBannerView

   Called after a BannerView has been created. This method can hide the ad from
   showing on screen. An example call of this is shown below:

   AdMobPlugin.HideBannerView();

4. ShowBannerView

   Called after a BannerView has been created, this method can show any ad that
   has been hidden. An example call of this is shown below:

   AdMobPlugin.ShowBannerView();

This plugin also allows you the option to listen for ad events. The following
events are supported:

    public static event Action ReceivedAd;
    public static event Action<string> FailedToReceiveAd;
    public static event Action ShowingOverlay;
    public static event Action DismissedOverlay;
    public static event Action LeavingApplication;

Registering for an event can be done using the += operater as is shown below:

    // Assume HandleReceivedAd is your function.
    AdMobPlugin.ReceivedAd += HandleDidReceiveAd;

Remember to un-register for events when you're cleaning up your GameObjects.
You can unregister using the -= operator as is shown below:

    // Assume HandleReceivedAd is your function.
    AdMobPlugin.ReceivedAd -= HandleDidReceiveAd;

Updating the plugin
---------------------

The plugin's .unitypackage only includes the compiled Android library project
with AdMob implementation. If you want to make changes to the library or see
the source code, you can find the project in the examples-android repository.

Additional Resources:
---------------------
https://developers.google.com/mobile-ads-sdk/docs
https://groups.google.com/group/google-admob-ads-sdk
https://plus.google.com/+GoogleAdsDevelopers

