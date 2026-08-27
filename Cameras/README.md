# Cameras

4 automation(s) in this category.

| Automation | Description |
|---|---|
| Camera Quiet Mode - Activate | When Camera Quiet Mode is toggled on, disable person detection on all cameras with the Camera Snooze label and start a 1-hour timer to auto re-enable. |
| Camera Quiet Mode - Deactivate | When the quiet mode timer expires or the toggle is manually turned off, re-enable person detection on all cameras with the Camera Snooze label. |
| Doorbell Person or Visitor - Tablet Camera View v2.0 | When a person is detected or someone presses the G6 Pro Doorbell, wake all tablets, show the doorbell camera in full screen for 30 seconds, then return to the main dashboard. |
| Water Leak Alert 1 - Triggered Response | Sounds the alarm for a detected water leak: TTS announcement on media_player.whole_house naming the sensor, a high priority actionable push with Snooze and Dismiss, then three siren pulses on switch.ring_alarm_siren, repeating every 5 minutes until the leak clears or the alert is snoozed.

Mode is restart so a second leak sensor tripping restarts the loop and re-announces with the new sensor name rather than starting a competing siren.

DEFECT FIXED 2026-08-20: the repeat while condition was or(any sensor on, leak_alert_snoozed on). Because the snooze flag was ORed in rather than negated and ANDed, pressing Snooze suppressed nothing and instead kept the siren looping after every sensor had cleared, until Dismiss was pressed. It is now and(any sensor on, not snoozed), so Snooze actually stops the loop and the loop ends on its own when the leak clears.

The Snooze and Dismiss buttons are handled by automation.water_leak_alert_notification_action_handler, which sets and clears input_boolean.leak_alert_snoozed. Nothing automatically clears the snooze flag, so after snoozing a leak you must press Dismiss (or clear the boolean) before this alarm can sound again.

TEMPORARY SIREN FALLBACK, APPLIED 2026-08-21 - REVERT THIS WHEN THE RING SIREN RETURNS.

This automation used to pulse switch.ring_alarm_siren three times. That entity no longer exists. The Ring Alarm security panel device (Ring zid 6f3a0b61-64c5-4b2d-b835-68d429ad00a0), which carried BOTH the alarm_control_panel and the siren switch, stopped being published by the ring-mqtt add-on around 2026-08-15. Ruled out as causes: authentication, the add-on state file, the add-on version (5.9.3 is latest), and the HA entity registry. A complete uninstall, reinstall and re-authentication of ring-mqtt on 2026-08-21 rediscovered from scratch and still returned only three devices - Base Station (ece94eb9-b82f-4452-a387-3c64368ff224), Keypad 1 (2a6309f1-76c2-431c-a3c7-d77b2dbff9f6) and Keypad 2 (f6129287-6437-4ced-a2d0-16925827a75b). The alarm itself is healthy and arms and disarms normally from the Ring phone app, so the panel exists on the Ring account and ring-mqtt is simply not being given it. Open with the ring-mqtt maintainer.

UNTIL THEN the siren step uses siren.chime_play_tone, the Ring Chime, tone 3 (siren2.mp3, 40 seconds) at full volume with an 8 second duration per pulse, keeping the original three-pulse 8-on 12-off rhythm. Scott's stated preference is to go back to the Ring siren, so when a Ring siren entity reappears, replace this whole fallback block and delete these two paragraphs.

YOLINK LOCAL MIGRATION, 2026-08-26. All nine leak sensors moved off the YoLink cloud integration onto the YoLink Local (yolocal) HACS integration, which talks straight to the YS1606-UC Local Hub at 192.168.30.11 over HTTP 1080 and MQTT 18080. Every entity_id in this automation changed as a result; old ids such as binary_sensor.leak_sensor_1_moisture_2 and binary_sensor.hvac_condensate_pan_sensor_9 no longer exist. The nine sensors are now named for their location. The trigger list is deliberately explicit rather than label driven: HA state triggers cannot resolve entity_id from a template, and a label driven list would silently pull in the gate and mailbox door sensors, which carry the same Yolink Local and LoRa labels. triggered_sensor still resolves from trigger.to_state.name, so the TTS announcement and the actionable push both continue to name the specific sensor that tripped.

CLOSE WATER BUTTON ADDED 2026-08-26. The actionable push now carries three buttons: Close Water, Snooze, Dismiss. Close Water is listed FIRST so it is the one reachable without expanding the notification, since it is the only one that stops the damage. It fires the CLOSE_WATER action, handled by automation.water_leak_alert_notification_action_handler, which closes valve.main_water_valve, waits up to 30 seconds for confirmation, and pushes back either success or a warning to check the valve manually.

This automation still does NOT close the valve on its own, by deliberate choice. Automatic unconditional shutoff would mean a single false positive cuts the water while Scott is away. The shutoff stays human-in-the-loop here, with YoLink Control-D2D providing the unattended failsafe at the radio level for the power-out and internet-out case. |
