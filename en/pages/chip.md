# C.H.I.P.

## Drivers

[C.H.I.P. Driver for Windows](https://bbs.nextthing.co/t/need-gadget-serial-v2-4-driver-for-windows-7/2044/5)

If you're using Windows 10, this won't work. All drivers need to be signed18, so plain inf files won't do it for you. If you don't feel like downloading the Windows Driver Kit and signing the driver yourself, you can download a signed copy by searching github for 'linux-cdc-acm.inf', or you can use the driver currently in use on my system138 (it's crypto-signed by Microsoft12 for Pyramid Innovation17, so it should be safe to use).

[Need Gadget Serial v2.4 Driver for Windows](https://bbs.nextthing.co/t/need-gadget-serial-v2-4-driver-for-windows-7/2044/11)

joshua013914d
I found the solution so you can enjoy 4.4 "mine was 4.4 headless" without having to revert back to 4.3 GUI

Connecting from my computer to my Chip via Micro-usb
from a Windows 10 64bit pc
I successfully flash my chip after having to restart my chrome browser after installing the flasher addon.
After flashing my chip from 4.3 GUI to 4.4 Headless, it changed my device into a cdc composite gadget, I never flashed back to 4.3 GUI as I wanted to try 4.4.

Basically, find your device "unknown device" or cdc composite gadget. in device manager.

right click and update driver
now click Browse my computer for driver software
now click the "let me pick from a list of device drivers on my computer"
Under manufacturer and scroll to Pyramid Innovation Ltd.
Select PI USB to Serial
now click next.
windows will now warn you that it may make the device not function correctly, click yes.
now you should have a PI USB to Serial (COM#)

Apparently the flasher doesn't restore the driver for your Chip so you must do it manually.

## Tweaks

[Changing Background on PocketCHIP](https://bbs.nextthing.co/t/personalization-of-gui/5167)

To 'easily' complete this task you will need:

Desktop computer
USB Flash Drive
And a Pocketchip

Okay, so first things first you need a background image! Any picture can work, just make sure you resize the image on your desktop computer to 480x272 (I used Adobe Photoshop to resize the canvas, but I'm sure Blender GIMP ((a free program, can also be used)@UnixOutlaw also mentions some other great alternatives in the comments below), save the image as mainBackground.png(exactly the same making sure to capitalize when needed!) to your USB flash drive.

Next, Get your Pocketchip and go to Browse Files. Navigate to /usr/share/pocket-home and find the picture that is named mainBackground.png. Highlight it (don't select it) and click EDIT>COPY in the tool bar at the top of the screen. Once you have copied your image navigate to your Pictures folder located at /home/chip/Pictures and then EDIT>PASTE(this is just so its somewhere if you ever want it again).

Now, go back to your desktop and eject and remove your USB flash drive. Then insert it into Pocketchip. A window will pop up and It will ask you "would you like to open removable media" you don't have to. Just exit the window.

The next bit should be done in terminal it is super simple.

```Bash
cd /media/chip/ YOURFLASHDRIVENAME
```

This Changes the directory(cd) to the location of the new mainBackground.png picture.

```Bash
ls -a
```

to list all ```(ls -a)``` the contents of the directory.

Once you are in the directory containing the image.

```Bash
sudo cp mainBackground.png /usr/share/pocket-home
```

This Tells Super User(sudo) to copy(cp) mainBackground.png to /usr/share/pocket-home thus replacing the original image.

All that is left is to reboot your Pocketchip and.......... PRESTOCHANGO... you have your very own background!

[Changing the Boot Screen](https://bbs.nextthing.co/t/personalization-of-gui/5167/31)

So this one is similar to the first post on this topic about changing the background.

You are pretty much going to follow the same instructions finding and resizing the image to 480x272, except this time save the image as boot-splash.png, and use it to replace the original ```boot-splash.png``` in the directory ```/usr/share/pocketchip``` then reboot the system, or you can type ```sudo systemctl restart lightdm``` as @itxaka mentions, to reload the windows manager.

When you do changes, you dont actually need to restart the whole thing. If you have terminal access via ssh or local you can simply do

```Bash
sudo systemctl restart lightdm
```

[Quick Way to Restart PocketCHIP](https://bbs.nextthing.co/t/personalization-of-gui/5167/7)

When you do changes, you dont actually need to restart the whole thing. If you have terminal access via ssh or local you can simply do

```Bash
sudo systemctl restart lightdm
```

and it will restart the gui. Pretty useful for fast testing 

## Fixes

[Disable blinking led (heartbeat)](https://bbs.nextthing.co/t/blinking-status-led/11563/9)

The blinking is the kernel's "heartbeat", documented [here](https://www.kernel.org/doc/Documentation/devicetree/bindings/leds/common.txt4)

you can disable it like so:

```Bash
echo none | sudo tee /sys/class/leds/chip\:white\:status/trigger > /dev/null
```

or set any other "trigger", for example a HD-style access LED for the nand:

```Bash
echo nand-disk | sudo tee /sys/class/leds/chip\:white\:status/trigger > /dev/null
```

to view the full list of available triggers,

```Bash
cat /sys/class/leds/chip\:white\:status/trigger
```

## Software

[Pocketchip Doom](http://blog.nextthing.co/customize-the-hell-out-of-your-pocketc-h-i-p-install-doom-give-it-an-icon-on-the-home-screen/)

[PocketCHIP Cell Phone](http://blog.nextthing.co/learn-how-the-community-created-a-pocketc-h-i-p-cell-phone/)

[PocketCHIP RetroArch](http://blog.nextthing.co/get-started-with-retro-arch-and-game-boy-color-emulation-on-pocketc-h-i-p/)

[SoftEther VPN Project - C.H.I.P.](https://bbs.nextthing.co/t/a-better-vpn-solution-than-openvpn/5324/1)

[Headless Setup for WiFi and VNC](https://bbs.nextthing.co/t/headless-no-screen-setup-for-wifi-and-vnc/1992)

[OpenVPN on C.H.I.P.](https://bbs.nextthing.co/t/share-your-tweaks/7261)

[PSX on your CHIP](http://blog.nextthing.co/community-project-emulate-the-playstation-on-your-pocketc-h-i-p/)

[Personalize Your PocketC.H.I.P.](http://blog.nextthing.co/personalize-your-pocketc-h-i-p-tutorials-for-changing-the-background-icons-adding-a-web-browser/)

## Projects

[The $10 Echo](http://sammachin.com/the-10-echo/)

Turn a $9 C.H.I.P. and a USB Soundcard + Microphone into a D.I.Y. Amazon Echo!

[Teddy Ruxpin - C.H.I.P. enabled](https://chip.hackster.io/chip/c-h-i-p-py-ruxpin-5f02f1?ref=platform&ref_id=5276_trending___&offset=3)

[Connecting a Weather Station with WeeWx](https://bbs.nextthing.co/t/connecting-a-weather-station-with-weewx/2472)

