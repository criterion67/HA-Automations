# Robot

3 automation(s) in this category.

| Automation | Description |
|---|---|
| David Mowie: Stuck or Error Alert | Notify phone and announce via Cloud TTS when mower goes from mowing to error, 15 minute cooldown.

NOTIFY WRAPPER 2026-09-22: every notify.mobile_app_pixel_9 call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent and icon values. Delivery behavior is unchanged; channel and importance policy now lives in the shared script. |
| Elsa – Finish Cleanup (Notify + Reset) | Clears room selections and sends notifications when Elsa finishes.

NOTIFY WRAPPER 2026-09-22: every direct notify.mobile_app_* call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent, color, image, url and icon values, and target set to watch or bill where the call went to those devices. Delivery behavior is unchanged; channel and importance policy now lives in the shared scripts. |
| Vacuum Bedroom & Bathroom via Inovelli Config Button | Hold the config button on the Inovelli bedroom switch to vacuum bedroom (segment 1) and bathroom (segment 2). |
