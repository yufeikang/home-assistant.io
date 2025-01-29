---
title: "B-Route Smart Meter"
description: "Integration with Japanese smart meters via B-route [Bルートサービス] interface"
ha_category: Sensor
ha_release: "0.1.0"
ha_iot_class: "Local Polling"
ha_config_flow: true
ha_domain: b_route_meter
ha_quality_scale: bronze
ha_codeowners:
  - '@yufeikang'
---

The B-Route (Bルートサービス) Smart Meter integration allows you to read power consumption data from Japanese smart meters through the B-route interface.

## Prerequisites

- Smart meter with B-route support (e.g., smart meters from TEPCO and Chubu Electric Power)
- B-route authentication ID and password (obtained from your power company)
- USB to Wi-SUN adapter (e.g., tested with [BP35A1](https://www.rohm.co.jp/products/wireless-communication/specified-low-power-radio-modules/bp35a1-product))

## Setup

This integration can be configured through the Home Assistant UI:

1. Navigate to the Integrations page in Home Assistant
2. Click the "Add Integration" button in the bottom right corner
3. Search for "B-Route Smart Meter"
4. Follow the configuration wizard

{% configuration %}
route_b_id:
  description: B-route ID obtained from your power company
  required: true
  type: string
route_b_pwd:
  description: B-route password obtained from your power company
  required: true
  type: string
serial_port:
  description: Path to the serial device
  required: false
  type: string
  default: /dev/ttyS0
{% endconfiguration %}

## Sensors

This integration creates the following sensor entities:

| Entity ID | Description | Unit |
|-----------|-------------|------|
| sensor.b_route_instantaneous_power | Instantaneous power consumption | W |
| sensor.b_route_instantaneous_current | Instantaneous current | A |
| sensor.b_route_instantaneous_voltage | Instantaneous voltage | V |
| sensor.b_route_cumulative_forward | Cumulative forward power consumption | kWh |
| sensor.b_route_cumulative_reverse | Cumulative reverse power consumption | kWh |

## Troubleshooting

If you experience connection issues:

1. Verify your B-route ID and password are correct
2. Check if the serial port path is correct
3. Confirm your smart meter supports B-route functionality
4. Check Home Assistant logs for detailed error messages

<div class='note'>

For TEPCO customers, you can apply for B-route ID and password through the [TEPCO website](https://www.tepco.co.jp/pg/consignment/liberalization/smartmeter-broute.html).

</div>

## Data Updates

The integration polls the smart meter every 10 seconds to update the sensor values.

## Technical Details

The integration uses the ECHONET Lite protocol to communicate with the smart meter via the B-route interface. It automatically handles:

- Channel scanning
- PANA authentication
- Data parsing for various power metrics (E7, E8, E9, EA, EB)

For more information about the protocol, refer to the [ECHONET Lite Specification](https://echonet.jp/spec_g/).
