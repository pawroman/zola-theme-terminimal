+++
title = "Universal Remote - Part IV"
date = 2015-11-05

[taxonomies]
tags = ["RaspberryPi", "UniversalRemote"]
+++



With the hardware built the next step is getting the Raspberry Pi up and running and installing [LIRC](http://www.lirc.org/). [Alexba.in](http://alexba.in/) has a comprehensive post for both of these things: [RaspberryPi Quickstart](http://alexba.in/blog/2013/01/04/raspberrypi-quickstart/) and [Setting Up LIRC on the RaspberryPi](http://alexba.in/blog/2013/01/06/setting-up-lirc-on-the-raspberrypi/). 

I discovered and modified a few things along the way, so here’s what I did.

- Download the latest [Raspbian Image](https://www.raspberrypi.org/downloads/raspbian/) and follow their [Installation Guide](https://www.raspberrypi.org/documentation/installation/installing-images/README.md).
- Network the Pi over wired Ethernet using RJ45 connector.
- Connect to the Pi over SSH with [PuTTy](http://www.putty.org/).

Since I’d like to connect over WiFi I’ve added a [Belkin USB F7D2101](https://www.belkin.com/us/support-product?pid=01t80000002G16OAAS). For future development, I also added a [ORICO BTA-402 USB Bluetooth 4.0 Micro Adapter Dongle](https://www.amazon.com/ORICO-Bluetooth-Adapter-Windows-Consumption/dp/B01827IICO) for controlling a Play Station 3 using [GIMX](https://gimx.fr/wiki/index.php?title=Main_Page).

{{ image(src="https://raw.githubusercontent.com/kylejcarlton/zola-theme-terminimal/master/img/RemoteBuildWirelessBT.png", position="left") }}

- With the Pi temporarily connected by Ethernet cable, I [set up the wireless connection via the command line](https://www.raspberrypi.com/documentation/computers/configuration.html) over SSH.
- The following commands update the Software and Firmware then sync the Time with a source on the Internet:

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
sudo apt-get install git-core
sudo wget http://goo.gl/1BOfJ -O /usr/bin/rpi-update && sudo chmod +x /usr/bin/rpi-update
sudo rpi-update

sudo apt-get install ntpdate
sudo ntpdate -u ntp.ubuntu.com
```