+++
title = "Storage Wars"
date = 2022-03-24
draft = true 

[taxonomies]
tags = ["Synology", "NAS", "AWS", "S3GlacierDeepArchive", "DataBackup", "DisasterRecovery"]
+++

An overwhelming choice of cloud based storage these days, and all the marketing around them can make it seem like an overly complicated endeavor to keep data safe.
I decided to take some control back from the cloud and host as much as possible on my home network. I went with a [Synology DS220+ NAS](https://www.synology.com/en-us/products/DS220+), a [Seagate 5TB External Drive](https://www.amazon.com/gp/product/B07VS8QCXC/) and [Amazon Web Services (AWS) S3 Glacier Deep Archive](https://aws.amazon.com/s3/storage-classes/?nc=sn&loc=3#____) for a low-cost off-site backup location. I also added an [APC Back-UPS 600VA](https://www.apc.com/us/en/product/BE600M1/apc-backups-600va-120v-1-usb-charging-port-7-nema-outlets-2-surge/) and used a [Raspberry Pi 2 Model B Rev 1.1](https://learn.adafruit.com/introducing-the-raspberry-pi-2-model-b) to connect and orchestrate everything.

{{ image(src="/img/NASDeepArchive.drawio.png", position="left") }}

<!-- more -->
