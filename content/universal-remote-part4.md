+++
title = "Universal Remote - Part IV"
date = 2015-11-05

[taxonomies]
tags = ["RaspberryPi", "UniversalRemote"]
+++



With the hardware built the next step is getting the Raspberry Pi up and running and installing [LIRC](http://www.lirc.org/). [Alexba.in](http://alexba.in/) has a comprehensive post for both of these things: [RaspberryPi Quickstart](http://alexba.in/blog/2013/01/04/raspberrypi-quickstart/) and [Setting Up LIRC on the RaspberryPi](http://alexba.in/blog/2013/01/06/setting-up-lirc-on-the-raspberrypi/).

I discovered and modified a few things along the way, so here’s what I did:

- Download the latest [Raspbian Image](https://www.raspberrypi.org/downloads/raspbian/) and follow their [Installation Guide](https://www.raspberrypi.org/documentation/installation/installing-images/README.md).
- Network the Pi over wired Ethernet using RJ45 connector.
- Connect to the Pi over SSH with [PuTTy](http://www.putty.org/).

Since I’d like to connect over WiFi I’ve added a [Belkin USB F7D2101](https://www.belkin.com/us/support-product?pid=01t80000002G16OAAS). For future development, I also added a [ORICO BTA-402 USB Bluetooth 4.0 Micro Adapter Dongle](https://www.amazon.com/ORICO-Bluetooth-Adapter-Windows-Consumption/dp/B01827IICO) for controlling a Play Station 3 using [GIMX](https://gimx.fr/wiki/index.php?title=Main_Page).

<!-- more -->

{{ image(src="/img/RemoteBuildWirelessBT.jpg", position="left") }}

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

- Next install [LIRC](http://www.lirc.org/)

```bash
sudo apt-get install lirc
```

- Modify **/etc/modules** and **/etc/lirc/hardware.conf** for the specific hardware being used:

_**/etc/modules**_

```bash
lirc_dev    
lirc_rpi gpio_in_pin=23 gpio_out_pin=22
```

_**/etc/lirc/hardware.conf**_

```bash
######################
# /etc/lirc/hardware.conf    
#    
# Arguments which will be used when launching lircd    
LIRCD_ARGS="--uinput"    
# Don't start lircmd even if there seems to be a good config file    
# START_LIRCMD=false    
# Don't start irexec, even if a good config file seems to exist.    
# START_IREXEC=false    
# Try to load appropriate kernel modules LOAD_MODULES=true    
# Run "lircd --driver=help" for a list of supported drivers.    
DRIVER="default"    
# usually /dev/lirc0 is the correct setting for systems using udev    
DEVICE="/dev/lirc0"    
MODULES="lirc_rpi"
# Default configuration files for your hardware if any    
LIRCD_CONF="" LIRCMD_CONF=""    
###################### 
```

- Restart LIRC to pick up these changes:

```bash
sudo /etc/init.d/lirc stop
mode2 -d /dev/lirc0
```

- Pressing buttons on an IR remote pointed at the receiver and activity similar to the following should be displayed:

```bash
space 16300    
pulse 95    
space 28794    
pulse 80    
space 19395    
pulse 83  
```

In the next post on this topic I’ll cover recording the IR signal from remotes using the [irrecord command](http://www.lirc.org/html/irrecord.html) and testing functionality from the command line. I’ll also install [Node.js](https://nodejs.org/) and the client library [lirc_node](https://github.com/alexbain/lirc_node) for controlling LIRC from a web site.
