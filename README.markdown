## SteamBox - SteamPunk themed PirateBox clone for Android

Screen shot (computer):
<a target="_blank" href="https://github.com/thedod/SteamBox/raw/master/gfx/Screenshot.jpg"><img border="0" height="100" src="https://github.com/thedod/SteamBox/raw/master/gfx/Screenshot.jpg" alt="Screenshot"></a>
Upload notification (phone):
<a target="_blank" href="https://github.com/thedod/SteamBox/raw/master/gfx/upload-notification.jpg"><img border="0" height="100" src="https://github.com/thedod/SteamBox/raw/master/gfx/upload-notification.jpg" alt="Upload notification"></a>

* [PirateBox](http://wiki.daviddarts.com/PirateBox) by _David Darts_ is both useful and damn fine looking.
* _pspunderground_ has [sorta] [ported it to android](http://forum.xda-developers.com/showthread.php?t=935157) (based on _Jochen Ruehl's_ [PAW](http://paw-android.fun2code.de/) beanshell-powered web server).
* **SteamBox** is a SteamPunk theme for that project that doesn't require a rooted phone (can't serve on port 80, tough).

### Features:

* Original [Android PirateBox](http://forum.xda-developers.com/showthread.php?t=935157) functionality: upload/browse/download
* Shoutbox (no chat yet) - change a single-line global message. Optional text to speech
  (which is fun if the droid is connected to an amp and playing music - try it)
* Notification when file is uploaded (vibration, no sound, see above why)
* Large url display + QR code to help others easily join the pirate party
* SteamPunk look and pirate-friendly GUI :)

----

<img width="99" height="33" alt="lal" src="http://artlibre.org/wp-content/lal2.png" title="lal" class="alignnone size-full wp-image-632"> _PirateBox_ was created by <a href="http://daviddarts.com">David Darts</a> and is registered under the
 <a href="http://artlibre.org/licence/lal/en">Free Art License (FAL 1.3)</a>.
The Free Art License grants the right to freely copy, distribute, and transform creative works according to the principles of <a href="http://www.gnu.org/copyleft/copyleft.html">copyleft</a>. This license also applies to any derivative works including (but not limited to) _SteamBox_.

----

### To install:

(You'll need a file manager that can handle zip files).

* Install [PAW Server](http://paw-android.fun2code.de/).
\[[QR Code](http://paw-android.fun2code.de/images/paw_android_qr_code.png)].
* Run Paw, and let it extract the initial `/sdcard/paw/` folder. **Do not** press the "play" button to start the server yet.
* [Download SteamBox](https://github.com/thedod/SteamBox/archives/master)
  \[[QR code](http://chart.apis.google.com/chart?cht=qr&chs=100x100&chl=https%3A%2F%2Fgithub.com%2Fthedod%2FSteamBox%2Fzipball%2Fmaster)],
  and extract the `SteamBox/` and `conf/` folders to `/sdcard/paw/` (Overwriting existing content at `conf/`).

### To start the Wi-Fi hotspot:

* Go to `Wireless & networks` settings,
* Under `Mobile networks`, **Make sure `Data enabled` isn't checked**
  (you don't want to be an internet provider for untrusted strangers).
* Under `Tethering & portable hotspot` / `Potable Wi-Fi hotspot settings`,
  configure `SSID` to be _piratebox_ and `Secruity` to be _Open_.
* Check the `Portable Wi-Fi hotspot` checkbox, and you're live.

### To start the server:
Run the PAW app, press the "play" button, and it will tell you where to browse.

### Tips:

* If you've configured the Wi-Fi hotspot as suggested, you can browse to `/qrhotspot.png` and show
  it to people who want quick Wi-Fi setup.
* After you upload the first file, the folder `/sdcard/piratebox/` will be created.
  It's handy to have a shortcut to it on your phone, so that you can clean up
  the mess there once in a while.
* You can also run the app without setting the phone up as a Wi-Fi hotspot.
  It won't be a PirateBox then, but it would still be convenient for file exchange
  (much less of a hassle than blue-tooth). I do both. I hope I'm not breaking any
  pirate rules by this :)

----

#### Enjoy it. Skin it. It's fun.

----

### Advanced:

#### Why you sometimes don't see the frame with the QR code, and how to fix this

SteamBox doesn't _generate_ QR codes by itself [at least not yet]. It's actually a simple JS "cheat":
The page tries to lookup the [pregenerated] image `/sdcard/paw/SteamBox/qrdcodes/`protocol`-`ip`-`port`.png`

For example: `http-192.168.1.23-8080.png` is expected to contain a 100x100 pixel QR code for `http://192.168.1.23:8080`.

If there's an error (image doesn't exist) the entire luxurious QR Code frame gets hidden. No harm done, but it kinda ties the room together :)

Now `http-192.168.43.1-8080.png` and `https-192.168.43.1-4031.png` are already in the distribution,
so you're covered as long as you _run your droid as a Wi-Fi hotspot_, but if you want to run the server
in an _existing Wi-Fi lan_ where your droid is at - say -
`192.168.1.23` and SteamBox runs as `https` over port `4031`, out-of-the-box SteamBox won't find `https-192.168.1.23-4031.png`.

You can easily generate a "SteamBox ready" QR code for your server: 
Just extract the file `tools/qrmaker.html` and open it with your browser or html viewer.
Read the instructions and use the form to manually generate the QR Code you need via google API.

#### How to run PAW as an SSL server

**Warning:** PAW is a beta product and shouldn't be trusted for critical encryption.

    On the other hand, PirateBox is a good scenario to experiment with Android security practices and tools,
    since the threat is relatively small: The information that can be gathered amounts to
    "person x has uploaded/download file y". The content of file y is public to begin with.

* On you computer, use [portecle](http://portecle.sourceforge.net/) to create an rsa key and save it
  to a safe place (e.g. a [TrueCrypt](http://www.truecrypt.org/) device) as a `.bks` file.
* Turn off PAW.
* Replace `/sdcard/paw/conf/certs/pawKeystore` (_without_ a `.bks` extension) with your file.
* At `/sdcard/paw/conf/`, copy `4031/server.xml` to `server.xml` (overwriting it. There's a copy
  of it at `8088/server.xml` if you want to go back to http).
* Start the server and connect to it (https on port 4031). You'll get the certificate warning,
  and should see the details of your key (not the default [fun2code](https://github.com/thedod/SteamBox/raw/master/SteamBox/images/fun2code-cert.jpg) one).

**Note:** Each time _Paw server_ app gets upgraded (e.g. from the market), it overwrites `/sdcard/paw/conf/certs/pawKeystore` the next time it runs and you need to replace it with your own key again.

To avoid [man-in-the-middle attacks](https://secure.wikimedia.org/wikipedia/en/wiki/Man-in-the-middle_attack), you should
keep the fingerprints of your key in a text file on your phone. It's also handy to have it on paper, but make it a point
that _you only have one copy and you need it back_. If there are several copies running around at a party, it's switcheroo
waiting to happen.

All in all - unless it's a small group of technically skilled people - you're better of with plain http :)

