---
title: SABnzbd
description: Instructions on how to integrate SABnzbd with Home Assistant.
ha_category:
  - Downloading
  - Sensor
ha_release: 0.7
ha_config_flow: true
ha_iot_class: Local Polling
ha_codeowners:
  - '@shaiu'
  - '@jpbede'
ha_domain: sabnzbd
ha_platforms:
  - sensor
  - binary_sensor
  - button
  - number
ha_integration_type: integration
---

The SABnzbd integration will allow you to monitor and control your downloads with [SABnzbd](https://sabnzbd.org) from within Home Assistant and setup automations based on the information.

## Prerequisites

You need to grab your API key from your SABnzbd instance in order to configure this integration:

- Navigate to your SABnzbd.
- Click "Config", then click "General".
- Copy your API key under "Security".

{% include integrations/config_flow.md %}

## Sensor

This integration will create these sensors:

- `status`: The current status of SABnzbd. (Idle, Paused, etc.)
- `speed`: The current download speed.
- `queue`: The total size of the download queue.
- `left`: The remaining size of the download queue.
- `disk`: The total disk size at SABnzbd's download location.
- `disk_free`: The available disk space at SABnzbd's download location.
- `queue_count`: The number of items in the download queue.
- `total`: Total GB downloaded.
- `daily_total`: GB downloaded today. (disabled by default)
- `weekly_size`: GB downloaded this week. (disabled by default)
- `monthly_total`: GB downloaded this month. (disabled by default)

## Binary sensor

This integration will create a binary sensor to indicate if SABnzbd has recorded any warnings or errors.

## Button

This integration will create two buttons:

- Pause the download queue.
- Resume the download queue.

## Number

This integration will create a number entity to set the download queue speed limit in percentage.
