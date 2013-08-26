# Notes

## References

* [MDN Firefox on Android landing page](https://developer.mozilla.org/en-US/docs/Mozilla/Firefox_for_Android)
* [Getting started with building extensions](https://developer.mozilla.org/en-US/docs/Building_an_Extension)
* [Content html talking to extension code] (https://developer.mozilla.org/en-US/docs/Code_snippets/Interaction_between_privileged_and_non-privileged_pages#Resources)
* [Q & A for 2 way comms] (http://stackoverflow.com/questions/13350595/how-to-organize-a-two-way-communication-with-the-firefox-extension-code-injectio)
* [MDN docs on 2 ways comms between ext and content](https://developer.mozilla.org/en-US/docs/Code_snippets/Interaction_between_privileged_and_non-privileged_pages#Chromium-like_messaging.3A_json_request_with_json_callback)
* [Filesystem access in extension](https://developer.mozilla.org/en-US/docs/Code_snippets/File_I_O?redirectlocale=en-US&redirectslug=Code_snippets%252FFile_I%252FO)
* [Intercepting HTTP requests/reponses Q&A](http://stackoverflow.com/questions/1695440/altering-http-responses-in-firefox-extension?rq=1)
* [FF extensions built from greasemonkey scripts](http://geo.inge.org.uk/grease-vervet.php)
* [Intercepting Page Load](https://developer.mozilla.org/en-US/docs/XUL/School_tutorial/Intercepting_Page_Loads?redirectlocale=en-US&redirectslug=XUL_School%2FIntercepting_Page_Loads#HTTP_Observers)
* [Intercepting http responses with addon SDK Q&A](stackoverflow.com/questions/7812604/firefox-extension-observing-response)

## Useful Moz links

* [Tinderbox - Moz's CI Service](https://tbpl.mozilla.org/)

### Add-ons SDK 

## Basics

* need to create install.rdf and bootstrap.js [as per](https://developer.mozilla.org/en-US/docs/Extensions/Mobile/Walkthrough)
* **BUG** When testing on a android device beware of [this bug](https://bugzilla.mozilla.org/show_bug.cgi?id=762648) which prevents installing the extension xpi from sdcard.

The add-ons SDK is (hopefully) a newer and nicer more high-level way to develop firefox extensions. 

[Mobile add-ons docs](https://addons.mozilla.org/en-US/developers/docs/sdk/1.12/dev-guide/tutorials/mobile.html)

*NOTE:* make sure you are using the latest stable SDK to match the latest version of Firefox for Android otherwise you may get errors trying to run your add-on xpi using cfx tool or the generated xpi may have strange errors with globals not being defined in content script scope, etc.

### Budnling XPIs (addons) in Fennec APK

[see this bug](https://bugzilla.mozilla.org/show_bug.cgi?id=754312)

### Communication between content scripts and normal html pages in Add-on SDK based extensions

This is documented [here](???) 