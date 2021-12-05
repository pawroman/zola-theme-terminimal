+++
title = "Mining BTC with Pi - Part II"
date = 2015-10-16

[taxonomies]
tags = ["RaspberryPi", "BTC"]
+++

I mined a total of 0.24359921 Bitcoin (BTC) with the Raspberry Pi and Butterfly Labs 5 GH/s miner from December 17, 2013 - July 29, 2015. 

Here’s a breakdown of costs: 

- Hardware = $390
- Electricity = $571
- **Total = $961**

Total cost of power over that period of approximately 14,136 hours was calculated assuming $0.19 / kWh by taking the average over a one year period. The power consumption was approximated by recording usage with a [P3 Kill A Watt](http://www.p3international.com/products/p4400.html) over a ten day period and interpolating linearly.

<!-- more -->

{{ image(src="https://raw.githubusercontent.com/kylejcarlton/zola-theme-terminimal/master/img/BTCMinerPowerUsage.png", position="left") }}

Thanks to the technology behind Bitcoin, you can see the full contents of the wallet where mining profits were deposited on [BlockChain.info](https://www.blockchain.com/explorer) @ [1BsWqHJh5kwLNHZzj6Q6DGaxRZVTK9U9A6](https://blockchain.info/address/1BsWqHJh5kwLNHZzj6Q6DGaxRZVTK9U9A6) and a graph over time. 

{{ image(src="https://raw.githubusercontent.com/kylejcarlton/zola-theme-terminimal/master/img/BTCMinerProfitability.png", position="left") }}

With the exchange rate of Bitcoins to USD at the time of writing this, the Return on Investment (ROI) with a balance of 0.24359921 BTC is about negative (-) $896. Breaking even would require the exchange rate to reach $3,844 USD / BTC; historically speaking the highest was around $1,100 in late 2013. Never say never though, here’s the [current price from CoinDesk](https://www.coindesk.com/price/bitcoin/).