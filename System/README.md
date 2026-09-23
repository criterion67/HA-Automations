# System

10 automation(s) in this category.

| Automation | Description |
|---|---|
| Alert Light: Migraine Green Therapy Toggle (Aqara B1 Hold) | Hold the Front Door Aqara B1 button to activate 520nm migraine therapy green (RGB 0,255,0) at 100%. Uses input_boolean.migraine_therapy_mode_active as a clean flag. Snapshots previous light state into input_text.migraine_light_restore_state before activating, and restores it on deactivation. |
| Charge monitor for curtain motors | Announces via TTS when curtain motors are fully charged and reminds every 5 minutes while still plugged in |
| Energy Monitoring Plug Failsafe | Keeps all energy monitoring plugs ON. If any are turned off, they are restored and a notification is sent.

NOTIFY WRAPPER 2026-09-22: every direct notify.mobile_app_* call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent, color, image, url and icon values, and target set to watch or bill where the call went to those devices. Delivery behavior is unchanged; channel and importance policy now lives in the shared scripts. |
| GitHub Backup - Daily | Runs both GitHub backup scripts at 03:00 and alerts on failure. github_backup.sh pushes the whole /config repo; automations_backup.sh pushes automations.yaml plus the per category split files to HA-Automations. Both exit codes are captured with response_variable so a failure raises a phone alert instead of only a log line. This matters because automations_backup.sh failed silently for roughly five months and 295 commits were stranded locally before anyone noticed. |
| Govee2MQTT restart |  |
| Internet Connectivity Monitor | Notify + change cabinet lights when internet goes down or comes back up. Forces light ON for red warning.

NOTIFY WRAPPER 2026-09-22: every direct notify.mobile_app_* call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent, color, image, url and icon values, and target set to watch or bill where the call went to those devices. Delivery behavior is unchanged; channel and importance policy now lives in the shared scripts. |
| Master Zigbee2MQTT Watchdog | State-based watchdog: if the Z2M bridge connection sensor goes offline for 10 minutes (giving the built-in Z2M watchdog time to self-recover), automatically restart the Z2M addon and send a mobile notification.

NOTIFY WRAPPER 2026-09-22: every direct notify.mobile_app_* call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent, color, image, url and icon values, and target set to watch or bill where the call went to those devices. Delivery behavior is unchanged; channel and importance policy now lives in the shared scripts. |
| Pi-hole VIP Down Alert | Sends a mobile notification when the Pi-hole VIP (192.168.10.49) stops responding to pings for 2 minutes, indicating DNS filtering may be offline.

NOTIFY WRAPPER 2026-09-22: every direct notify.mobile_app_* call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent, color, image, url and icon values, and target set to watch or bill where the call went to those devices. Delivery behavior is unchanged; channel and importance policy now lives in the shared scripts. |
| System - Deprecation Warning Alert | Notifies when a deprecation warning appears in the HA logs.

NOTIFY WRAPPER 2026-09-22: every direct notify.mobile_app_* call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent, color, image, url and icon values, and target set to watch or bill where the call went to those devices. Delivery behavior is unchanged; channel and importance policy now lives in the shared scripts. |
| Toggle Sun Visibility Dashboard Chip | Toggle dawn and dusk badges based on sun events |
