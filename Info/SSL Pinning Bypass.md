## Fiddler Setup
Go to Tools -> Connections
Turn on `Allow remote computers to connect` if not on already
and change the port if you want
## PS4 Setup
Go to Settings -> Network -> Setup Internet Connection -> Prefered Network Methode
Select `Custom` and just do the basic setup until you are promoted if you want to use a Proxy
Server, Select `Use`  and type in your Computers IP Adresse and the Port you set

## Fiddler Script

```cs 
import System;
import System.Web;
import System.Windows.Forms;
import Fiddler;

class Handlers
{ 
    static function OnBeforeRequest(oSession: Session) {
        if (oSession.hostname.Contains(".ol.epicgames.com")) {
            if (oSession.HTTPMethodIs("CONNECT"))
            {
                oSession["x-replywithtunnel"] = "FortniteTunnel";
                return;
            }
            oSession.fullUrl = "http://localhost:7877" + oSession.PathAndQuery;
        }
        else if (oSession.hostname.Contains("epicgames.net")) {
            if (oSession.HTTPMethodIs("CONNECT"))
            {
                oSession["x-replywithtunnel"] = "FortniteTunnel";
                return;
            }
            oSession.fullUrl = "http://localhost:7877" + oSession.PathAndQuery;
        }
        else if (oSession.hostname.Contains("epicgames.dev")) {
            if (oSession.HTTPMethodIs("CONNECT"))
            {
                oSession["x-replywithtunnel"] = "FortniteTunnel";
                return;
            }
            oSession.fullUrl = "http://localhost:7877" + oSession.PathAndQuery;
        }
        else if (oSession.hostname.Contains("retrac.site")) {
            if (oSession.HTTPMethodIs("CONNECT"))
            {
                oSession["x-replywithtunnel"] = "FortniteTunnel";
                return;
            }
            oSession.fullUrl = "http://localhost:7877" + oSession.PathAndQuery;
        }
    }
} 
```

Go to FModel and load up your console paks and Get the `DefaultEngine.ini` which is located under `FortniteGame/Config`
Search up `[OnlineSubsystemMcp.BaseServiceMcp]` and change the protocol to `http`
and Repack it with u4pak under the same location as the .ini


## PKG setup
you would need to have dumped fortnite yourself you cannot use the version on orbispatches since the eboot.bin is encrypted and you need a license to decrypt it
so either you have license on your ps4 which you got by actually playing the game prior to your Jailbreak or spend around 100 - 200 bucks for a Fortnite CD

you either can dump the whole Game or use AFR to redirect paks tho you would need to upload all paks to your ps4

In the uecommandline.txt change add following
`-skippatchcheck`

and launch it and you should be able to see the traffic in fiddler


