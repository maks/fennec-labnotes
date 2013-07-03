# Implementing HTTP Authenticated Proxies

## Purpose

Need to be able to authenticate with a http proxy using basic auth **without** showing any UI to the user, the proxy-hostname/username/password all need to come from settings via opensign agent.


## src code

The code for handling 407s (Proxy Authentication) is in netwerk/protocol/http/nsHttpChannel.cpp with the Authentication bit being the interface in: netwerk/protocol/http/nsIHttpChannelAuthProvider.idl and implementation in: netwerk/protocol/http/nsHttpChannelAuthProvider.cpp

But for our purposes, we want to have a non-interactive AuthProvider implementation...

SetProxyCredentials() in line 1312 of nsHttpChannelAuthProvider.cpp seems to be what actually puts the auth header fields into the request.

### Now how to get proxy username, password into there?

## Using FF Prefs

mobile prefs in: mobile/android/app/mobile.js


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

__Now how does Java code set Firefox prefs?__

## Testing

Once we actually have something working in FF this should be a simple way to test it: http://stackoverflow.com/questions/724599/setting-up-an-apache-proxy-with-authentication