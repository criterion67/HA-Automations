# Health & Safety

4 automation(s) in this category.

| Automation | Description |
|---|---|
| Alert Light: Migraine Green Therapy Toggle (Aqara B1 Hold) | Hold the Front Door Aqara B1 button to activate 520nm migraine therapy green (RGB 0,255,0) at 100%. Uses input_boolean.migraine_therapy_mode_active as a clean flag. Snapshots previous light state into input_text.migraine_light_restore_state before activating, and restores it on deactivation. |
| CGM Monitor & Alerts (with 1hr cooldown) | Monitors blood glucose levels from sensor.librelink_glucose_measurement. Triggers alerts for readings above 180 (limited to once per hour) or below 50. Plays alerts, sends notifications, controls lights, and optionally restores TV lights. |
| CO2 Level Monitor | Changes Apollo sensor LED to purple when CO2 exceeds 1300ppm, returns to teal when below 1000ppm. |
| Health - Blood Pressure Morning Reminder | Send reminder notification between 7 AM and 10 AM if blood pressure hasn't been logged today |
