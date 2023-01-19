+++
title = "Nest Thermostat Logger"
date = 2022-12-24
draft = false

[taxonomies]
tags = ["Nest", "Google", "API", "DeviceAccess", "OAuth2", "Temperature", "Humidity", "Weather"]
+++

Since [Works with Nest (WWN)](https://developers.nest.com/) is retiring, I decided to get set up on [Device Access](https://developers.google.com/nest/device-access/get-started) to check out the Smart Device Management (SDM) API. The Quick Start Guide on the Device Access page is very comprehensive, and here's what I did to get everything up and running.

First I paid the seemingly unavoidable one-time, non-refundable $5 USD fee and accepted both the [Google API](https://developers.google.com/terms) and [Device Access Sandbox](https://developers.google.com/nest/device-access/tos) Terms of Service.

Since access to the SDM API is through [Google Cloud Platform (GCP)](https://cloud.google.com/gcp/) I created a project and enabled the Smart Device Management API from the [API Enablement](https://console.developers.google.com/apis/library/smartdevicemanagement.googleapis.com) page and created an OAuth 2.0 Client ID on the [Credentials](https://console.developers.google.com/apis/credentials) page.

My final step in setup was to create a project in Device Access, so I have the Project UUID needed to make SDM API calls.

Authorizing an account through this link allows granting access to my nest:

[https://nestservices.google.com/partnerconnections/**project-id**/auth?redirect_uri=https://www.google.com&access_type=offline&prompt=consent&client_id=**oauth2-client-id**&response_type=code&scope=https://www.googleapis.com/auth/sdm.service](https://nestservices.google.com/partnerconnections/project-id/auth?redirect_uri=https://www.google.com&access_type=offline&prompt=consent&client_id=oauth2-client-id&response_type=code&scope=https://www.googleapis.com/auth/sdm.service)

This redirects to [google.com](https://www.google.com) and returns the authorization code in the address bar:

[https://www.google.com?code=**authorization-code**&scope=https://www.googleapis.com/auth/sdm.service](https://www.google.com?code=authorization-code&scope=https://www.googleapis.com/auth/sdm.service
)

This [curl](https://curl.se/) request returns the access and refresh tokens:

```bash
$ curl -L -X POST 'https://www.googleapis.com/oauth2/v4/token?client_id=oauth2-client-id&client_secret=oauth2-client-secret&code=authorization-code&grant_type=authorization_code&redirect_uri=https://www.google.com'
```
