# Using Firefox as a webview

## Building Firefox for Android (aka Fennec)

* [Instructions on getting source, setting up build env, build steps etc](https://wiki.mozilla.org/Mobile/Fennec/Android)
* [Useful architecture info about Firefox on Android](https://wiki.mozilla.org/Fennec/NativeUI)

## Java side activity

Firefoxes android app manifest is in ```mobile/android/base/AndroidManifest.xml.in```

The important part of the manifest is that it points to the App class to be launched for all its intents, which is just a place-holder subclass of BrowserApp which is where all the functionality is implemented. 

But there is also WebApp which again just subclasses WebAppImpl which implements the features needed for Firefoxes new packaged installable apps from the Firefox Marketplace.

There are also a bunch of extra activities (eg. awesomebar, settings) and services (eg. password provider, notification provider, etc) that we probably need to strip-out down the track.








