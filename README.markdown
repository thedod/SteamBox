## SteamBox - a SteamPunk Android PirateBox theme

Screen shot:
<a target="_blank" href="https://github.com/thedod/SteamBox/raw/master/gfx/Screenshot.jpg"><img border="0" height="100" src="https://github.com/thedod/SteamBox/raw/master/gfx/Screenshot.jpg" alt="Screenshot"></a>
Upload notification:
<a target="_blank" href="https://github.com/thedod/SteamBox/raw/master/gfx/upload-notification.jpg"><img border="0" height="100" src="https://github.com/thedod/SteamBox/raw/master/gfx/upload-notification.jpg" alt="Upload notification"></a>

* [PirateBox](http://wiki.daviddarts.com/PirateBox) by _David Darts_ is both useful and damn fine looking.
* _pspunderground_ has [sorta] [ported it to android](http://forum.xda-developers.com/showthread.php?t=935157) (based on _Jochen Ruehl's_ [PAW](http://paw-android.fun2code.de/) beanshell-powered web server).
* **SteamBox** is a theme for that project.

### Features:

* Original Android PirateBox functionality: upload/browse/download
* Shoutbox (no chat yet) - change a single-line global message. It also gets spoken as text to speech
  (which is fun if the droid is connected to an amp and playing music - try it).
* Notification when file is uploaded (vibration, no sound, see above why).
* Large url display + QR code to help others easily join the party.
* [Relatively] spiffy design :)

### To install:

* [Download SteamBox](https://github.com/thedod/SteamBox/archives/master) (or clone/fork it).
* Install [pspunderground's apk](http://forum.xda-developers.com/showthread.php?t=935157).
* rename `/sdcard/paw/html` (to keep it as a backup) and use the `html` folder from SteamBox instead.

#### Why you sometimes don't see the QR code and how to fix this

SteamBox doesn't _generate_ QR codes by itself [at least not yet]. It's actually a simple JS "cheat":
The page tries to lookup the [pregenerated] image `/sdcard/paw/html/qrdcodes/`protocol`-`ip`-`port`.png`

For example: `http-192.168.1.23-8080.png` is expected to contain a 100x100 pixel QR code for `http://192.168.1.23:8080`.

If there's an error (image doesn't exist) the entire luxurious QR Code frame gets hidden. No harm done, but it kinda ties the room together :)

Now `http-192.168.43.1-8080.png` and `https-192.168.43.1-4031.png` are already in the distribution,
so you're covered as long as you _run your droid as a wifi hotspot_, but if you want to run the server
in an _existing wifi lan_ where your droid is at - say -
`192.168.1.23` and SteamBox runs as `https` over port `4031`, out-of-the-box SteamBox won't find `https-192.168.1.23-4031.png`.

You can easily generate a "SteamBox ready" QR code for your server: 
Just open the file `tools/qrmaker.html` in your browser (from hard disk. no special voodoo required),
and use the form to manually generate the QR Code you need via google API.

#### Enjoy it. Skin it. It's fun.
