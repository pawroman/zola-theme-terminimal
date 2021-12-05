+++
title = "WiFi Temperature Monitor - Part II"
date = 2016-10-05

[taxonomies]
tags = ["Particle", "WiFiTemp"]
+++

Since writing the first WiFi temperature monitor post, I’ve implemented retrieving temperature values on a schedule, to generate a real-time dashboard. I came across this [Gadgets Apps Hacks Post](http://www.gadgetsappshacks.com/2014/01/how-to-record-daily-portfolio-values-in.html), which utilizes [Google Apps Script’s](https://developers.google.com/apps-script/) ability to connect to [External APIs](https://developers.google.com/apps-script/guides/services/external) and record stock ticker values over time in [Google Sheets](https://www.google.com/sheets/about/). The method I used in the first part to write the temperature sensor value in a Sheet is more suited for a single import of a larger data set in JSON format. There is also a [tutorial from Particle](https://docs.particle.io/tutorials/projects/maker-kit/#tutorial-4-temperature-logger) that uses [IFTTT](https://ifttt.com/) to log the data in a Sheet. Although the tutorial from Particle might be a little easier to implement, I chose to work solely with Google Apps Script; since I wanted to pull data from other APIs. I’ll use [WeatherUnderground](https://www.wunderground.com/weather/api/d/docs) for the outside temperature and [Nest](https://developers.nest.com/documentation/cloud/get-started) for a comparison of inside temperature from another device.

<!-- more -->

{{ image(src="https://raw.githubusercontent.com/kylejcarlton/zola-theme-terminimal/master/img/Google_Apps_Script_Temp.png", position="left") }}

For communication with my Nest Thermostat, I didn’t implement the [OAuth2.0](https://oauth.net/2/) standard completely inside the Apps Script; although this would be possible using [apps-script-oauth2](https://github.com/googlesamples/apps-script-oauth2). Following the [REST Quick Guide](https://developers.nest.com/documentation/cloud/how-to-auth), I generated a [PIN for my Nest](https://developers.nest.com/documentation/cloud/authorization-overview#pin-based-authorization) and then used [Postman](https://www.getpostman.com/) to initiate the POST call for the Access Token to be used in the script.

Here are the results after a few days:

<iframe width="697" height="431" seamless frameborder="0" scrolling="no" style="display: block; margin: 0 auto" src="https://docs.google.com/spreadsheets/d/1ir8ENcChkleHsPGUWlmbGlXQQTnxPHI-o29nMX9jvO8/pubchart?oid=280457042&format=interactive"></iframe>

The [Google Sheet](https://docs.google.com/spreadsheets/d/1ir8ENcChkleHsPGUWlmbGlXQQTnxPHI-o29nMX9jvO8/edit) is here (create a copy to view Script Editor and make changes) and I also posted the code as a [Gist here](https://gist.github.com/kylejcarlton/12a85c4a5b375eaff62ee509d76a6720). API keys, device ID’s etc. are all variables to be defined at the beginning of the Script.