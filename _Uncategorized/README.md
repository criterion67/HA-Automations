# _Uncategorized

113 automation(s) in this category.

| Automation | Description |
|---|---|
| Alert Light: Migraine Green Therapy Toggle (Aqara B1 Hold) | Hold the Front Door Aqara B1 button to activate 520nm migraine therapy green (RGB 0,255,0) at 100%. Uses input_boolean.migraine_therapy_mode_active as a clean flag. Snapshots previous light state into input_text.migraine_light_restore_state before activating, and restores it on deactivation. |
| Aqara 6-button remote (updated) | This automation configures actions for the Aqara 6-button remote. Camera streaming uses Google TV Streamer 4K via Cast (media_player.bedroom_tv_chromecast). |
| Bathroom Humidity Fan Control | Automate hall and primary bath exhaust fans based on respective humidity sensors. |
| Bathroom light switch daylight scene |  |
| Bathroom Lighting Control (Presence + TV v2.3) | Smart bathroom lighting tied to bedroom TV activity and mmWave presence with corrected overnight time handling. |
| Bathroom Shower: Light Timer v4.4 | Door open sets 5000 K at 100%. If still open after 1:30, red plus chime plus TTS, then back to 5000 K. After announcement, the next door close starts a 10 minute in shower timer and announces "Shower timer has started". Timer finish shows a brief red reminder, then returns to 5000 K. Light turns off when the door closes for quick in and out, or when you exit and close the door after a timed shower. |
| Bedroom Fridge - Temp & Connectivity Alerts |  |
| Bedroom Fridge Light |  |
| Bedroom Light Control: Rodret Remote | Updated for light.bedroom_bedside_lamps_group |
| Bedroom Light Switch Control - V2 Inovelli | Controlling bedroom lights via the Innovelli Smart switch mode. |
| Bedroom Sensor Recovery - Re-enable Control When Available | When bedroom sensor comes back online, dismiss the unavailability notification. |
| Bills phone location based light - Home + Neighborhood | Turns Bill’s light on when he arrives at Neighborhood or Home, and off when he leaves. Also checks state on Home Assistant startup. |
| Camera Quiet Mode - Activate | When Camera Quiet Mode is toggled on, disable person detection on all cameras with the Camera Snooze label and start a 1-hour timer to auto re-enable. |
| Camera Quiet Mode - Deactivate | When the quiet mode timer expires or the toggle is manually turned off, re-enable person detection on all cameras with the Camera Snooze label. |
| Candle Simulated Light |  |
| Car Battery Voltage Alerts (Temp Compensated) | Warn at temp-adjusted 12.2 V (20 min), critical at temp-adjusted 12.0 V (10 min) |
| CGM Monitor & Alerts (with 1hr cooldown) | Monitors blood glucose levels from sensor.librelink_glucose_measurement. Triggers alerts for readings above 180 (limited to once per hour) or below 50. Plays alerts, sends notifications, controls lights, and optionally restores TV lights. |
| Charge monitor for curtain motors |  |
| Check Unavailable Entities at 8:00 AM |  |
| Christmas Lights for December 1-31 (v2) |  |
| CO2 Level Monitor | Changes Apollo sensor LED to purple when CO2 exceeds 1300ppm, returns to teal when below 1000ppm. |
| Dashboard - HVAC Cost Show at 6 PM | Show HVAC cost summary cards on tablet for 30 minutes at 6 PM daily |
| Dashboard - Reset BP Reminder Dismissed | Re-show the BP reminder card at midnight (new day) and again at 7 PM as an evening check-in |
| Dashboard - Reset Dog Bowl Dismissed When Bowl Refilled |  |
| Dashboard - Reset Garage Door Dismissed When Garage Closes |  |
| Dashboard - Reset Gate Dismissed When Gate Closes |  |
| Dashboard - Reset Mower Stuck Dismissed When Mower Clears Error | When David Mowie leaves error state, reset the dismissed flag so the alert can show again next time |
| David Mowie Smart Mowing Automation v2 | Smart mowing cycle with dock, recharge, and conditional resume |
| David Mowie: Stuck or Error Alert | Notify phone and announce via Cloud TTS when mower goes from mowing to error, 15 minute cooldown. |
| Dawn Dusk Routine (Elevation Based v4) | Using sun elevation for natural dawn and dusk transitions. |
| Dishwasher Cycle Timer and Pod Tracker | Monitors dishwasher cycles, sends notifications, manages pod usage, and stores start time for cycle countdown. |
| Dishwasher Pods Low Notification |  |
| Doorbell - Delivery Vehicle AI Notification | When a vehicle is detected by the Driveway 2 camera, OR when the mailbox or parcel box sensors trip, captures snapshots from both Driveway 2 and the doorbell, sends both to LLM Vision to identify delivery carriers (USPS, FedEx, UPS, Amazon) and whether a package is being left. Suppresses notification if no delivery is detected. |
| Doorbell Notifications Sync (Helper <-> Reolink Switch) |  |
| Doorbell Person or Visitor - Tablet Camera View v2.0 | When a person is detected or someone presses the doorbell, wake all tablets, show the doorbell camera in full screen for 30 seconds, then return to the main dashboard. |
| Ecovacs Mower: Battery Charge Alert | Notify when mower recharges to 80%+ after being used (battery < 50%) and when battery drops to 17%. This automation triggers notifications and audio alerts  to inform you of both low battery (17%) and successful charging (80%) events. |
| Ego Battery Charge Monitor v3.7 (Combined) | Monitors both Ego battery chargers (Plug 1 & Plug 2). Notifies when charging starts and when the battery is ✅ Fully Charged, powers off plug with failsafe, and provides actionable notification (Snooze/Reset) with a 3-snooze limit. Includes startup recovery and failsafe cutoff. |
| Ego Battery Notification Actions (Combined) | Handles app notification actions for both plugs with a 3-snooze limit. |
| Emergency - Alternating Red/White Lights | This automation triggers the lights to flash alternately between red and white for 2 minutes as an emergency alert, followed by a steady white light. It involves 6 steps, alternating colors every 10 seconds. |
| Energy Monitoring Plug Failsafe | Keeps all energy monitoring plugs ON. If any are turned off, they are restored and a notification is sent. |
| Ensure Bedroom Ceiling Fan Starts at 100% |  |
| Entity Unavailable Notification (Immediate) |  |
| Evening Routine (Fully Dynamic Scenes + Verification + Retry Actions) | Executes 10 PM, 11 PM, and 12 AM scenes with dynamic entity verification for locks and lights, retry logic, actionable notifications, and safeguards for jammed/unavailable devices. |
| Front Door Lock: Aqara Button (B1) | Single press locks. Double press unlocks. |
| Garage Button Control | Controls garage lighting and door using the Aqara Mini Button via Zigbee2MQTT. • Single press → Toggles garage lights • Double press → Toggles garage night light • Hold for ≥ 4 seconds → Toggles garage door |
| Garage Door position change notifications v2 |  |
| Garage Light Override Control | Manages override mode and direct light control |
| Garbage/Recycling Pickup AI Notification | Detects when green garbage can or blue recycling bin have been emptied by city trucks on Thursday mornings. |
| GitHub Backup - Daily | Automatically backup Home Assistant configuration and automations to GitHub daily at 3 AM |
| Govee2MQTT restart |  |
| Hall Bath Presence Lighting Control v2 | Lighting control based on presence with day and night split. |
| Health - Blood Pressure Morning Reminder | Send reminder notification between 7 AM and 10 AM if blood pressure hasn't been logged today |
| HVAC UV Bulb Monitor | Notify if the HVAC UV purifier draws <5W for 24h; allow Snooze or Dismiss from the notification. |
| Internet Connectivity Monitor | Notify + change cabinet lights when internet goes down or comes back up. Forces light ON for red warning. |
| Jarvis – Finish Cleanup (Notify + Reset) | Clears room selections and sends notifications when Jarvis finishes. |
| Kitchen Fridge Alerts: Low Battery | Monitors battery level on both the refrigerator temp sensor (sensor.battery_sensor_main_fridge) and the freezer Inkbird sensor (sensor.inkbird_temperature_sensor_battery). Fires when either drops below 10%.

