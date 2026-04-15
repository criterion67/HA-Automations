# _Uncategorized

13 automation(s) in this category.

| Automation | Description |
|---|---|
| Controller - Philips Hue Smart Button Blueprint - Taken Control |  |
| Hue Button - Desk Lamp Control | Blueprint-based automation for the Philips Hue Smart Button (RDM005) controlling light.desk_lamp_short. Short press toggles the lamp. Long press loops brightness up 15% per repeat while held, stops on release. Uses fixed EPMatt awesome-ha-blueprints controller blueprint - Z2M action mapping corrected from ROM001 strings (press/hold/release) to RDM005 strings (on/brightness_move_up/brightness_stop). |
| LCM: Calendar PIN Setter - Slot 4 | Extracts a 4-digit PIN from calendar event description and sets it on Slot 4. Clears PIN when event ends. |
| LCM: Calendar Slot Enable/Disable - Slot 4 | Enables Slot 4 when a Gmail calendar event starts, disables it when the event ends. Works alongside Calendar PIN Setter. |
| LCM: Slot Usage Limiter - Slot 4 | Decrements the usage counter each time Slot 4 PIN is used. Disables slot when counter reaches 0. |
| LibreLink - Sensor Expiration Notification | Sends mobile notifications and TTS announcements at 24 hours, 1 hour, and at the moment of Libre 3 sensor expiration. |
| Medication Reminders - Handle Notification Actions | Handles taps on medication reminder notifications. Taken: dismisses the notification silently by clearing the tag. Snooze: turns on the corresponding snooze input_boolean which triggers the main reminder automation to wait 30 minutes and re-send. |
| Medication Reminders - Mobile Notifications | Sends mobile notifications to Pixel 9 at each scheduled medication time with Snooze (30 min) and Taken action buttons. Six time slots: 7am (Levothyroxine), 8am (morning meds + antibiotics), 10am (supplements), 5pm (Levofloxacin), 7pm (evening meds), bedtime (Magnesium). Snooze fires a second notification after 30 minutes by turning on the corresponding input_boolean snooze flag, which re-triggers via state change. Taken dismisses without re-alerting. |
| Office- Network Cabinet WLED Presence Control | Turns the network cabinet WLED strip on when office presence is detected, off after 5 min of no presence. If internet is down, skips the turn-off so the red warning from the Internet Connectivity Monitor stays active. |
| Office- Presence Lighting Control V3 | Turns office lamps on with presence, turns them off after 5 min of no presence, and resets manual override. Replaces V2 which controlled the ceiling light. |
| Power Outage - Graceful Shutdown Sequence | When EcoFlow River 3 (EFR3P-1) detects AC power loss for 2 minutes, gracefully shuts down SCOTT-DESKTOP, UNAS Pro, UDM Pro Max, then Home Assistant itself. |
| TEST - Doorbell Button Press Triggers Chime | Test automation: triggered by an incoming webhook HTTP POST to /api/webhook/doorbell_chime_trigger. Intended to be called by the Reolink doorbell's built-in HTTP alarm action when the button is pressed. Plays tone ring_doorbell.mp3 (6 sec) on the Zooz ZSE50 chime via siren.chime_play_tone. Uses restart mode so rapid presses reset the sequence. |
| Unlock Front Door: UniFi Access Granted | When UniFi Access grants entry at the front door via any authentication method (PIN, NFC, face unlock, mobile app, or remote), unlock the front door deadbolt via Z-Wave. Triggered by the hass-unifi-access integration event entity via local WebSocket — no cloud dependency. |
