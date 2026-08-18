# Reminders & Notifications

46 automation(s) in this category.

| Automation | Description |
|---|---|
| Bedroom Closet Alert Notification  |  |
| Bedroom Fridge Light |  |
| Bills phone location based light - Home + Neighborhood | Turns Bill’s light on when he arrives at Neighborhood or Home, and off when he leaves. Also checks state on Home Assistant startup. |
| Candle Simulated Light |  |
| Check Unavailable Entities at 8:00 AM |  |
| Dashboard - HVAC Cost Show at 6 PM | Show HVAC cost summary cards on tablet for 30 minutes at 6 PM daily |
| Dashboard - Reset Dog Bowl Dismissed When Bowl Refilled |  |
| Dashboard - Reset Garage Door Dismissed When Garage Closes |  |
| Dashboard - Reset Gate Dismissed When Gate Closes |  |
| Dashboard - Reset Mower Stuck Dismissed When Mower Clears Error | When David Mowie leaves error state, reset the dismissed flag so the alert can show again next time |
| Dawn Dusk Routine (Elevation Based v4) | Using sun elevation for natural dawn and dusk transitions. |
| Dishwasher Cycle Timer and Pod Tracker | Monitors dishwasher cycles, sends notifications, manages pod usage, and stores start time for cycle countdown. |
| Dishwasher Pods Low Notification |  |
| Dog Door Position Notification  | When the position of the dog door changes, provide a push notification for specific change. |
| Ecovacs Mower: Battery Charge Alert | Notify when mower recharges to 80%+ after being used (battery < 50%) and when battery drops to 17%. This automation triggers notifications and audio alerts  to inform you of both low battery (17%) and successful charging (80%) events. |
| Ego Battery Notification Actions (Combined) | Handles app notification actions for both plugs with a 3-snooze limit. |
| Entity Unavailable Notification (Immediate) |  |
| Garage AC Power Loss Notification |  |
| Garbage/Recycling Pickup AI Notification | On Thursday mornings between 6:00 and 7:30, a vehicle detection on the Driveway 2 camera sends a frame to LLM Vision (Google Gemini) asking for a structured JSON verdict on whether the green garbage bin and blue recycling bin have been collected. The prompt tells the model to ignore the homeowner's parked pickup, visitor vehicles, lawn equipment, neighbors, pets, and passing traffic. Nothing is written to the timeline automatically. Only when pickup_detected comes back true does the automation create an LLM Vision timeline event labeled Truck and push a notification. This replaces the old version, which stored every Thursday-morning vehicle detection on the timeline and notified unconditionally, so any passing car during that window would alert. |
| HVAC UV Bulb Monitor | Alerts when the HVAC UV purifier has drawn under 5W for a full 24 hours, which indicates a failed bulb or ballast. Uses a level-based daily check against a 24h max Statistics helper instead of an edge-based numeric_state trigger, because the original edge trigger fired once on 2026-06-20 and could never re-arm after the power stayed at 0W. Snooze defers 24h via an input_datetime stamp; Dismiss suppresses alerts until the purifier draws power again. Both are restart-safe. |
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
| Levoit Air Purifier Filter Below 10% Notification | Sends a daily notification when the Levoit filter life drops below 10%, with snooze and dismiss actions. |
| Lock Batteries: Alert below 15% with Snooze and Dismiss |  |
| Lock Offline: Possible Dead Battery Alert | If any lock is unavailable for 2+ hours, send a notification with Snooze 24h and Replaced options. Uses the same snooze store as the low battery alert. Replaced sets a 7-day snooze. |
| Master Critical System Updates Notification |  |
| Master Garage Climate Control | Central controller for garage heat and cool based on button, temperature, and freeze protection. |
| Master Wonkavator Print Finished TTS | Announce when Wonkavator finishes printing with speaker fallback and light cue |
| Master Wonkavator Print Start Reset | Resets announcement state only when a REAL new print begins |
| Master: Garage Climate Doors | Turns off heater or AC when doors open, resumes automatically when closed, and sends actionable notifications for cool/heat resume. |
| Medication Reminders with Mounjaro | Provides audible reminders and visual alerts for taking medications at designated times and days. Uses parallel actions for efficiency and restores TV lights to their original state after reminders. |
| Network Cabinet Fan Smart Control | Controls the network cabinet fan based on temperature and office presence. Turns on at 85°F or higher, off 5 min after temp drops below 85°F. Disables fan while office is occupied. Honors override via input_boolean.network_cabinet_fan_automation_enabled. |
| New consumable added to to-do list |  |
| NFC - HVAC Filter Change Reminder |  |
| Parcel box delivery notification | Plays chime and TTS when a package is delivered to the parcel box. Prevents repeat alerts using a dashboard indicator boolean. Allows manual reset and auto-reset at 6:00 AM. Adds actionable notification buttons to reset or dismiss on Scott's phone only. |
| Plant Watering Reminder by Moisture Percentage | Notify when a plant drops below its moisture threshold, with Watered action and specific plant name. 24-hour cooldown to prevent duplicate notifications. |
| Rear Gate: Open Notification | Contact sensor to monitor whether rear yard gate is open or closed. SUPPRESSED during a full yard mowing cycle: when input_boolean.mower_full_yard_cycle is on, the gate is intentionally open so the mower can reach the rear yard, and automation.mower_gate_reminders owns the messaging. |
| Rudy's Heater Offline Alert (New) |  |
| Toothbrush: Battery State Notification | Monitors the battery level for the Oral-B toothbrush and sends a notification when a recharge is necessary and also sends a follow-up notification once it has been recharged. |
| Trash Day Reminder & Reset | Trash day is Thursday. Tomorrow chip shows Wed, Today chip shows Thu. Safety reset runs Fri midnight. |
| Update Forecast High/Low Temp Today | Calls weather.get_forecasts daily and on startup to store today's forecast high/low in input_number.forecast_high_temp_today and input_number.forecast_low_temp_today for use on dashboards. |
| V2: Doorbell - Button Pressed Notification Chime | G6 Pro Doorbell button pressed. Streams camera to TVs, plays chime and TTS announcement on Dining Room Speaker. Uses medium resolution channel (1440x1920) as high-res portrait stream is not rendered correctly by Chromecast. |
| Watch charging notifications |  |
| Zigbee Keypad - Lock/Unlock Front Door | Home button + PIN unlocks front door. Away button + PIN locks front door. Wrong PIN sends rejection beep. |
