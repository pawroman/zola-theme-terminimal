+++
title = "Universal Remote - Part II"
date = 2014-11-11

[taxonomies]
tags = ["RaspberryPi", "UniversalRemote"]
+++

I purchased the [Prototyping Pi Plate directly from adafruit](https://www.adafruit.com/product/801), and the [Raspberry Pi from Amazon](https://www.amazon.com/Raspberry-Pi-Motherboard-RASPBRRYPCBA512-MC-RP001-CLR/dp/B01CF0RTUG). The [IR Transmitters, Right Angle Mounts, Transistor, Resistor and IR Receiver from Mouser](http://www.mouser.com/). [The 22 AWG solid wire and soldering supplies from Fry’s](http://www.frys.com/).

Parts List:

---
- 1 x [Adafruit Industries ADA801](https://octopart.com/801-adafruit+industries-24605284)
- 1 x [Raspberry Pi Model B 756-8308 Motherboard](https://en.wikipedia.org/wiki/Raspberry_Pi)
- 2 x [Everlight IR333C](https://octopart.com/ir333c-everlight-17677690)
- 2 x [Avago HLMP-5029](https://octopart.com/hlmp-5029-avago-549484)
- 1 x [ON Semiconductor P2N2222AG](https://octopart.com/p2n2222ag-on+semiconductor-55396558)
- 1 x [Ohmite OD103JE](https://octopart.com/od103je-ohmite-133027)
- 1 x [Vishay Semiconductor TSOP38238 IR Receiver](https://octopart.com/tsop38238-vishay-5517697)
- 1 x 22 [AWG Solid Core Wire](http://www.frys.com/product/7716148/)
---

<!-- more -->

{{ image(src="https://raw.githubusercontent.com/kylejcarlton/zola-theme-terminimal/master/img/OpensourceRemoteParts.png", position="left") }}

Here's [the circuit](https://upverter.com/alexbain/f24516375cfae8b9/Open-Source-Universal-Remote/#/) I’ll be building: 

<iframe width='800' height='600' frameborder='0' scrolling='no' src='https://upverter.com/eda/embed/#designId=f24516375cfae8b9'></iframe>

Once complete the next step will be installing and configuring [LIRC](https://www.lirc.org/).