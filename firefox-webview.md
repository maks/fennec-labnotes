# Modifying stock Firefox to work as a webview aka Opensign-view

## Building Firefox for Android (aka Fennec)

* [Instructions on getting source, setting up build env, build steps etc](https://wiki.mozilla.org/Mobile/Fennec/Android)
* [Useful architecture info about Firefox on Android](https://wiki.mozilla.org/Fennec/NativeUI)

### Hg Sidebar

Firefox is stored in Hg (mercurial). So some useful Hg commands:
``` 
hg pull && hg update #to get the latest code
hg status # same as git
hg diff # same as git 
hg revert --all ## DISCARD all changes since last commit
```

## Java side activity

Firefoxes android app manifest is in ```mobile/android/base/AndroidManifest.xml.in```

The important part of the manifest is that it points to the App class to be launched for all its intents, which is just a place-holder subclass of BrowserApp which is where all the functionality is implemented. 

But there is also WebApp which again just subclasses WebAppImpl which implements the features needed for Firefoxes new packaged installable apps from the Firefox Marketplace.

There are also a bunch of extra activities (eg. awesomebar, settings) and services (eg. password provider, notification provider, etc) that we probably need to strip-out down the track.

### Custom Activity

* So we implement our own subclass on GeckoApp (OpensignApp.java)
* We add it to AndroidManifest.xml attached to the intent Action ```au.com.sct.opensign.FFWEBVIEW``` the url should be the Intents data attribute.

### Bugs

* [no audio playback](https://bugzilla.mozilla.org/show_bug.cgi?id=879651)

### HTTP Authenticated Proxies

The code for handling 407s (Proxy Authentication) is in netwerk/protocol/http/nsHttpChannel.cpp with the Authentication bit being the interface in: netwerk/protocol/http/nsIHttpChannelAuthProvider.idl and implementation in: netwerk/protocol/http/nsHttpChannelAuthProvider.cpp

But for our purposes, we want to have a non-interactive AuthProvider implementation...

SetProxyCredentials() in line 1312 of nsHttpChannelAuthProvider.cpp seems to be what actually puts the auth header fields into the request.

### Now how to get proxy username, password into there?

something like this might work via using prefs:
```
static const char kAllowProxies[] = "network.automatic-ntlm-auth.allow-proxies";

...

nsCOMPtr<nsIPrefBranch> prefs = do_GetService(NS_PREFSERVICE_CONTRACTID);
    if (!prefs)
        return;

    if (isProxyAuth) {
        bool val;
        if (NS_FAILED(prefs->GetBoolPref(kAllowProxies, &val)))
            val = false;
        LOG(("Default credentials allowed for proxy: %d\n", val));
        return val;
    }
```
