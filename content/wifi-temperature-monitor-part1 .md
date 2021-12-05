+++
title = "WiFi Temperature Monitor - Part I"
date = 2016-05-22

[taxonomies]
tags = ["Particle", "WiFiTemp"]
+++

[Particle.io](https://www.particle.io/) has some relatively inexpensive and lightweight IoT boards that connect via WiFi ([Photon](https://www.particle.io/products/hardware/photon-wifi-dev-kit)) or Cellular Networks ([Electron](https://store.particle.io/collections/electron)). They are focused on providing a fully functioning cloud based IDE for development and production devices. Programming is accomplished via [Wiring](http://wiring.org.co/), the same framework as [Arduino](https://www.arduino.cc/). Since the framework is open source down to the bare metal, you can also use C/C++ or ARM assembly.

For my first project with the Photon, I created a wireless temperature monitor that displays in a [Google Sheet](https://www.google.com/sheets/about/). I used a [TMP36 Sensor](http://www.analog.com/en/products/analog-to-digital-converters/integrated-special-purpose-converters/digital-temperature-sensors/tmp36.html) and imported the results utilizing Script Editor and this [Import JSON Script](https://github.com/fastfedora/google-docs/blob/master/scripts/ImportJSON/Code.gs). The JSON output from the Photon looks like this (“deviceID” intentionally obscured):

```json
{
 "cmd": “VarReturn”,
 "name": “analogvalue”,
 "result": 964,
 "coreInfo": {
   "last_app": “”,
   "last_heard": “2016-05-22T22:00:00.209Z”,
   "connected": true,
   "last_handshake_at": “2016-05-22T21:20:20.002Z”,
   "deviceID": “UNIQUE_ID”,
   "product_id": 6
 }
}
```

Then the temperature can be calculated based on the voltage output from the TMP36 using _Temp °C = 100*(reading in V) - 50_.

{{ image(src="https://raw.githubusercontent.com/kylejcarlton/zola-theme-terminimal/master/img/TMP36_Graph.png", position="left") }}

After importing I also converted to Fahrenheit using _T(°F) = T(°C) × 1.8 + 32_. Here’s the final output in the Google Sheet using _ImportJSON(https://api.particle.io/v1/devices/UNIQUE_ID/analogvalue?access_token=UNIQUE_TOKEN)_:


{{ image(src="https://raw.githubusercontent.com/kylejcarlton/zola-theme-terminimal/master/img/TMP36_Gsheet.png", position="left") }}
