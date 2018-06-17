# STRATUX HUD

## Introduction

This project aims to bring an affordable heads up display system into ANY cockpit.

The focus is to improve traffic awareness and to reduce the amount of time pilots reference tablets and EFBs.

There are two versions that can be built:

### Recommended

Using the "HUDLY Classic" projector and a Raspberry Pi 3.

![HUDLY Version](media/hudly_on_ground.jpg)

### Alternative, Less Expensive Version

A self contained system that uses a 3D printed case and teleprompter glass. This version can be built for the cost of a Raspberry Pi and the 3D print.

*NOTE:* This version does have visibility issues in daylight conditions. The HUDLY Version is fully daylight visible.

![Teleprompter Glass Version In Flight](media/in_flight.jpg)

## Parts List

### All Builds

*NOTE:* This _does not_ include a power source. You will need to supply ship power from a 5V USB port or from a battery.

* [Raspberry Pi 3](https://www.amazon.com/Raspberry-Pi-RASPBERRYPI3-MODB-1GB-Model-Motherboard/dp/B01CD5VC92/ref=sr_1_3?s=electronics&ie=UTF8&qid=1529215701&sr=1-3&keywords=raspberry+pi+3)
* [Case For Raspberry Pi](https://www.amazon.com/iPhoenix-Raspberry-White-Compatible-Model/dp/B06XQSXZ97/ref=sr_1_3?s=electronics&dd=iYEspjjyeRXfqDW9BHwJFw%2C%2C&ddc_refnmnt=pfod&ie=UTF8&qid=1529215794&sr=1-3&keywords=white+raspberry+pi+3+case&refinements=p_97%3A11292772011)
* [Micro USB Cable](https://www.amazon.com/AmazonBasics-Male-Micro-Cable-Black/dp/B0711PVX6Z/ref=sr_1_6?s=electronics&ie=UTF8&qid=1529215888&sr=1-6&keywords=micro+usb+cable)
* [Micro SD Card](https://www.amazon.com/SanDisk-Ultra-Micro-Adapter-SDSQUNC-016G-GN6MA/dp/B010Q57SEE/ref=sr_1_10?s=pc&ie=UTF8&qid=1529215944&sr=1-10&keywords=micro+sd+card)
* [Rottay Mechanical Keypad](https://www.amazon.com/Number-Rottay-Mechanical-Numeric-backlit/dp/B076FTSY6J/ref=sr_1_3?ie=UTF8&qid=1529215627&sr=8-3&keywords=mechanical+keypad)

### Recommended HUDLY Build

* [HUDLY Classic](https://gethudly.com/classic)
* [12" HDMI Cable](https://www.amazon.com/StarTech-com-0-3m-Short-Speed-Cable/dp/B00K3HF276/ref=sr_1_11?s=electronics&ie=UTF8&qid=1529216822&sr=1-11&keywords=short%2Bhdmi%2Bcable&th=1)

### 3D Print Build

* [Teleprompter Glass Sample of both thickness of the 60/40 glass](<https://telepromptermirror.com/sample/>)
* [SunFounder 5" TFT LCD](https://www.amazon.com/SunFounder-Monitor-Display-800X480-Raspberry/dp/B01HXSFIH6)

## Install instructions

### First Boot

1. Flash the latest [Raspbian](https://www.raspberrypi.org/downloads/raspbian/) to an SD card
2. Plug in a keyboard and a monitor
3. Plug in the power to the Pi.
4. Press ctrl+alt+f1 to quit from the GUI to the desktop
5. `sudo raspi-config`
6. boot options -> desktop / cli -> "Console auto-login"
7. "Advanced options" -> "Expand Filesystem"
8. "OK"
9. "Finish"
10. "Yes"
11. Wait for the reboot
12. `sudo raspi-config`
13. "Network options" -> "WiFi"
14. Choose your country. Pressing "u" will take you to USA.
15. Enter your network name and password.
16. "Interfacing Options" -> "Enable SSH"
17. "Localization" -> "Change Keyboard Layout" -> "Generic 104"
18. "Other" -> "English US" -> "Default" -> "No compose" -> "Yes"
19. "Finish"

### Install Software

1. Enter `ping google.com`. Press ctrl+c after a while. This will confirm that you have internet access. If you do not, then use rasp-config to re-enter your wi-fi
2. `pip install ws4py`
3. `pip install pygame`
4. `pip install requests`
5. `cd ~`
6. `git clone https://github.com/JohnMarzulli/StratuxHud.git`
7. `sudo raspi-config`
8. Choose "WiFi" again, and enter `stratux` as the SSID. No password
9. `sudo vim /etc/wpa_supplicant/wpa_supplicant.conf`
10. Delete the section that contains your WiFi network, leaving the section that contains the Stratux network.
11. More info on configuring Linux WiFi: <https://www.raspberrypi.org/forums/viewtopic.php?t=160620>
12. Save and quit.
13. Type "crontab -e"
14. Select "Nano" (Option 1)
15. Enter the following text at the _bottom_ of the file:

  ```code
  @reboot sudo python /home/pi/StratuxHud/stratux_hud.py &
  ```

1. Save and quit.

### HUDLY Based Setup

1. Install the HUDLY projector per the HUDLY directions. It is handy to have the projector turned on to help locate the glass.
2. Plug in the HDMI cable between the HUDLY input box and the Raspberry Pi.


### Teleprompter Glass Based Setup

1. Print the case.
2. Attach the LCD screen to the "GPIO Board" of the Raspberry Pi
3. Download the LCD drivers. <https://s3.amazonaws.com/sunfounder/Raspberry/images/LCD-show.tar.gz>
4. Install the LCD driver per SunFounder's instructions. <http://wiki.sunfounder.cc/index.php?title=5_Inch_LCD_Touch_Screen_Monitor_for_Raspberry_Pi>
5. Edit the StratuxHud config.json file so "flip_vertical" is True.

## Appendix



Teleprompter sample: <https://telepromptermirror.com/sample/>
