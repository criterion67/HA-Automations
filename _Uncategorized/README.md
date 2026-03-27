# _Uncategorized

5 automation(s) in this category.

| Automation | Description |
|---|---|
| Controller - Philips Hue Smart Button Blueprint - Taken Control |  |
| Hue Button - Desk Lamp Control | Blueprint-based automation for the Philips Hue Smart Button (RDM005) controlling light.desk_lamp_short. Short press toggles the lamp. Long press loops brightness up 15% per repeat while held, stops on release. Uses fixed EPMatt awesome-ha-blueprints controller blueprint - Z2M action mapping corrected from ROM001 strings (press/hold/release) to RDM005 strings (on/brightness_move_up/brightness_stop). |
| Medication Reminders - Handle Notification Actions | Handles taps on medication reminder notifications. Taken: dismisses the notification silently by clearing the tag. Snooze: turns on the corresponding snooze input_boolean which triggers the main reminder automation to wait 30 minutes and re-send. |
| Medication Reminders - Mobile Notifications | Sends mobile notifications to Pixel 9 at each scheduled medication time with Snooze (30 min) and Taken action buttons. Six time slots: 7am (Levothyroxine), 8am (morning meds + antibiotics), 10am (supplements), 5pm (Levofloxacin), 7pm (evening meds), bedtime (Magnesium). Snooze fires a second notification after 30 minutes by turning on the corresponding input_boolean snooze flag, which re-triggers via state change. Taken dismisses without re-alerting. |
| TEST - Doorbell Button Press Triggers Chime | Test automation: triggered by an incoming webhook HTTP POST to /api/webhook/doorbell_chime_trigger. Intended to be called by the Reolink doorbell's built-in HTTP alarm action when the button is pressed. Plays tone ring_doorbell.mp3 (6 sec) on the Zooz ZSE50 chime via siren.chime_play_tone. Uses restart mode so rapid presses reset the sequence. |
