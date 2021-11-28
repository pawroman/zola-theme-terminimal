+++
title = "Mining Bitcoin with Pi - Part I"
date = 2015-08-15

[taxonomies]
tags = ["RaspberryPi", "Bitcoin"]
+++

I first heard about Bitcoin in early 2013 and decided the best way to learn about it would be to start mining. If you don’t know anything about Bitcoin, check out the video below and [bitcoin.org](https://bitcoin.org/en/) for more. 

{{ youtube(id="Gc2en3nHxA4", class="youtube")}}

I ordered the [Butterfly Labs](https://en.bitcoinwiki.org/wiki/Butterfly_Labs) 5 GH/s Miner in July of 2013 and actually received it in December 2013, ASIC mining was catching on like wildfire and they had a decent backlog of orders to fulfill. The most similar product they offer currently is a 10 GH/s miner. The miner connects as a peripheral via USB, so I started mining with it connected to my Windows 7 lap top using the EasyMiner Software. This reliance on my lap top to “drive” the miner wasn’t optimal, so I found a Linux based alternative that runs on Raspberry Pi called [MinePeon](https://minepeon.com/). Now I had a reliable hardware setup that required little maintenance and more importantly my lap top was free to roam. 

{{ image(src="https://raw.githubusercontent.com/kylejcarlton/zola-theme-terminimal/master/img/ButterflyLabsMinerAndPi.png", position="left") }}

Hardware in place, I decided to join a mining pool since my hash rate would be contributing such a small percentage of the entire Bitcoin network’s computing power. I joined BTC Guild, which has since shut down due to security and regulatory concerns. [P2Pool](http://p2pool.org/), [Eligius](http://eligius.st/~gateway/) and [BitMinter](https://bitminter.com/) are some mining pools still in existence. [This CoinDesk article](https://www.coindesk.com/information/get-started-mining-pools/) provides more information about mining pools. At this point I just sat back and let the miner burn electricity. Was I making a profit? Only time would tell. Next update I’ll summarize the profitability of mining with this hardware from December 2013 - July 2015.