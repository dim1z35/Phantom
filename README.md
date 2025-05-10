# Phantom

![Imgur](https://i.postimg.cc/y6bNgxgC/phantom-logo.png)

Phantom is an OG Fortnite Project written in [JavaScript](https://en.wikipedia.org/wiki/JavaScript)

Created by [Dim1Z](https://github.com/dim1z35), This is a fortnite backend

## How to start Phantom
1) Install [NodeJS](https://nodejs.org/en/) and [MongoDB](https://www.mongodb.com/try/download/community).
2) **Download** and **Extract** Phantom.
3) Run **"install_packages.bat"** to install all the required modules.
4) Go to **Config/config.json** in the directory you extracted Phantom into.
5) Open it, set your discord bot token and **save it**. The discord bot will be used for creating accounts and managing your account.
6) Run **"start.bat"** or run the command `node index.js` in a cmd, if it has no errors, it should work.
7) Use something to redirect the Fortnite servers to **localhost:8080**, *I recommend u to use fiddler*
8) When Fortnite launches and is connected to the backend, enter your email and password (or an exchange code) then press login. It should let you in.

### For login
You need to use the **FortniteLauncher.exe** and also the **AntiCheat**

If you are using [Fiddler](https://www.telerik.com/download/fiddler) you can use this script:

```
import Fiddler;

class Handlers
{
    static function OnBeforeRequest(oSession: Session) {

        if (oSession.PathAndQuery.Contains("/caldera/api/v1/launcher/racp"))
        {
            if (oSession.HTTPMethodIs("CONNECT"))
            {
                oSession["x-replywithtunnel"] = "ServerTunnel";
                return;
            }
            oSession.fullUrl = "http://127.0.0.1:5000" + oSession.PathAndQuery
        }
        if (oSession.hostname.Contains("epicgames"))
        {
            if (oSession.HTTPMethodIs("CONNECT"))
            {
                oSession["x-replywithtunnel"] = "ServerTunnel";
                return;
            }
            oSession.fullUrl = "http://127.0.0.1:3551" + oSession.PathAndQuery
        }
    }
}
```

if u change **Caldera Service port** modify this string on **fiddler script**: `oSession.fullUrl = "http://127.0.0.1:urport" + oSession.PathAndQuery`
if u change **Backend port** modify this string on **fiddler script**: `oSession.fullUrl = "http://127.0.0.1:urport" + oSession.PathAndQuery`

After that go to the build folder **(/FortniteGame/Binaries/Win69)** and create a file with the name **launch.bat** or whatever you prefer and insert this code inside it:

```bat
@echo off
set /p code=code: 
start "" "FortniteLauncher.exe" -obfuscationid=WXis54njnKX1MJqoH0uRwdzlbQ1uqQ -AUTH_LOGIN=unused -AUTH_PASSWORD=%code% -AUTH_TYPE=exchangecode -epicapp=Fortnite -epicenv=Prod -EpicPortal -epicsandboxid=fn -noeac -noeaceos -fromfl=be 
```

Launch it, then go to Discord and type **/exchange-code**, copy the code and paste it into the .bat file.

### Tested versions: 
Right now the only tested version is **27.11**, if you test version, have questions or anything please make a ticket or a pull request [In the official repo](https://github.com/xLoigi/CalderaService).

## License
This **project/backend** is licensed under the **BSD 3-Clause License.**

## Credits
Credits to **dim1_z** on Discord!
