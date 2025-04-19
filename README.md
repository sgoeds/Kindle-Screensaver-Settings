# Kindle Screensaver Settings
This is a simple [KUAL](https://www.mobileread.com/forums/showthread.php?t=203326) application to turn off special offers on a [jailbroken](https://github.com/KindleModding/WinterBreak) Kindle.

USE THIS AT YOUR OWN RISK!!!! I AM NOT REPOSONSIBLE FOR BROKEN KINDLES!!!!

I have tested this on my Kindle 10th gen and no other device. So good luck.

## Installation
1. Download the screensaver_toggle folder and paste it into you /extensions folder.
2. That's it

## Usage
This "application" lives entirely in the menus of KUAL where you can disable and enable special offer screensavers and the USB connection screen.
You choices will be reset when you reboot, so you will either have to setup a boot script or run the program every time you boot.

## KUAL Menu Options
#### Disable Ads
This disables the ad "special offers" screensavers and replaces them with the default screensavers (remeber this gets reset on boot).

#### Disable all screensavers
This disables ad "special offers" screensaver *and* the normal screensaver (if already enabled). 
When you press the lock button it will just turn the frontlight off and lock the screen on whatever is on it.

#### Revert back to ads
Disables the normal screensaver (if enabled) and enables the ad "special offers" screensaver.
I have no idea what would happen on a device that does not have special offers enabled.

#### USB Screensaver off (UNSAFE)
This will disable the full screen image that is shown when you plug your device into a computer.
I really really really recommend you don't do this, it is cool to be able to control your Kindle while transfering files, but there is a reason your normally can't do that. 
It will very quickly softlock your Kindle.

#### USB Screensaver on
Reverts the previously mentioned option.

## How It Works
This utilizes the lipc framework (which I barely undestand). 
Specifically the `com.lab126.blanket` `load` and `unload` options 
(Blanket is the program that shows full screen images on Kindles btw).

You can view the current blanket components that are in use by running the following command (note that KOReader sometimes [temporarily alters values](https://github.com/koreader/koreader/blob/8556d77f557b787292f9a96f7667e729e5a4d2b2/frontend/device/kindle/device.lua#L332) while it is running):
```bash
lipc-get-prop com.lab126.blanket load
```
Adding a component is done with the following command:
```bash
lipc-set-prop com.lab126.blanket load {NAME}
```
And removing one:
```bash
lipc-set-prop com.lab126.blanket unload {NAME}
```

Listing the values, by default for me, produces:
```
langpicker blankwindow ad_screensaver usb
```
Swapping from ad screens to normal is as simples as:
```bash
lipc-set-prop com.lab126.blanket unload ad_screensaver
lipc-set-prop com.lab126.blanket load screensaver
```
|Value in com.lab126.blanket|Meaning|
|-|-|
|langpicker|IDK|
|blankwindow|IDK, but your system will crash if you remove it|
|ad_screensaver|Ad screensaver (duh)|
|screensaver| The normal screensaver (without ads)|
|usb|Shows the full screen image when plugged into a computer|

## Contributions
If you have some cool idea of more things this could do, make a merge request!
Like for example, if you want to have a way to install this into a boot script, that would be splendid (I am lazy).

If you have success with this, please let me know so I can list your device as being supported, make an issue or something I don't really care how, but please let me know!

If you have knowledge about one of the many things in this README that I do not, please make an issue or merge request.
