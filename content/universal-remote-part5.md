+++
title = "Universal Remote - Part V"
date = 2016-02-13

[taxonomies]
tags = ["RaspberryPi", "UniversalRemote"]
+++

In the last post I tested the IR receiver; next step verify the IR LEDs emit light. If you are lucky enough to have a remote in the database maintained @ [lirc.sourceforge.net/remotes/](http://lirc.sourceforge.net/remotes/), you may not even need to record. None of these worked for my remotes, so I created custom config files for each remote. However, these are great for testing functionality. I found it easier to connect to the Raspberry Pi via FTP with [FileZilla](https://filezilla-project.org/) to move config files around than via SSH with [PuTTy](http://www.putty.org/). This did require adjusting permissions using [chmod](https://en.wikipedia.org/wiki/Chmod) on /etc/lirc/lircd.conf via SSH, to allow the Write operation.

- Back up the original _/etc/lirc/lircd.conf_ and then replace it with a working config from the [LIRC Database](http://lirc.sourceforge.net/remotes/).
- Restart LIRC to pick up these changes:

```bash
sudo /etc/init.d/lirc stop
sudo /etc/init.d/lirc start
```

- Use [irsend](https://www.lirc.org/html/irsend.html) to initiate an IR signal:

```bash
irsend SEND_ONCE samsung KEY_POWER
```

The easiest way to verify the IR LEDs are working is to point them at a camera that detects IR and check if the LEDs emit light when initiating the SEND_ONCE command. Some cameras may have a filter to remove light in this spectrum. Older devices are less likely to have these filters; IR was visible on the built in webcam of my HP Envy laptop.

Now that the hardware and LIRC are working, the next step is control from a website. [Lirc_web](https://github.com/alexbain/lirc_web) relies on [Node.js](https://nodejs.org). For most of the following steps I referenced [alexba.in/blog/2013/02/23/controlling-lirc-from-the-web](http://alexba.in/blog/2013/02/23/controlling-lirc-from-the-web/).

- Install and start lirc_web:

```bash
wget https://github.com/alexbain/lirc_web/archive/master.zip
unzip master.zip
mv lirc_web-master lirc_web
rm master.zip
cd lirc_web
npm install
node app.js
```

- Create an initialization script in _/etc/init.d_ and register it using _update-rc.d_, this way lirc_web starts automatically when the Raspberry Pi boots. For more details see [stuffaboutcode.com/2012/06/raspberry-pi-run-program-at-start-up and wiki.debian.org/LSBInitScripts](http://www.stuffaboutcode.com/2012/06/raspberry-pi-run-program-at-start-up.html).

```bash
sudo nano /etc/init.d/URemote
```
```bash
#! /bin/sh    
# /etc/init.d/lirc_web     
### BEGIN INIT INFO     
# Provides:          lirc_web    
# Required-Start:    $remote_fs $syslog    
# Required-Stop:     $remote_fs $syslog    
# Default-Start:     2 3 4 5    
# Default-Stop:      0 1 6    
# Short-Description: Simple script to start a program at boot    
# Description:       Script to start / stop a program a boot / shutdown.    
### END INIT INFO    
# If you want a command to always run, put it here    
# Carry out specific functions when asked to by the system    
case "$1" in    
  start)    
    echo "Starting lirc_web"    
    # run application you want to start    
    node /home/pi/lirc_web/app.js    
    ;;    
  stop)    
    echo “Stopping lirc_web”    
    # kill application you want to stop    
    killall /home/pi/lirc_web/app.js    
    ;;    
  *)    
    echo “Usage: node /home/pi/lirc_web/app.js {start|stop}”    
    exit 1    
    ;;    
esac    
exit 0  
```
- Make the script executable:
```bash
sudo chmod 755 /etc/init.d/URemote
```
- Test starting and stopping lirc_web with the script:
```bash
sudo /etc/init.d/URemote start
sudo /etc/init.d/URemote stop
```
- Register the script to be run at start-up:
```bash
sudo update-rc.d URemote defaults
```
If your remotes aren’t in the [available index](http://lirc.sourceforge.net/remotes/) or those config files don’t work, [irrecord](http://www.lirc.org/html/irrecord.html) can be used.
- Stop lirc to free up _/dev/lirc0_:
```bash
sudo /etc/init.d/lirc stop
```
- Create a new remote control configuration file using _/dev/lirc0_ and save the output to _~/lircd.conf_. Once a file is generated for each remote it can be compiled into a single lircd.conf, this is much easier with FTP access. A list of namespace values for buttons is available @ [ocinside.de/modding_en/linux_ir_irrecord_list](http://www.ocinside.de/modding_en/linux_ir_irrecord_list/).
```bash
irrecord -d /dev/lirc0 ~/lircd.conf
```
- After all the remotes are recorded and compiled, the lircd.conf file can be placed @ _/etc/lirc/_ and then restart LIRC to pick up the new configuration:
```bash
sudo /etc/init.d/lirc stop
sudo /etc/init.d/lirc start
```
To finish of the hardware build I made a case out of Lego bricks, so it stays oriented vertically and has some protection. 
{{ image(src="https://raw.githubusercontent.com/kylejcarlton/zola-theme-terminimal/master/img/UniversalRemoteLegoCase.png", position="left") }}

Now control of IR devices is possible from a website, next up controlling Bluetooth devices the same way using [GIMX](http://gimx.fr/wiki/index.php?title=Command_line).

{{ image(src="https://raw.githubusercontent.com/kylejcarlton/zola-theme-terminimal/master/img/UniversalRemoteWebsite.png", position="left") }}

