---
title: Somfy
description: Instructions on how to set up the Somfy hub within Home Assistant.
ha_category:
  - Hub
ha_iot_class: Cloud Polling
ha_release: 0.95
ha_config_flow: true
ha_codeowners:
  - '@tetienne'
ha_domain: somfy
ha_zeroconf: true
ha_platforms:
  - climate
  - cover
  - sensor
  - switch
ha_integration_type: integration
---

<div class="note warning">

The Somfy Open API (cloud-based) has been deprecated in favor of the [Somfy TaHoma Developer Mode](https://developer.somfy.com/developer-mode) and will shut down after June 21st, 2022. The [Overkiz integration](/integrations/overkiz/) will support this new local API and can already be used to control your Somfy devices via the cloud.

</div>

The Somfy integration will allow users to integrate their Somfy devices into Home Assistant using the [official API](https://developer.somfy.com/somfy-open-api/apis).

## Installation

Somfy is leveraging the new account linking service. This means that to set up Somfy, you only need to go to the integrations page and click on add new integration.

<lite-youtube videoid="y0SECWUVR-M" videotitle="New OAuth2 account linking service" posterquality="maxresdefault"></lite-youtube>

## Installation with own developer account

It is possible to create your own developer account and configure Somfy via that.

### Setting up developer account

1. Visit [https://developer.somfy.com](https://developer.somfy.com).
2. Log in using your Somfy credentials.
3. Open the _My Apps_ menu.
4. Add a new App:

- App Name: Home Assistant
- Callback URL: `<YOUR_HOME_ASSISTANT_URL>/auth/external/callback`
- Description: Home Assistant instance
- Product: Somfy Open API

### Pre-configuration

```yaml
# Example configuration.yaml entry
somfy:
  client_id: CONSUMER_KEY
  client_secret: CONSUMER_SECRET
```

{% configuration %}
client_id:
  description: Your Somfy consumer key.
  required: true
  type: string
client_secret:
  description: Your Somfy consumer secret.
  required: true
  type: string
optimistic:
  description: Set optimistic mode.
  required: false
  default: false
  type: boolean
{% endconfiguration %}

**optimistic** mode should only be used when the integration is not able to gain information on whether a cover is open or closed (e.g., [RTS](https://www.somfysystems.com/en-us/discover-somfy/technology/radio-technology-somfy) devices). It will attempt to track the status within Home Assistant. This mode should only be used if Home Assistant is the only way you operate the blind. If you also use the physical remote control or the Somfy app, Home Assistant will become out of sync.

{% include integrations/config_flow.md %}
