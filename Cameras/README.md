# Cameras

4 automation(s) in this category.

| Automation | Description |
|---|---|
| Camera Quiet Mode - Activate | When Camera Quiet Mode is toggled on, disable person detection on all cameras with the Camera Snooze label and start a 1-hour timer to auto re-enable. |
| Camera Quiet Mode - Deactivate | When the quiet mode timer expires or the toggle is manually turned off, re-enable person detection on all cameras with the Camera Snooze label. |
| Doorbell Person or Visitor - Tablet Camera View v2.0 | When a person is detected or someone presses the G6 Pro Doorbell, wake all tablets, show the doorbell camera in full screen for 30 seconds, then return to the main dashboard. |
| Water Leak Alert 1 - Triggered Response | Sounds the alarm for a detected water leak: TTS announcement on media_player.all_speakers naming the sensor, a high priority actionable push with Snooze and Dismiss, then three siren pulses on switch.ring_alarm_siren, repeating every 5 minutes until the leak clears or the alert is snoozed.

Mode is restart so a second leak sensor tripping restarts the loop and re-announces with the new sensor name rather than starting a competing siren.

DEFECT FIXED 2026-08-20: the repeat while condition was or(any sensor on, leak_alert_snoozed on). Because the snooze flag was ORed in rather than negated and ANDed, pressing Snooze suppressed nothing and instead kept the siren looping after every sensor had cleared, until Dismiss was pressed. It is now and(any sensor on, not snoozed), so Snooze actually stops the loop and the loop ends on its own when the leak clears.

The Snooze and Dismiss buttons are handled by automation.water_leak_alert_notification_action_handler, which sets and clears input_boolean.leak_alert_snoozed. Nothing automatically clears the snooze flag, so after snoozing a leak you must press Dismiss (or clear the boolean) before this alarm can sound again.

SIREN RESTORED 2026-08-30. From 2026-08-21 this automation used a temporary Ring Chime fallback because switch.ring_alarm_siren had disappeared. ROOT CAUSE, now confirmed: Scott had excluded all of his Z-Wave contact sensors from the Ring base station and paired them directly to Home Assistant. With no sensors enrolled, Ring stops returning the security-panel device in its API, so ring-mqtt never publishes the alarm_control_panel or the siren switch. This matches ring-mqtt discussion #1073, where another user hit the same thing and resolved it the same way. Re-enrolling a single contact sensor in the Ring app on 2026-08-30 brought the security-panel device back within seconds, and ring-mqtt rebuilt both entities on their original entity_ids automatically. The siren step pulses switch.ring_alarm_siren again. KEEP AT LEAST ONE SENSOR ENROLLED IN THE RING APP, or the panel and siren will vanish again.

YOLINK LOCAL MIGRATION, 2026-08-26. All nine leak sensors moved off the YoLink cloud integration onto the YoLink Local (yolocal) HACS integration, which talks straight to the YS1606-UC Local Hub at 192.168.30.11 over HTTP 1080 and MQTT 18080. Every entity_id in this automation changed as a result; old ids such as binary_sensor.leak_sensor_1_moisture_2 and binary_sensor.hvac_condensate_pan_sensor_9 no longer exist. The nine sensors are now named for their location. The trigger list is deliberately explicit rather than label driven: HA state triggers cannot resolve entity_id from a template, and a label driven list would silently pull in the gate and mailbox door sensors, which carry the same Yolink Local and LoRa labels. triggered_sensor still resolves from trigger.to_state.name, so the TTS announcement and the actionable push both continue to name the specific sensor that tripped.

CLOSE WATER BUTTON ADDED 2026-08-26. The actionable push now carries three buttons: Close Water, Snooze, Dismiss. Close Water is listed FIRST so it is the one reachable without expanding the notification, since it is the only one that stops the damage. It fires the CLOSE_WATER action, handled by automation.water_leak_alert_notification_action_handler, which closes valve.main_water_valve, waits up to 30 seconds for confirmation, and pushes back either success or a warning to check the valve manually.

This automation still does NOT close the valve on its own, by deliberate choice. Automatic unconditional shutoff would mean a single false positive cuts the water while Scott is away. The shutoff stays human-in-the-loop here, with YoLink Control-D2D providing the unattended failsafe at the radio level for the power-out and internet-out case.

TTS TARGET FIXED 2026-08-29. The announcement step targeted media_player.whole_house, a Music Assistant entity that no longer exists, so the spoken leak warning could not play. It now targets media_player.all_speakers, the house-wide Cast speaker group. Note that Music Assistant duplicates of these speaker groups carry a _2 suffix and are NOT valid TTS targets. |
