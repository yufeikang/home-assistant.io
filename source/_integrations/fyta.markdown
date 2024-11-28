---
title: FYTA
description: Instructions on how to integrate FYTA sensors within Home Assistant.
ha_category:
  - Sensor
ha_release: 2024.4
ha_iot_class: Cloud Polling
ha_config_flow: true
ha_codeowners:
  - '@dontinelli'
ha_domain: fyta
ha_platforms:
  - diagnostics
  - sensor
ha_integration_type: hub
ha_quality_scale: platinum
---

The **FYTA** {% term integration %} uses the open API of [FYTA](https://www.fyta.de) to obtain the data from your plant sensors and integrate these into Home Assistant.

## Supported devices

The integration should work with any [FYTA Beam](https://fyta.de/collections/all/products/single-beam).

## Prerequisites

For the integration to work you need a [FYTA Beam](https://fyta.de/collections/all/products/single-beam) and a FYTA account.

{% include integrations/config_flow.md %}

To setup the integration you need the following information:

{% configuration_basic %}
Email:
    description: "The email address used to access the FYTA account."
Password:
    description: "The password used to access the FYTA account."
{% endconfiguration_basic %}

## Configuration options

The integration has no additional configuration options.

## Supported functionality
### Sensors

The following sensors are currently available per plant:

| name                  | Unit   | Description   |
|-----------------------|--------|:-------------------------------------------|
| scientific_name       |        | Scientific name of the plant               |
| plant_status          |        | FYTA-Status (number 1 to 5)                |
| temperature_status    |        | FYTA-Status (number 1 to 5)                |
| light_status          |        | FYTA-Status (number 1 to 5)                |
| moisture_status       |        | FYTA-Status (number 1 to 5)                |
| salinity_status       |        | FYTA-Status (number 1 to 5)                |
| temperature           | °C     | Temperature measured by sensor             |
| light                 | μmol/h | Light measured by sensor (hourly photosynthetically active radiation PAR)|
| moisture              | %      | Moisture measured by sensor                |
| salinity              | mS/cm  | Salinity measured by sensor (measured as conductivity)|
| battery_level         | %      | Battery level of the sensor                |

## Data updates

The integration fetches data from the device every 4 minutes.

## Actions

The integration provides no additional actions.

## Known limitations

The integration provides the data exposed by means of the plant API. The light measurement as current daily light integral (DLI) is not yet available (currently only the PAR value is provided).

Please note that in order to be able to access your plant data over the API, you need a [FYTA hub](https://fyta.de/collections/all/products/single-hub) that uploads the data from the Beam sensor to the FYTA server. Alternatively, the mobile app can serve as a gateway to upload the data from the Beam to the server. No direct connection to the FYTA Beam is supported (as the Beam only provides raw data, that needs to be processed on the FYTA server).

## Remove integration

For this integration the general process to remove integrations applies:

{% include integrations/remove_device_service.md %}
