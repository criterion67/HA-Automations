# Appliances

5 automation(s) in this category.

| Automation | Description |
|---|---|
| Ego Battery Charge Monitor v3.7 (Combined) | Monitors both Ego battery chargers (Plug 1 & Plug 2). Notifies when charging starts and when the battery is ✅ Fully Charged, powers off plug with failsafe, and provides actionable notification (Snooze/Reset) with a 3-snooze limit. Includes startup recovery and failsafe cutoff.


NOTIFY WRAPPER 2026-09-22: every direct notify.mobile_app_* call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent, color, image, url and icon values, and target set to watch or bill where the call went to those devices. Delivery behavior is unchanged; channel and importance policy now lives in the shared scripts. |
| Office- Desk Lighting Remote (Unified) | Unified automation to handle both remote control and wall switch control. |
| Scent Diffuser - Scheduled 10 Minute Cycle | Turn on the scent diffuser for 60 seconds every 10 minutes when Scott is home, the thermostat is in cool or heat mode, the fan is actively running, and the time is between 8:00 a.m. and 8:00 p.m. |
| V2- Doorbell - Person Detected | G6 Pro Doorbell person detection triggers cooldown, bedroom alert light, notification, and camera stream to bedroom TV. Pauses active TV playback before stream and resumes after 1 minute. Only runs when Scott is home. On HA restart, resets any stuck cooldown boolean.

NOTIFY WRAPPER 2026-09-22: every direct notify.mobile_app_* call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent, color, image, url and icon values, and target set to watch or bill where the call went to those devices. Delivery behavior is unchanged; channel and importance policy now lives in the shared scripts. |
| Washer/Dryer Status Management | This automation monitors the washer and dryer's status, providing voice notifications for each cycle change. It also uses light color changes and mobile notifications to alert when cycles start or finish. The bedroom ceiling light state is snapshotted at the start of each run and restored at the end, so the notification flash never leaves the light in the wrong state.

ESPHOME MIGRATION 2026-10-21: triggers moved from the dead geappliances MQTT entities (sensor.machine_state_machine_status, sensor.sub_cycle_state_machine_sub_cycle) to the ESPHome GE Ultrafast Combo entities (sensor.ge_ultrafast_combo_state, sensor.ge_ultrafast_combo_sub_cycle). State names changed: Run to Running, Finished to Cycle Complete, Fill to Filling, Cool Down to Cooldown. Trigger IDs are unchanged so the choose branches still match. Every trigger ignores changes coming from unavailable or unknown, so an ESPHome reconnect mid cycle does not repeat an announcement. The Off trigger stays disabled; ESPHome has not been seen reporting Off. |
