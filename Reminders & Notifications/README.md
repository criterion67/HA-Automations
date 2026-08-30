# Reminders & Notifications

35 automation(s) in this category.

| Automation | Description |
|---|---|
| Bedroom Closet Alert Notification  |  |
| Bedroom Fridge Light |  |
| Bills phone location based light - Home + Neighborhood | Turns Bill’s light on when he arrives at Neighborhood or Home, and off when he leaves. Also checks state on Home Assistant startup. |
| Candle Simulated Light |  |
| Check Unavailable Entities at 8:00 AM |  |
| Dashboard - HVAC Cost Show at 6 PM | Show HVAC cost summary cards on tablet for 30 minutes at 6 PM daily |
| Dishwasher Cycle Timer and Pod Tracker | Monitors dishwasher cycles, sends notifications, manages pod usage, and stores start time for cycle countdown. |
| Dishwasher Pods Low Notification |  |
| Dog Door Position Notification  | When the position of the dog door changes, provide a push notification for specific change. |
| Ecovacs Mower: Battery Charge Alert | Notify when mower recharges to 80%+ after being used (battery < 50%) and when battery drops to 17%. This automation triggers notifications and audio alerts  to inform you of both low battery (17%) and successful charging (80%) events. |
| Ego Battery Notification Actions (Combined) | Handles app notification actions for both plugs with a 3-snooze limit. |
| Garage AC Power Loss Notification |  |
| Garbage/Recycling Pickup AI Notification | On Thursday mornings between 6:00 and 7:30, a vehicle detection on the Driveway 2 camera sends a frame to LLM Vision (Google Gemini) asking for a structured JSON verdict on whether the green garbage bin and blue recycling bin have been collected. The prompt tells the model to ignore the homeowner's parked pickup, visitor vehicles, lawn equipment, neighbors, pets, and passing traffic. Nothing is written to the timeline automatically. Only when pickup_detected comes back true does the automation create an LLM Vision timeline event labeled Truck and push a notification. This replaces the old version, which stored every Thursday-morning vehicle detection on the timeline and notified unconditionally, so any passing car during that window would alert. |
| HVAC UV Bulb Monitor | Alerts when the HVAC UV purifier has drawn under 5W for a full 24 hours, which indicates a failed bulb or ballast. Uses a level-based daily check against a 24h max Statistics helper instead of an edge-based numeric_state trigger, because the original edge trigger fired once on 2026-06-20 and could never re-arm after the power stayed at 0W. Snooze defers 24h via an input_datetime stamp; Dismiss suppresses alerts until the purifier draws power again. Both are restart-safe. |
| Laundry Finish Time Notification |  |
| Levoit Air Purifier Filter Below 10% Notification | Notifies when the bedroom Levoit air purifier filter life drops below 10 percent. Fires on the threshold crossing and again daily at 09:00 while still low. Snooze pushes the next reminder to 08:00 tomorrow, Dismiss suppresses reminders until midnight tomorrow. Notification action names are namespaced (LEVOIT_FILTER_SNOOZE and LEVOIT_FILTER_DISMISS) so they cannot collide with other automations handling mobile notification actions. Suppression windows are compared using each input_datetime timestamp attribute rather than strptime, which previously raised a naive versus aware datetime error on every evaluation. Trigger threshold was 20 while the condition required below 10, so the threshold crossing never produced a notification; both are now 10. REPOINTED 2026-08-29: this automation previously watched sensor.bedroom_air_purifier_filter_life, which is a dead entity and, despite its entity_id, actually belonged to the Office purifier rather than the Bedroom one. It now reads sensor.bedroom_vital_200s_1_filter_lifetime, the live Bedroom Vital 200S filter sensor. EXTENDED 2026-08-29 to cover BOTH live purifiers: the Bedroom Vital 200S and the Living Room unit. The notification names whichever unit tripped, via trigger.to_state.name. KNOWN LIMITATION: Snooze and Dismiss write to the two shared input_datetime helpers, so snoozing one purifier snoozes both. Because the two filters sit only a few percent apart they are likely to go low around the same time; if that becomes annoying, give each unit its own pair of snooze/dismiss helpers. |
| Lock Batteries: Alert below 15% with Snooze and Dismiss |  |
| Lock Offline: Possible Dead Battery Alert | If any lock stays unavailable past its offline window, send a notification with Snooze 24h and Replaced options. The four Z-Wave locks use a 2 hour window. The bedroom closet Yale Bluetooth lock uses a 6 hour window because Bluetooth dropouts are more frequent and normally self recovering. Uses the same snooze store as the low battery alert. Replaced sets a 7 day snooze. |
| Master Garage Climate Control | Central controller for garage heat and cool based on button, temperature, and freeze protection. |
| Master Wonkavator Print Finished TTS | Announce when Wonkavator finishes printing with speaker fallback and light cue |
| Master Wonkavator Print Start Reset | Resets announcement state only when a REAL new print begins |
| Master: Garage Climate Doors | Turns off heater or AC when doors open, resumes automatically when closed, and sends actionable notifications for cool/heat resume. |
| Medication Reminders with Mounjaro | Provides audible reminders and visual alerts for taking medications at designated times and days. Uses parallel actions for efficiency and restores TV lights to their original state after reminders. |
| Network Cabinet Fan Smart Control | Controls the network cabinet fan based on temperature and office presence. Turns on at 85°F or higher, off 5 min after temp drops below 85°F. Disables fan while office is occupied. Honors override via input_boolean.network_cabinet_fan_automation_enabled. |
| New consumable added to to-do list |  |
| Parcel box delivery notification | Plays chime and TTS when a package is delivered to the parcel box. Prevents repeat alerts using a dashboard indicator boolean. Allows manual reset and auto-reset at 6:00 AM. Adds actionable notification buttons to reset or dismiss on Scott's phone only. |
| Plant Watering Reminder by Moisture Percentage | Notify when a plant drops below its moisture threshold, with Watered action and specific plant name. 24-hour cooldown to prevent duplicate notifications. |
| Rear Gate: Open Notification | Contact sensor to monitor whether rear yard gate is open or closed. SUPPRESSED during a full yard mowing cycle: when input_boolean.mower_full_yard_cycle is on, the gate is intentionally open so the mower can reach the rear yard, and automation.mower_gate_reminders owns the messaging. |
| Rudy's Heater Offline Alert (New) |  |
| Toothbrush: Battery State Notification | Monitors the battery level for the Oral-B toothbrush and sends a notification when a recharge is necessary and also sends a follow-up notification once it has been recharged. |
| Trash Day Reminder & Reset | Trash day is Thursday. Tomorrow chip shows Wed, Today chip shows Thu. Safety reset runs Fri midnight. |
| Update Forecast High/Low Temp Today | Calls weather.get_forecasts daily and on startup to store today's forecast high/low in input_number.forecast_high_temp_today and input_number.forecast_low_temp_today for use on dashboards. |
| V2: Doorbell - Button Pressed Notification Chime | G6 Pro Doorbell button pressed. Streams camera to TVs, plays chime and TTS announcement on Dining Room Speaker. Uses medium resolution channel (1440x1920) as high-res portrait stream is not rendered correctly by Chromecast. |
| Watch charging notifications | Chimes and announces on the bedroom speaker when the watch starts charging, and again when it reaches full, with a push on the full event.

ENTITY RENAME 2026-08-30: sensor.galaxy_watch7_904t_battery_state became sensor.scott_s_watch_battery_state. The watch entities were renamed off the model number so a future watch upgrade drops straight in without editing automations. |
| Zigbee Keypad - Lock/Unlock Front Door | Home button + PIN unlocks front door. Away button + PIN locks front door. Wrong PIN sends rejection beep. |
