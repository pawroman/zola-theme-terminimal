+++
title = "Nest Thermostat Logger"
date = 2022-12-24
draft = false

[taxonomies]
tags = ["Nest", "Google", "API", "DeviceAccess", "OAuth2", "Temperature", "Humidity", "Weather"]
+++

Since [Works with Nest (WWN)](https://developers.nest.com/) is retiring, I decided to configure [Device Access](https://developers.google.com/nest/device-access/get-started) and check out the [Smart Device Management (SDM) Application Programming Interface (API)](https://developers.google.com/nest/device-access/api). The Quick Start Guide on the Device Access page is very comprehensive, and here's what I did to get a log of temperature and humidity from my Nest thermostat and corresponding outdoor values.

{{ image(src="/img/NestandOutside.png", position="left") }}
<!-- more -->

First I paid the seemingly unavoidable one-time, non-refundable $5 USD fee and accepted both the [Google API](https://developers.google.com/terms) and [Device Access Sandbox](https://developers.google.com/nest/device-access/tos) Terms of Service.

Since access to the SDM API is through [Google Cloud Platform (GCP)](https://cloud.google.com/gcp/) I created a [project](https://developers.google.com/workspace/marketplace/create-gcp-project). Then enabled the Smart Device Management API from the [API Enablement page](https://console.developers.google.com/apis/library/smartdevicemanagement.googleapis.com) and created an [OAuth 2.0](https://oauth.net/2/) Client ID on the [Credentials page](https://console.developers.google.com/apis/credentials).

My final step in setup was to create a project in Device Access, so I have the project [Universally Unique Identifier (UUID)](https://en.wikipedia.org/wiki/Universally_unique_identifier) needed to make SDM API calls.

<!-- more -->

Authorizing an account through this link allows granting access to my Nest (replace ***project-id*** and ***oauth2-client-id*** with project values):

>[https://nestservices.google.com/partnerconnections/***project-id***/auth?redirect_uri=https://www.google.com&access_type=offline&prompt=consent&client_id=***oauth2-client-id***&response_type=code&scope=https://www.googleapis.com/auth/sdm.service](https://nestservices.google.com/partnerconnections/project-id/auth?redirect_uri=https://www.google.com&access_type=offline&prompt=consent&client_id=oauth2-client-id&response_type=code&scope=https://www.googleapis.com/auth/sdm.service)

This redirects to [google.com](https://www.google.com) and returns the authorization code in the address bar:

>[https://www.google.com?code=***authorization-code***&scope=https://www.googleapis.com/auth/sdm.service](https://www.google.com?code=authorization-code&scope=https://www.googleapis.com/auth/sdm.service
)

From here the authorization code can be used to obtain both the access and refresh tokens. This project on Github is a simple Bash script to accomplish everything once the authorization code is obtained:  [Google-SDM-API-Bash](https://github.com/kylejcarlton/Google-SDM-API-Bash).