The 10% threshold is intentional: these sensors run on small batteries and can drop quickly once they pass 20%. A dead sensor means temperature monitoring is completely blind. Alerting at 10% gives enough lead time to replace batteries before the sensor drops offline.

Sends a high-priority push to notify.mobile_app_pixel_9 with the current battery percentage included so you know how urgent replacement is. |
| Kitchen Fridge Alerts: No Power Draw | Monitors sensor.kitchen_fridge (energy monitoring smart plug the refrigerator is connected to) for a sustained zero-watt reading.

Normal refrigerator behavior: idles at 2.5-8W between compressor cycles, then spikes to 75-330W during compressor runs. Even at idle, the plug never reads 0W under normal operation. A reading below 1W sustained for 10 minutes indicates the fridge has lost power entirely, which could mean: the plug was accidentally unplugged, a GFCI or breaker tripped, the smart plug itself has failed, or the fridge has a power fault.

This alert is intentionally separate from the temperature automations because a power loss may not immediately trigger a temperature alert, especially if the fridge was recently cooled. Catching the power loss early allows intervention before food is at risk.

Sends a high-priority push to notify.mobile_app_pixel_9. |
| Kitchen Fridge Alerts: Temperature and Sensor | Monitors kitchen refrigerator (sensor.temp_sensor_main_fridge) and freezer (sensor.inkbird_kitchen_freezer_temperature) for unsafe temperature conditions and sensor loss. Uses parallel mode so multiple simultaneous conditions each fire independently.

