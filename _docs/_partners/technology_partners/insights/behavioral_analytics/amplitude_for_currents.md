---
nav_title: Amplitude for Currents
page_order: 0
alias: /partners/amplitude_for_currents/
---

# About Amplitude & Currents

[Amplitude](https://amplitude.com/) is a product analytics and business intelligence platform. You can export the data events from your Braze integration to Amplitude in order to perform deep analysis of your product and marketing data.

To get started, find the following information from your Amplitude dashboard:

-   Amplitude API Key

Add this information to the Amplitude integration page on the dashboard, and press save.

![Amplitude]({% image_buster /assets/img_archive/currents-amplitude-edit.png %})

Amplitude's documentation is available [here](https://amplitude.zendesk.com/hc/en-us/articles/115000217351-Appboy-Amplitude-Integration#how-to-set-up-and-use-the-integration).

## Data Import

Using Braze and Amplitude's deep partnership, you can configure your integration to import Amplitude cohorts directly into Braze for retargeting, creating a full loop of data from one system to another. This allows you to perform deep analysis using Amplitude and seamlessly execute on your strategies using Braze.

You can manage the Amplitude Data Import process from the Technology Partners page. Note that any integration that you setup will count towards your account's data point volume.

![Amplitude cohort import]({% image_buster /assets/img_archive/currents-amplitude-import.png %})


## Integration Details

A list of the events that can be exported from Braze to Amplitude is below. All events sent to Amplitude will include the user's `external_user_id` as the Amplitude User ID. At this time, Braze does not send event data for users who do not have their `external_user_id` set. Braze-specific event properties will be sent under the `event_properties` key in the data sent to Amplitude. The properties for each event type are listed below.

You can export two types of events events to Amplitude: "Message Engagement Events" consisting of the Braze events that are directly related to message sending, and "Customer Behavior Events" including other App or Website activity such as Sessions, Custom Events, and Purchases tracked through the platform. All regular events are prefixed with `[Appboy]`, and all Custom Events are prefixed with `[Appboy] [Custom Event]`. Custom Event properties and Purchase Event properties are prefixed with `[Custom event property]` and `[Purchase property]`, respectively.

Please contact your Account Manager or [open a support ticket][support] if you need access to additional event entitlements.

### Scheduled Cohort Syncs

Braze customers using Amplitude can schedule the timed cohort syncs between Amplitude and Braze. The can be set up as hourly or daily syncs of data to be sent into Braze.

{% alert important %}
Scheduled syncs will only send deltas of the updated data set.
{% endalert %}


## Rate Limits

Currents connects to Amplitude's HTTP API, which has a [Rate Limit](https://amplitude.zendesk.com/hc/en-us/articles/204771828-HTTP-API#upload-limit) of 60 events/second per device. Above that threshold, Amplitude will throttle events that are logged through Currents. If a device in your integration is sending above this rate limit, you may experience a delay in when events from all devices will appear in Amplitude.

Devices should not report more than 60 events/second under normal circumstances, and this event pattern should only occur due to a misconfigured integration. To avoid this type of delay, ensure that your SDK integration is reporting events at a normal rate as specified in our SDK integration instructions.

## Customer Behavior Events

### Custom Events

```json
// <Custom Event Name>
{
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
```

### Purchase Events

```json
// Purchase
{
  "product_id": (string) id of product purchased (sent in the “productId” field of Amplitude HTTP API),
  "price": (float) price of product (sent in the “price” field of Amplitude HTTP API),
  "currency": (string) three letter alpha ISO 4217 currency code,
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
```

### Session Events

```json
// First Session
{
  "session_id": (string) id of the session,
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
// Session Start
{
  "session_id": (string) id of the session,
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
// Session End
{
  "session_id": (string) id of the session,
  "duration": (float) seconds session lasted,
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
```

### Location Events

```json
// Location
{
  "longitude": (float) longitude of recorded location,
  "latitude": (float) latitude of recorded location,
  "altitude": (float) altitude of recorded location,
  "ll_accuracy": (float) a percentage representing the OS determined accuracy of the recorded location,
  "alt_accuracy": (float) altitude accuracy of recorded location,
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
```

### Install Attribution Events

```json
// Install Attribution
{
  "source": (string) the source of the attribution
}
```

## Message Engagement Events

### Push Notification Events

```json
// Push Notification Send
{
  "campaign_id": (string) id of the campaign if from a campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation if from a campaign,
  "canvas_id": (string) id of the Canvas if from a Canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the canvas variation the user is in if from a Canvas,
  "canvas_step_id": (string) id of the step for this message if from a Canvas,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions),
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.)
}
// Push Notification Open
{
  "campaign_id": (string) id of the campaign if from a campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation if from a campaign,
  "canvas_id": (string) id of the Canvas if from a Canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the Canvas variation the user is in if from a Canvas,
  "canvas_step_id": (string) id of the step for this message if from a Canvas,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions),
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
// Push Notification iOS Foreground Open
{
  "campaign_id": (string) id of the campaign if from a campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation if from a campaign,
  "canvas_id": (string) id of the Canvas if from a Canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the Canvas variation the user is in if from a Canvas,
  "canvas_step_id": (string) id of the step for this message if from a Canvas,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions),
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.)
}
// Push Notification Bounce
{
  "campaign_id": (string) id of the campaign if from a campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation if from a campaign,
  "canvas_id": (string) id of the Canvas if from a Canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the Canvas variation the user is in if from a Canvas,
  "canvas_step_id": (string) id of the step for this message if from a Canvas,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions),
  "app_id": (string) id for the app on which the bounce occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.)
}
```

### Email Events

```json
// Email Send
// Email Delivery
// Email Open
// Email Click
// Email Bounce
// Email Soft Bounce
// Email Mark As Spam
// Email Unsubscribe
{
  "campaign_id": (string) id of the campaign if from a campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation if from a campaign,
  "canvas_id": (string) id of the Canvas if from a canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the canvas variation the user is in if from a Canvas,
  "canvas_step_id": (string) id of the step for this message if from a Canvas,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions),
  "dispatch_id": (string) id of the message dispatch (unique id for each 'transmission' sent from the Braze platform). Users who are sent a schedule message get the same dispatch_id. Action-based or API triggered messages get a unique dispatch_id per user.,
  "email_address": (string) email address for this event,
  "url": (string) the URL that was clicked (Email Click events only)
}
```

### Subscription Events

```json
// Subscription Group State Change
{
  "campaign_id": (string) id of the campaign if from a campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation if from a campaign,
  "canvas_id": (string) id of the Canvas if from a canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the canvas variation the user is in if from a Canvas,
  "canvas_step_id": (string) id of the step for this message if from a Canvas,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions),
  "email_address": (string) email address for this event,
  "subscription_group_id": (string) id of the subscription group,
  "subscription_status": (string) status of the subscription after the change: 'Subscribed' or 'Unsubscribed'
}
```

### In-App Message Events

```json
// In-App Message Impression
{
  "campaign_id": (string) id of the campaign if from a campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation if from a campaign,
  "canvas_id": (string) id of the Canvas if from a Canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the Canvas variation the user is in if from a Canvas,
  "canvas_step_id": (string) id of the step for this message if from a Canvas,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions),
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
// In-App Message Click
{
  "button_id": (string) index of the button clicked, if it was a button that was clicked,
  "campaign_id": (string) id of the campaign if from a campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation if from a campaign,
  "canvas_id": (string) id of the Canvas if from a Canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the Canvas variation the user is in if from a Canvas,
  "canvas_step_id": (string) id of the step for this message if from a Canvas,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions),
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
```

### Webhook Events

```json
// Webhook Send
{
  "campaign_id": (string) id of the campaign if from a campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation if from a campaign,
  "canvas_id": (string) id of the Canvas if from a Canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the Canvas variation the user is in if from a Canvas,
  "canvas_step_id": (string) id of the step for this message if from a Canvas,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions)
}
```

### Content Card Events

```json
// Content Card Send
{
  "card_id": (string) id of the content card that was sent,
  "campaign_id": (string) id of the campaign if from a campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation if from a campaign,
  "canvas_id": (string) id of the Canvas if from a Canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the Canvas variation the user is in if from a Canvas,
  "canvas_step_id": (string) id of the step for this message if from a Canvas,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions)
}
```

```json
// Content Card Impression
// Content Card Click
// Content Card Dismiss
{
  "card_id": (string) id of the content card that was viewed/clicked/dismissed,
  "app_id": (string) id for the app on which the user action occurred,
  "campaign_id": (string) id of the campaign if from a campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation if from a campaign,
  "canvas_id": (string) id of the Canvas if from a Canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the Canvas variation the user is in if from a Canvas,
  "canvas_step_id": (string) id of the step for this message if from a Canvas,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions),
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
```

### News Feed Events

```json
// News Feed Card Impression
{
  "card_id": (string) id of the card that was viewed,
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
// News Feed Card Click
{
  "card_id": (string) id of the card that was clicked,
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
// News Feed Impression
{
  "app_id": (string) id for the app on which the user action occurred,
  "platform": (string) platform of the device (iOS, Android, web, etc.),
  "os_version": (string) os version of device used for the action,
  "device_model": (string) hardware model of the device
}
```

### Uninstall Events

```json
// Uninstall
{
  "app_id": (string) id for the app on which the user action occurred
}
```

### Conversion Events

```json
// Campaign Conversion Event
{
  "campaign_id": (string) id of the campaign,
  "campaign_name": (string) name of the campaign,
  "conversion_behavior_index": (int) index of the conversion behavior,
  "conversion_behavior": (string) JSON-encoded string describing the conversion behavior,
  "message_variation_id": (string) id of the message variation,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions)
}
// Canvas Conversion Event
{
  "canvas_id": (string) id of the Canvas,
  "canvas_name": (string) name of the Canvas,
  "conversion_behavior_index": (int) index of the conversion behavior,
  "conversion_behavior": (string) JSON-encoded string describing the conversion behavior,
  "canvas_variation_id": (string) id of the Canvas variation the user is in,
  "canvas_step_id": (string) id of the last step the user was sent before the conversion
}
```

### Canvas Entry Events

```json
// Canvas Entry
{
  "canvas_id": (string) id of the Canvas,
  "canvas_name": (string) name of the Canvas,
  "canvas_variation_id": (string) id of the Canvas variation the user is in,
  "in_control_group": (boolean) whether the user was enrolled in the control group for a Canvas
}
```

### Campaign Enrollment Events

```json
// Campaign Control Group Enrollment
{
  "campaign_id": (string) id of the campaign,
  "campaign_name": (string) name of the campaign,
  "message_variation_id": (string) id of the message variation,
  "send_id": (string) id of the message if specified for the campaign (See Send Identifier under REST API Parameter Definitions)
}
```
[support]: {{ site.baseurl }}/support_contact/
