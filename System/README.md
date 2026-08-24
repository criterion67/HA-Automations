# System

10 automation(s) in this category.

| Automation | Description |
|---|---|
| Alert Light: Migraine Green Therapy Toggle (Aqara B1 Hold) | Hold the Front Door Aqara B1 button to activate 520nm migraine therapy green (RGB 0,255,0) at 100%. Uses input_boolean.migraine_therapy_mode_active as a clean flag. Snapshots previous light state into input_text.migraine_light_restore_state before activating, and restores it on deactivation. |
| Charge monitor for curtain motors | Announces via TTS when curtain motors are fully charged and reminds every 5 minutes while still plugged in |
| Energy Monitoring Plug Failsafe | Keeps all energy monitoring plugs ON. If any are turned off, they are restored and a notification is sent. |
| GitHub Backup - Daily | Runs both GitHub backup scripts at 03:00 and alerts on failure. github_backup.sh pushes the whole /config repo; automations_backup.sh pushes automations.yaml plus the per category split files to HA-Automations. Both exit codes are captured with response_variable so a failure raises a phone alert instead of only a log line. This matters because automations_backup.sh failed silently for roughly five months and 295 commits were stranded locally before anyone noticed. |
| Govee2MQTT restart |  |
| Internet Connectivity Monitor | Notify + change cabinet lights when internet goes down or comes back up. Forces light ON for red warning. |
| Master Zigbee2MQTT Watchdog | State-based watchdog: if the Z2M bridge connection sensor goes offline for 10 minutes (giving the built-in Z2M watchdog time to self-recover), automatically restart the Z2M addon and send a mobile notification. |
| Pi-hole VIP Down Alert | Sends a mobile notification when the Pi-hole VIP (192.168.10.49) stops responding to pings for 2 minutes, indicating DNS filtering may be offline. |
| System - Deprecation Warning Alert | Notifies when a deprecation warning appears in the HA logs. |
| Toggle Sun Visibility Dashboard Chip | Toggle dawn and dusk badges based on sun events |