Thresholds based on 7-day historical data and FDA food safety guidelines:
- Fridge normal range: 35-39F. Early warning above 43F for 10 min (door left open / compressor struggling). Ceiling alert above 45F for 20 min (food safety risk). Runaway cold below 33F for 20 min (thermostat failure, food freezing risk).
- Freezer normal range: 0F target. Early warning above 10F for 10 min. Ceiling alert above 15F for 20 min (food safety failure zone). Runaway cold below -10F for 20 min (thermostat failure).
- Sensor offline: unavailable or unknown for 30 min indicates battery failure or Zigbee drop. Without sensor data, temperature monitoring is blind.

All alerts send high-priority push to notify.mobile_app_pixel_9 with current temperature included in the message. |
| Laundry Finish Time Notification |  |
| Laundry Room Presence  Lighting Control | Lighting control based on motion. |
| Levoit Air Purifier Filter Below 10% Notification | Sends a daily notification when the Levoit filter life drops below 10%, with snooze and dismiss actions. |
| Light Control: Bedroom Inovelli switch | Controls bedroom ceiling lights and bedside lamps via Inovelli switch — single tap up/down for ceiling, double tap for bedside lamps. |
| Light Control: Bill's Desk |  |
| Light Control: Bill's Recliner | Aqara mini button: single press toggles lamp, double press toggles overhead light. |
| Living Room TV - Control TV Backlighting | Turns the Living Room TV backlight on or off based on the TV's power state. Includes a 3-second retry for turn-off if the light fails to respond. |
| Lock Batteries: Alert below 15% with Snooze and Dismiss |  |
| Lock Offline: Possible Dead Battery Alert | If any lock is unavailable for 2+ hours, send a notification with Snooze 24h and Replaced options. Uses the same snooze store as the low battery alert. Replaced sets a 7-day snooze. |
| Lutron Aurora: Living Room Floor Lamps v2.5 (Performance Edition) | Ultra-responsive control with true off, daylight toggle, and stabilized dimming. |
| Mailbox delivery notification, 5 p.m. reminder & reset | Notifies when mail is delivered (only on first open of the day), resets the notification flag daily at 6:00 AM, reminds to check the mail at 5:00 PM only if the mailbox hasn't been opened a second time, and allows a manual reset using a dashboard button. Adds actionable notification buttons to reset or dismiss on Scott's phone only. |
| Master Critical System Updates Notification |  |
| Master Garage Climate Control | Central controller for garage heat and cool based on button, temperature, and freeze protection. |
| Master Standard Updates Notification |  |
| Master Wonkavator Print Finished TTS | Announce when Wonkavator finishes printing with speaker fallback and light cue |
| Master Wonkavator Print Start Reset | Resets announcement state only when a REAL new print begins |
| Master Zigbee2MQTT Watchdog | State-based watchdog: if the Z2M bridge connection sensor goes offline for 10 minutes (giving the built-in Z2M watchdog time to self-recover), automatically restart the Z2M addon and send a mobile notification. |
| Master: Garage Climate Doors | Turns off heater or AC when doors open, resumes automatically when closed, and sends actionable notifications to stop climate. |
| Medication Reminders with Mounjaro | Provides audible reminders and visual alerts for taking medications at designated times and days. Uses parallel actions for efficiency and restores TV lights to their original state after reminders. |
| Network Cabinet Fan Smart Control | Controls the network cabinet fan based on temperature and office presence. Turns on at 85°F or higher, off 5 min after temp drops below 85°F. Disables fan while office is occupied. Honors override via input_boolean.network_cabinet_fan_automation_enabled. |
| New consumable added to to-do list |  |
| NFC - Front Door Lock is scanned |  |
| NFC - Garbage Can is scanned |  |
| NFC - HVAC Filter Change Reminder |  |
| NFC - Laundry Room Door Lock is scanned |  |
| NFC - Rear Door Lock is scanned |  |
| NFC - Sunroom Door Lock is scanned |  |
| NFC - Toggle Garage Door from Truck | NFC tag on dashboard will toggle garage door and lock/unlock laundry room door with failsafe notification. |
| Office- Ceiling Light Presence Control V2 | Turns ceiling light on with presence, turns it off after 5 min of no presence, and resets manual override. |
| Office- Desk Lighting Remote (Unified) | Unified automation to handle both remote control and wall switch control. |
| Parcel box delivery notification | Plays chime and TTS when a package is delivered to the parcel box. Prevents repeat alerts using a dashboard indicator boolean. Allows manual reset and auto-reset at 6:00 AM. Adds actionable notification buttons to reset or dismiss on Scott's phone only. |
| Pi-hole VIP Down Alert | Sends a mobile notification when the Pi-hole VIP (192.168.10.49) stops responding to pings for 2 minutes, indicating DNS filtering may be offline. |
| Possible Mail Delivery AI Notification | Detects possible USPS mail delivery from driveway camera. DISABLED - replaced by Doorbell - Delivery Vehicle AI Notification. |
| Presence Sensor Self Heal |  |
| Ring Door Chime |  |
| Scent Diffuser - Scheduled 10 Minute Cycle | Turn on the scent diffuser for 60 seconds every 10 minutes when Scott is home, the thermostat is in cool or heat mode, the fan is actively running, and the time is between 8:00 a.m. and 8:00 p.m. |
| Shower Light Switch |  |
| System - Deprecation Warning Alert | Notifies when a deprecation warning appears in the HA logs. |
| Toggle Sun Visibility Dashboard Chip | Toggle sunrise and sunset badges based on sun events |
| Toothbrush: Mirror Light Control | Turns bathroom mirror light on when toothbrush is running, off when idle. |
| Update Forecast Low Temp Today | Calls weather.get_forecasts daily and on startup to store today's forecast low in input_number.forecast_low_temp_today for use in dashboard visibility conditions. |
| V2- Doorbell - Person Detected |  |
| V2.1 Garage Presence Lighting Control | Controls garage lights based on presence detection unless the manual override is enabled. Lights will not turn on between 11:00 p.m. and 6:00 a.m. unless the time override toggle is enabled. Also resets the time override toggle each morning at 6:00 a.m. |
| V2: Doorbell - Button Pressed Notification Chime | Doorbell button pressed - streams cameras to TVs, plays chime and TTS announcement on Dining Room Speaker. |
| Vacation Water and Light Control |  |
| Vacuum Bedroom & Bathroom via Inovelli Config Button | Hold the config button on the Inovelli bedroom switch to vacuum bedroom (segment 1) and bathroom (segment 2). |
| Washer/Dryer Status Management | This automation monitors the washer and dryer's status, providing voice notifications for each cycle change. It also uses light color changes and mobile notifications to alert when cycles start or finish. |
| Watch charging notifications |  |
| Water Leak Alert 1 - Triggered Response |  |
| Water Leak Alert 2 - Snooze Handler |  |
| Water Leak Alert 3 - Dismiss Handler |  |
| Wonkavator Print Almost Done Notification |  |
| Zigbee Keypad - Lock/Unlock Front Door | Home button + PIN unlocks front door. Away button + PIN locks front door. Wrong PIN sends rejection beep. |
| Zone 2 Media Announcement Sample | Announces that the robot vacuum has completed cleaning and is returning to the dock. |
| Zooz Scene Button 1&2 - Bedroom Ceiling Fan On&Off | Controls bedroom ceiling fan on/off via Zooz scene buttons 1 and 2. |
