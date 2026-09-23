# Health & Safety

2 automation(s) in this category.

| Automation | Description |
|---|---|
| Bedroom Sensor Recovery - Re-enable Control When Available | When bedroom sensor comes back online, dismiss the unavailability notification. |
| CGM Monitor & Alerts (with 1hr cooldown) | Monitors blood glucose levels from sensor.librelink_glucose_measurement. Triggers critical alerts for readings below 40. Plays TTS alert, sends notification, and flashes TV lights red.

NOTIFY WRAPPER 2026-09-22: every notify.mobile_app_pixel_9 call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent and icon values. Delivery behavior is unchanged; channel and importance policy now lives in the shared script. |
