+++
title = "Universal Remote - Part V"
date = 2016-02-13

[taxonomies]
tags = ["RaspberryPi", "UniversalRemote"]
+++

{{ image(src="https://raw.githubusercontent.com/kylejcarlton/zola-theme-terminimal/master/img/UniversalRemoteWebsite.png", position="left") }}

In the last post I tested the IR receiver; next step verify the IR LEDs emit light. If you are lucky enough to have a remote in the database maintained @ [lirc.sourceforge.net/remotes/](http://lirc.sourceforge.net/remotes/), you may not even need to record. None of these worked for my remotes, so I created custom config files for each remote. However, these are great for testing functionality. I found it easier to connect to the Raspberry Pi via FTP with [FileZilla](https://filezilla-project.org/) to move config files around than via SSH with [PuTTy](http://www.putty.org/). This did require adjusting permissions using [chmod](https://en.wikipedia.org/wiki/Chmod) on /etc/lirc/lircd.conf via SSH, to allow the Write operation.

- Back up the original _/etc/lirc/lircd.conf_ and then replace it with a working config from the LIRC Database.
