# _Uncategorized

46 automation(s) in this category.

| Automation | Description |
|---|---|
| Aqara 4 button remote | This automation configures actions for the Aqara 4-button remote (Opple wireless switch, now on Zigbee2MQTT). Camera streaming uses Google TV Streamer 4K via Cast (media_player.bedroom_tv_chromecast). G6 Pro Doorbell uses medium resolution channel (1440x1920) as the high resolution portrait stream (3024x4096) is not rendered correctly by Chromecast. |
| Bathroom Vanity: Double Tap Full Bright with AL Override | Double tapping up on the Bathroom Light Switch marks the vanity group as manually controlled in Adaptive Lighting, then applies the daylight scene (full brightness, 6535K). Without the manual control mark, AL re-adapts brightness back down on its next 90 second cycle because detect_non_ha_changes is off and commands sent over the Zigbee group bind are invisible to it. When the vanity group turns off from any source (paddle, presence automation, dashboard), manual control is released so AL resumes adapting on the next turn on. Replaces the former 'Bathroom light switch daylight scene' automation, which used the same double tap trigger without the AL handling. |
| Dashboard - Reset Dismissed Flags (Consolidated) | Clears the manual dismiss flags behind the conditional dashboard cards, so each alert card can appear again the next time its condition returns. Replaces six separate automations, one per flag.

Each trigger has a unique id and its own choose branch, so no branch can be shadowed by the first-match behavior of choose.

Mode is parallel with max 10. All six originals were mode single, but they were independent automations, so one firing never blocked another. Parallel preserves that independence. Every branch is a single instant input_boolean.turn_off with no delay or wait, so concurrent runs cannot race.

Mappings, all carried over unchanged:
- lawn_mower.david_mowie leaving state error clears input_boolean.mower_stuck_dismissed
- binary_sensor.rear_yard_gate to off clears input_boolean.gate_open_dismissed
- cover.garage_door to closed clears input_boolean.garage_door_open_dismissed
- sensor.dog_bowl_water_level to Full clears input_boolean.dog_bowl_empty_dismissed
- binary_sensor.dog_door to on clears input_boolean.dog_door_closed_dismissed
- sensor.nws_alerts_alerts any state change, gated on the count not being 0, clears input_boolean.nws_alert_dismissed

The NWS branch keeps its extra condition because unlike the other five it triggers on any state change of the sensor rather than on one specific target state, so it needs the not-zero guard to avoid clearing the flag when alerts drop to none.

Note on the mower trigger: it fires on leaving error with no to state specified, which is how the original behaved, so it also fires on a transition from error to unavailable. |
| Dawn Dusk Routine (Illuminance Based v5) | Illuminance-based test that replaces the sun elevation offsets. Dawn opens the bedroom curtains and runs the dawn scene when outdoor illuminance rises above 500 lx for 2 minutes. Dusk closes the curtains and runs the dusk scene when illuminance falls below 400 lx for 2 minutes. Reads sensor.weather_station_illuminance. Test version running while v4 (elevation based) is disabled. |
| Fridge Filters Weekly Countdown | Decrements the fresh air filter and water filter week counters by one every Monday morning. Each filter has a 26 week (6 month) service life, so the counters run 26 down to 0 and stop at the input_number minimum of 0. The M3 Supply Card on the Appliances view of the Mobile dashboard shows these as dots and its Pack refilled button sets the counter back to 26 when a filter is physically changed. |
| Garage AC - Apply Bill Setpoint | When Bill adjusts the dummy thermostat helper, apply the value to the real garage AC only if it is 80°F or above. Values below 80 are silently ignored — the restore automation handles snapping the AC back. |
| Garage AC - Restore Setpoint After Unauthorized Adjustment | If the garage AC temperature setpoint is lowered below 80°F while in cooling mode, silently restore it to 80°F after a 5-minute delay. Resets the timer if adjusted again before the delay expires. |
| Health - Blood Pressure Reminder (Consolidated) | Single source of truth for the blood pressure reminder, covering both the dashboard card and the phone notification. At 7:00 AM and again at 7:00 PM it clears input_boolean.bp_reminder_dismissed (which reveals the conditional card on the Mobile and Scott's Dashboard tablet views) and sends one push to the Pixel 9 tagged bp_reminder. The reminder goes away three ways, all of which end in the same state: tapping Dismiss on the phone notification, tapping the dashboard card, or a genuinely new systolic reading arriving from Health Connect. Any of those sets the boolean on and clears the phone notification by tag, so the two surfaces stay in sync. A new systolic reading also stamps input_datetime.last_bp_reading and input_number.last_known_systolic; the value-change guard on that branch prevents Health Connect resyncs and restarts from being mistaken for fresh readings. Replaces four earlier automations: the 30 minute time_pattern morning reminder, the midnight and 7 PM flag reset, the windowed auto dismiss, and the standalone stamp automation. |
| Hue Tap Dial 2: Bathroom Era 100 Media Controls | Controls the Sonos Era 100 in the bathroom using Hue Tap Dial 2. Dial adjusts volume. Button 1: Play/Pause. Button 2 short: Spotify playlist. Button 2 long: 1000 80s Hits radio (RadioBrowser via MA). Button 3: Previous Track. Button 4: Next Track. |
| HVAC Filter Reminder - Daily Check | Checks daily if HVAC filters are due and sends an actionable notification |
| HVAC Filter Reminder - Handle Actions | Handles snooze and replaced actions from HVAC filter notifications |
| Kitchen Fridge Alerts (Consolidated) | Single handler for all kitchen refrigerator and freezer alerting, replacing three automations: Temperature and Sensor, Low Battery, and No Power Draw. Every trigger has a unique id and its own choose branch, so no branch can be shadowed by the first-match behavior of choose.

Mode is parallel with max 10, inherited from the Temperature and Sensor automation, which was already parallel. The Low Battery and No Power Draw automations were mode single. Parallel is the correct choice for the merged version because these are independent notification paths that must not block one another: a battery alert should never be dropped because a temperature alert is mid-flight. Since every branch only sends a push notification and holds no state, there is no re-entrancy risk in running several at once.

Thresholds are carried over unchanged and are based on 7 day historical data plus FDA food safety guidance.
Fridge (sensor.temp_sensor_fridge): normal 35 to 39F. Early warning above 43F for 10 min. Ceiling alert above 45F for 20 min. Runaway cold below 33F for 20 min.
Freezer (sensor.inkbird_kitchen_freezer_temperature): 0F target. Early warning above 10F for 10 min. Ceiling alert above 15F for 20 min. Runaway cold below -10F for 20 min.
Sensor offline: unavailable or unknown for 30 min on either sensor indicates battery failure or a Zigbee drop, which leaves temperature monitoring blind.
Batteries (sensor.battery_sensor_fridge, sensor.inkbird_temperature_sensor_battery): below 10 percent. The low threshold is intentional because these small batteries fall off quickly once past 20 percent.
Power (sensor.kitchen_fridge): below 1W for 10 min. A fridge idles at 2.5 to 8W between compressor cycles and spikes to 75 to 330W during a run, so it never reads 0W in normal operation. Sustained zero means an unplugged cord, a tripped GFCI or breaker, a failed smart plug, or a fridge power fault. This stays a distinct branch because a power loss may not trigger a temperature alert for some time if the box was recently cooled.

All branches send a high priority push to notify.mobile_app_pixel_9 with the current reading included. |
| LCM: Calendar PIN Setter - Slot 4 | Extracts a 4-digit PIN from calendar event description and sets it on Slot 4. Clears PIN when event ends. |
| LibreLink - Sensor Expiration Notification | Sends mobile notifications and TTS announcements at 24 hours, 1 hour, and at the moment of Libre 3 sensor expiration. |
| Living Room TV - Turn Off When Bill Leaves | When Bill has been away from home for 10 minutes, turn off the Living Room Chromecast. If Scott is home, send an actionable notification first asking whether to keep it on. If no response within 2 minutes, turn it off automatically. |
| Mailbox delivery notification, 5 p.m. reminder & reset | Notifies when mail is delivered on the first mailbox opening of the day, then records a genuine second opening (mail collected) only when the delivery notification has already been standing for 30 minutes, so the door sensor bouncing during a single delivery does not falsely count as collection. Resets the notification flag daily at 6:00 AM, reminds to check the mail at 5:00 PM if the mailbox has not been opened a second time, and allows a manual reset using a dashboard button. Adds actionable notification buttons to reset or dismiss on Scott phone. Uses input_number.set_value rather than input_number.increment because Spook v5.0.0 overrides the increment service and reads a private attribute that HA core 2026.8 renamed, which raises an error and aborts the run. YOLINK LOCAL MIGRATION, 2026-08-26: the mailbox door sensor moved from the YoLink cloud integration to the YoLink Local (yolocal) integration on the YS1606-UC Local Hub. Its trigger entity changed from binary_sensor.mailbox_sensor_door to binary_sensor.mailbox_sensor. The local integration names the primary entity after the device, so the _door suffix is gone. Device class is still door, so the off to on transition still means the mailbox was opened. |
| Master Updates Notification | Notifies when any update entity becomes available or is completed, and uses the IKEA Fado lamp in the bedroom as a visual pending indicator: green while a critical infrastructure update is outstanding (HA Core, OS, Supervisor, Apps, UniFi gear), royalblue for everything else, and off once nothing is pending.

Replaces the two prior automations, Master Critical System Updates Notification and Master Standard Updates Notification. Both of those triggered on the raw state_changed event with no entity filter, so every state change across all 5,600+ entities woke them and ran four template conditions, one of which looped the entire state machine. They were also broken: their variables blocks stringified new_state, producing thousands of 'str object has no attribute name' template warnings per day and garbled notification names.

This version triggers only on sensor.pending_updates, a template helper whose state is the count of update entities currently on. Home Assistant subscribes that template to the update domain alone, so the automation is woken only when an update actually appears or completes rather than on every state change in the system.

LAMP OWNERSHIP. Neither of the old automations ever turned the lamp off, so a completed update simply relit it. This version tracks ownership with input_boolean.fado_update_indicator_active, which is set on whenever this automation lights the lamp. When the pending count reaches zero the lamp is turned off ONLY if that flag is on, so a lamp Scott turned on himself for normal bedroom use is never switched off by an update completing. A second trigger watches the lamp for any transition to off (manual, a scene such as the 11 PM Lights Off scene, or this automation itself) and clears the flag, so ownership is released as soon as anyone else takes the lamp.

The changed entity is identified as the update entity with the most recent last_changed, which is sound because last_changed only advances on an actual on/off transition, not on attribute updates. Limitation worth knowing: if two update entities flip in opposite directions within the same instant the count is unchanged and no notification fires, and if two flip the same direction at once only the most recent is named. Both are rare. The startup guard skips the unavailable to value transition after a restart so a reboot does not produce a spurious notification. |
| Medication Reminders - Handle Notification Actions | Handles taps on medication reminder notifications. Taken: dismisses the notification silently by clearing the tag. Snooze: turns on the corresponding snooze input_boolean which triggers the main reminder automation to wait 30 minutes and re-send. |
| Monthly Valve Test | On the 1st of each month, cycles the main water valve closed then open to verify it is operational. Sends a mobile notification with results. On failure, sends a critical alert and creates a persistent dashboard notification. |
| Mower Chain Advance | Drives the chained whole-yard run. script.mower_full_yard_chain starts leg one, the rear yard; this automation owns everything after that. It reads input_select.mower_chain_leg to know where the chain is and advances rear to front to side, each leg being its own single-zone session ending in a normal return and dock.

WHY THIS EXISTS: a single multi-zone job with zone_ids [3, 1, 2] failed on 2026-08-18, 2026-08-19 and 2026-08-20. The 2026-08-20 run was fully clean, with Zone mode held all the way through and no restarts, and the mower still finished the rear yard, drove to the shut garage door as if to dock, then went to the side yard and reported Some zones unreachable. Multi-zone chaining inside the mower does not work, so the chain lives in Home Assistant instead.

WHY THE THREE MINUTE HOLD ON THE DOCKED TRIGGER: two reasons, both load bearing. First, binary_sensor.jason_momower_docked flickers ON mid return, once for 33.5 seconds, so a bare trigger would fire while the mower is still outside. Second, automation.mower_garage_return waits 30 seconds after docking, rechecks, closes the door and only then clears input_boolean.mower_cycle_active, which on 2026-08-20 took until 50 seconds after the dock. Starting the next leg before that finishes would send open_cover into a closing door, and on this pulse opener that REVERSES it. Three minutes clears both with margin. Do not shorten it.

WHY THE HEALTH CONDITIONS: every advancing branch requires status notice Mowing task completed, error none, cycle flag off, garage door closed, and the mower actually charging. On 2026-08-20 the failed run docked reporting Some zones unreachable, so it would have failed this test and stopped the chain instead of advancing over a skipped zone. That is the whole point of the design.

GATE HANDLING: only the rear yard needs the gate open and only the side yard is obstructed by it, which is Scott's call. So the close-the-gate prompt fires when leg one DOCKS, a real event with no time pressure, rather than mid-mow off sensor.jason_momower_current_zone. That sensor has falsely reported Front Yard (#1) twice while the mower was physically heading elsewhere, for 98 seconds on 2026-08-18 and 84 seconds on 2026-08-20. The front leg runs regardless of gate state. The side leg requires the gate to read exactly off, so unavailable and unknown both hold the chain rather than risking it, and the chain parks at Waiting For Gate and resumes by itself when the sensor reports closed.

DOES NOT USE input_boolean.mower_full_yard_cycle. That marker enables the old mid-mow gate prompts and is deliberately left alone here. |
| Mower Garage Return | Return half of the MOVA LiDAX Ultra 2000 AWD garage sequence. Companion to script.mower_zone_cycle, which handles the outbound half.

WHY THIS IS AN AUTOMATION AND NOT PART OF THE SCRIPT
The mower can decide to come home on its own for a completed session, low battery, or rain, and a mow can run for hours. A script waiting that long would die on a Home Assistant restart and the door would never reopen, leaving the mower stranded outside a closed door. A state triggered automation survives restarts.

WHAT IT DOES
1. On binary_sensor.jason_momower_returning going on, opens the garage door and stops it after 2.5 seconds for a 21 inch opening. Verified 2026-08-11 from history: on a natural end of session the returning flag goes on 0.25 seconds after mowing goes off and stays on for about 1 minute 40 seconds before the mower docks, so there is ample time for the door to open.
3. ERROR HANDLING: if binary_sensor.jason_momower_error_active goes on during a cycle, sends an ACTIONABLE notification to Scott's Pixel 9 with two buttons, Close Garage and Leave Open, plus the current door state and the error text. The taps are handled by the companion automation Mower Notification Actions. A time based watchdog was built first and then removed on 2026-08-12 at Scott's request: an automatic close risks shutting the door on him while he is working in the garage, and it cannot tell a stalled mower from a slow one. Letting Scott decide from the notification is the safer design. NOTE: this means there is still no automatic close if the mower stalls silently without raising an error. The door would stay open until Scott notices.

2. On binary_sensor.jason_momower_docked going on, waits 30 seconds for the mower to settle, closes the door, waits for the door to travel, then clears input_boolean.mower_cycle_active and notifies Scott's Pixel 9.

The whole automation is gated on input_boolean.mower_cycle_active being on, so it only acts during a cycle that Home Assistant started. A mow started from the MOVA app will not move the garage door.

CORRECTED 2026-08-13: the returning flag DOES now fire on the lawn_mower.dock path. It was observed going on at 17:54:31, about half a second after script.mower_send_home issued its dock command. The earlier claim that it never fires on that path is wrong, whether because v0.2.68 changed the state flow or because the original 2026-08-11 observation did not generalise. Both this automation and script.mower_send_home were built on that false premise, which is why they collided on the door and shut it on the mower.

ANNOUNCEMENT ADDED 2026-08-14: the returning branch now speaks on media_player.bedroom_group via tts.home_assistant_cloud, but only between 07:00 and 19:00, and always sends a Pixel 9 notification regardless of the hour. Both run BEFORE the door-closed condition so they still fire on the script.mower_send_home path, where the door is already open and the rest of the branch is skipped.

ERROR ALERTING REBUILT 2026-08-14, now two stages. STAGE ONE fires on any error: speaks on the bedroom group between 07:00 and 19:00, and the Pixel 9 alert now uses channel alarm_stream, priority high, ttl 0 and sticky true, copied from automation.david_mowie_stuck_or_error_alert so it sounds through silent mode and survives a clear-all. STAGE TWO fires only when the error has been set for 5 minutes AND sensor.jason_momower_state_name is no longer "mowing", which separates a genuine stall from a transient bump, and it speaks at any hour. Background: on 2026-08-14 a Path blocked error latched for 25 minutes while the mower carried on mowing normally and completed the job, so a bare error flag is not by itself evidence of a problem.

SAFETY: the opener photo eyes remain the physical backstop and will reverse the door if the mower is in the doorway while it closes. |
| Mower Gate Reminders | Handles the side gate for mowing. MOST branches are scoped to a FULL YARD cycle (rear 3, front 1, side 2). Every branch is gated on input_boolean.mower_full_yard_cycle, which script.mower_full_yard_cycle sets. That marker is what stops a manual rear-then-front run from producing false gate prompts, which was Scott's specific concern on 2026-08-17.

WHY THIS EXISTS: the rear yard is only reachable with the gate open, but the gate obstructs the side yard. So the mower does the rear yard first, and Scott closes the gate while it is busy on the front yard.

BRANCH 0, reached_rear: the mower is entering the rear yard and the gate does NOT read open. Pauses immediately and alerts hard. THIS BRANCH IS UNGATED on the full yard marker, unlike every other branch, because a shut or unreadable gate on entry to the rear yard is a real problem on any session including a plain Rear Yard button press. It fails CLOSED, so unavailable and unknown from a dead sensor battery or weak signal also pause the mower.

BRANCH 1, reached_front: the rear yard is done, so tell Scott to go close the gate. Speaks at any hour, because missing this prompt is what breaks the whole cycle.

BRANCH 2, gate_closed: acknowledge so Scott knows it registered and stops wondering.

BRANCH 3, reached_side: the mower is entering the side yard with the gate STILL OPEN. Pauses the mower immediately, then alerts hard. NOTE this is a mitigation, not a guarantee: the zone transition is only reported once the mower is already moving, so it stops it quickly rather than preventing it from ever approaching the gate.

RESUME IS DELIBERATELY MANUAL. There is no resume service on this integration; the only candidate is lawn_mower.start_mowing and it is NOT yet verified whether that resumes a paused ZONE session or kicks off a whole-map mow. Until that is tested with Scott watching, branch 2 only tells him it is safe to resume and he does it himself.

BRANCH 4, cycle_ended: clears the full yard marker whenever input_boolean.mower_cycle_active clears, so a normal finish, a cancel, or an early dock all clean up.

LABEL FORM HANDLING, added 2026-08-20. All three current_zone triggers match both the friendly form and the raw form, because an integration reload or HA restart makes the sensor drop friendly names. Each also carries not_from with the same pair, so a label flip mid-run is not read as a fresh zone entry. If a fourth zone is ever added, both forms must be listed here or the branch silently never fires. |
| Mower Incomplete Job Alert | Tells Scott when a mowing job ends early and SILENTLY, so a partially mowed yard is not mistaken for a finished one.

WHY THIS EXISTS. On 2026-08-18 a Full Yard run mowed the rear yard, skipped the front yard entirely, mowed the side yard, then docked with battery to spare and no error present. Nothing in Home Assistant said a word, because every other alert keys off an error and that return looked completely normal. Scott only found out by walking outside.

REBUILT 2026-08-19 on sensor.jason_momower_status_notice. The original version compared sensor.jason_momower_mowing_progress against 95 percent, which was WRONG and false-alarmed on the successful side yard run that same evening: progress is measured against the WHOLE MAP, so a single-zone job reads around 13 percent even when it finishes perfectly. Do not reintroduce a progress threshold here.

THE SIGNAL. sensor.jason_momower_status_notice is a clean discriminator, verified against both runs on 2026-08-18:
  Successful side yard run: 'Mowing task started' 16:12:17, then 'Mowing task completed' 16:39:44, exactly as the mower turned for home.
  Failed Full Yard run: the sensor never left 'none'.
So a finished job announces itself and an abandoned one does not. This works for zone jobs and whole-map jobs alike, because it is the mower's own verdict rather than anything inferred from area covered.

WHY IT TRIGGERS ON RETURNING RATHER THAN ON DOCKED. The notice is set at the moment the mower turns for home, and a later session would overwrite it with 'Mowing task started'. Capturing it on the way home and carrying it through the wait means a self-resume cannot erase the evidence before it is read. Triggering on returning also guarantees a real session actually happened, so this cannot fire on an unrelated dock.

WHAT IT DELIBERATELY DOES NOT DO. It stays silent when an error is present, because sensor.jason_momower_error already drives two alerts in automation.mower_garage_return and a third here would be noise. It does not restart or resume anything. It reports, and Scott decides.

The notification quotes the raw notice text so an unexpected value is diagnosable rather than mysterious. |
| Mower Notification Actions | Handles the action buttons on the Jason MoMower error notification sent by automation.mower_garage_return.

WHY THIS IS A SEPARATE AUTOMATION
Mower Garage Return is gated on input_boolean.mower_cycle_active being on. If that flag were ever cleared while an error notification was still sitting on Scott's phone, a tap would silently do nothing. Handling the taps here, ungated, means the buttons always work.

WHAT IT DOES
- MOWER_CLOSE_GARAGE: closes the garage door and confirms. The cycle flag is deliberately NOT cleared, so the door will still reopen automatically if the mower later recovers and reports returning.
- MOWER_LEAVE_OPEN: acknowledges and does nothing to the door.

Both replies reuse the notification tag mower_error so they replace the original alert on the phone rather than stacking up.

CONTEXT: this replaced a time based watchdog that automatically closed the door after 15 minutes open during a cycle. Scott removed that on 2026-08-12 because it could shut the door on him while he was working in the garage, and it could not distinguish a stalled mower from a slow return. The tradeoff is that a silent stall with no error raised will leave the door open until Scott notices. |
| Mower Outbound Door Close | Closes the garage door after the mower leaves on an outbound leg. This is the outbound counterpart to automation.mower_garage_return, which owns the return leg.

WHY THIS IS AN AUTOMATION AND NOT PART OF THE SCRIPT. script.mower_zone_cycle used to own this close, and it kept losing it. On 2026-08-25 the chain ran twice and both times dreame_lawn_mower.start_zone_mowing RAISED an exception AFTER the mower had genuinely started, which aborted the script at that step and took the wait for undock, the 120 second delay and the door close with it. The garage was left standing open with the mower out on the lawn, at 08:11 and again at 09:37, and Scott had to close it by hand both times. continue_on_error was tried first and does NOT help: Home Assistant only suppresses errors an integration raises as HomeAssistantError, and this one raises an unexpected exception, which is deliberately not suppressed. A state triggered automation cannot be killed by a script dying, and it also survives a Home Assistant restart, which is the same reasoning that put the return leg in an automation.

THE MOWER DOES START. To be clear about what the raise means: it is a false positive from the integration's verification window closing too early. On 2026-08-25 it raised at 09:37:55 while the status notice read "Mowing task started" at 09:37:56 and the docked flag cleared at 09:37:58. Reported upstream as issue #166 on EvotecIT/homeassistant-dreamelawnmower.

WHAT IT DOES. Fires when the docked flag has been off for 20 seconds, waits out the remaining 100 seconds of the calibrated 120 second exit window, then closes the door if and only if it reads exactly open.

WHAT IT DOES NOT COVER. If the mower never undocks at all, this automation never fires, because there is no undock to trigger it. In that case the door close falls to the fail-safe branch still inside script.mower_zone_cycle, which only runs if the script survived long enough to reach it. A job that both fails to start the mower AND raises early would leave the door open with nothing to close it. The mower is not outside in that scenario, so it is a security gap rather than a safety one, but it is a real gap and worth closing later. |
| Mower Restart Recovery | Fires when Home Assistant finishes starting while input_boolean.mower_cycle_active is still ON, which means a restart or an integration reload landed in the middle of a mowing cycle.

WHAT IT FIXES: an integration reload resets select.jason_momower_mowing_action back to All area. Confirmed twice, at 08:25:30 on 2026-08-19 and again mid job at 12:36:31. A mower left in All area silently ignores any zone list, so the remainder of the job runs the mower's own whole map plan. This automation sets Zone again, reads it back, and tells Scott either way.

WHAT IT CANNOT FIX, AND SCOTT SHOULD NOT EXPECT IT TO: a restart KILLS the running script.mower_zone_cycle. Every remaining step in that script, including the wait for undock, the 120 second clearance delay and the garage door close, is gone and will never execute. No helper and no automation can resume a killed script. The garage door may therefore be sitting open with nothing scheduled to close it, which is why both notification branches report the live door state and tell Scott to check it himself.

WHY IT WAITS: after a restart the mower entities come back as unavailable for a while. Writing to the select before it is available would fail. The wait_template holds until the select reports a real value, then a 5 second settle, then the write.

WHY IT READS BACK: this integration can return success on a write that never reached the mower. Verified 2026-08-18, where an unverified select.select_option showed Zone optimistically in HA and a later device poll corrected it to All area. The read back after 6 seconds is the only trustworthy confirmation, and it is the same pattern already proven inside script.mower_zone_cycle.

This automation does NOT touch the garage door, does NOT restart the mow, and does NOT clear any flag. It only restores the mode and reports. Anything beyond that is Scott's call with eyes on the mower. |
| Mower Unattended Start | Catches any Jason MoMower session that Home Assistant did not start, and opens the garage door for it.

WHY THIS EXISTS. Built 2026-08-17 after a confirmed failure. During the front yard run that day the mower raised "Lidar temperature high with map" at 13:58:50 and ended the session at roughly 96 percent. automation.mower_garage_return handled that return correctly and cleared input_boolean.mower_cycle_active at 14:02:40. The mower then charged to 100 percent and RESTARTED ITSELF at 14:55:30 to finish the remaining few percent, with no command from Home Assistant or the MOVAhome app. Because the flag had been cleared, nothing opened the door on the way out and nothing opened it on the return, and Scott had to work the door by hand both times.

WHAT IT COVERS. Any undock Home Assistant did not initiate: the mower resuming an unfinished job after charging, and any session started from the MOVAhome app.

WHY IT IS A SEPARATE AUTOMATION. automation.mower_garage_return is gated on input_boolean.mower_cycle_active being ON. This one has to fire on exactly the opposite condition, so it cannot live inside that automation without breaking its gate.

HOW IT WORKS
1. Fires when binary_sensor.jason_momower_docked has been off for 10 seconds. The 10 second hold filters the known docked-flag flicker on this firmware, and costs nothing: the mower backs out, then spends roughly 60 seconds turning and positioning before it is ready to move, so it is not near the doorway for at least a minute after undocking.
2. Runs only when input_boolean.mower_cycle_active is OFF. Every Home Assistant initiated cycle raises that flag before it touches the door, so a scripted run can never reach this automation.
3. Raises the flag itself. That hands the return leg to automation.mower_garage_return exactly as if script.mower_zone_cycle had started the job, and suppresses the garage door notification and garage climate automations for the rest of the session.
4. Opens the door to the calibrated 21 inch gap, but ONLY if the door reads closed. This opener is a pulse type with no position control, and a second open pulse on a door that is open or stopped partway REVERSES it, which has stranded the mower outside before.
5. If it opened the door, it waits out the rest of the 120 second exit window and closes it. If the door was already open when the mower undocked, it leaves the door alone entirely, on the assumption Scott opened it on purpose.
6. Notifies Scott's Pixel either way, since an unattended start is something he should know about.

The flag is deliberately left ON at the end. automation.mower_garage_return clears it after the mower docks. |
| NFC Tag Actions (Consolidated) | Single handler for 11 NFC tags, replacing 11 separate automations. Each tag maps to its own trigger id and its own choose branch, so no two branches can ever match the same run and the first match behavior of choose cannot silently swallow a branch.

Mode is parallel with max 10 so scanning one tag never blocks another. The old automations were each mode single but independent of one another, so a slow action in one could not delay the rest; parallel preserves that independence. The tradeoff is that a rapid double scan of the same tag now runs twice instead of dropping the second. For the lock toggles this is harmless because both runs read the same lock state and issue the same command.

Tags handled: Front Door Deadbolt (eff1012d), Laundry Room Door Deadbolt (two separate physical tags in two different physical locations, 4b16c7c6 and 1c2ad52a, both intentional, both mapped to trigger id laundry_room), Rear Door Deadbolt (8018f3c2), Sunroom Door Deadbolt (6937711c), Bedroom Closet Deadbolt (b52cebc2), Office Door (0b24eba4, unlock only plus notify), Garage keypad (b5c0f90b), Bedside lamps (aa413690), Garbage can TTS (c5100db2).

Defect found and fixed during consolidation: tag eff1012d previously fired two separate enabled automations that performed the identical front door toggle, so every scan ran the toggle twice. It is now one branch.

The HVAC filter tag (823c6552) was REMOVED on 2026-08-20 at Scott's instruction. It had reset counter.hvac_filter_change_countdown and written a logbook entry gated on input_datetime.filter_reminder_date equalling today. That counter was orphaned, nothing decremented or displayed it, and the real filter reminder system is automation.hvac_filter_reminder_daily_check plus script.hvac_filter_replaced, which run on a 90 day cycle off input_datetime.filter_reminder_date. The counter helper was deleted. input_datetime.filter_reminder_date was KEPT because the live reminder system depends on it. The physical tag 823c6552 now does nothing.

The disabled second front door trigger (2b8bddee) is carried forward still disabled so the original intent is not lost.

NOT merged here: NFC - Toggle Garage Door from Truck (b38fed34). It uses wait_for_trigger with a 30 second timeout. Folding it in would either block every other tag for up to 30 seconds under mode single, or change its own re-entrancy under mode parallel. It stays standalone. |
| Office- Network Cabinet WLED Presence Control | Turns the network cabinet WLED strip on when office presence is detected, off after 5 min of no presence. If internet is down, skips the turn-off so the red warning from the Internet Connectivity Monitor stays active. |
| Office- Presence Lighting Control V3 | Turns office lamps, ceiling light, and fan on with presence, turns them off after 5 min of no presence, restores prior fan and ceiling light state on re-entry, and resets manual override. |
| Petkit - Feeder Notifications (Consolidated) | All notification and monitoring for Gracie's Fresh Element Solo feeder, replacing three automations: Feeder Notifications, Notify if Feed Not Dispensed, and Notify on Battery Issue. Every trigger has a unique id and its own choose branch, so no branch can be shadowed by the first-match behavior of choose.

DELIBERATELY NOT MERGED: automation.petkit_feeding_schedule, which is the automation that ACTUALLY DISPENSES FOOD (text.set_value on text.fresh_element_solo_manual_feed at 07:00, 12:00 and 18:00, 30g / 20g / 30g, plus the 9000 Hz call tone). It stays separate on purpose. Folding the feeder's own watchdog into the same automation as the actuator it watches would mean a fault in the notification path could take out feeding, and the two sets of time triggers sit only 5 minutes apart, which is harder to reason about when debugging a missed meal.

Mode is parallel with max 10. The originals were parallel max 3, parallel max 2 and single respectively, but they were independent automations so none could block another; parallel preserves that. Every branch is a single notification with no delay or wait, so concurrent runs cannot race.

The three feed watchdogs keep their original condition, that binary_sensor.fresh_element_solo_feeding has stayed off for 5 minutes. In the original that was one shared top-level condition; here it is repeated per branch so that the battery and feeder-event branches are not gated by it, which matches how the three separate automations actually behaved.

Battery semantics carried over unchanged: sensor.fresh_element_solo_battery_level reading 'Not in use' means the feeder is on USB power, and any other value means it is running on batteries. |
| Petkit - Feeding Schedule | Dispenses Gracie's three daily meals via the Fresh Element Solo and plays the 9000 Hz tone to call her. Schedule: 30g at 7:00 AM, 20g at 12:00 PM, 30g at 6:00 PM = 80g daily total. |
| Pico 2 - Bedroom Ceiling Lights Control | Controls bedroom ceiling lights using the Lutron Pico 2 remote: on, off, raise brightness, lower brightness. |
| Pico 2 - Bedroom: ON Button | Handles single, double, and hold for the Pico 2 ON button. Single=turn on, Hold=50% warm white, Double=100% warm white. |
| Power Outage - Desktop Shutdown | Shuts down SCOTT-DESKTOP when either: (1) EFR3P-1 AC has been offline for 10 minutes, or (2) Goldenmate battery drops below 25%. Both conditions ensure a graceful shutdown well before the Goldenmate runs dry. Network gear and HA host are handled separately by the EFR3P-2 automation. |
| Power Outage - EFR3P-2 Network & HA Shutdown | When EFR3P-2 battery drops to 20% while AC is offline, sets outage flag, sends mobile alert, then gracefully shuts down UNAS Pro, UDM Pro Max, and the HA host (Wyse 5070). HA will auto-restart when grid power is restored. |
| Power Restored — Recovery Notification | On HA startup, checks if the power outage shutdown flag is set. If so, sends a mobile and dashboard notification that power is restored and systems are back online, then clears the flag. Prevents false notifications on routine HA restarts. |
| Reminder - Re-pair YoLink D2D Leak Sensors to Water Valve | TEMPORARY REMINDER, created 2026-08-26. Delete or turn off this automation once the D2D re-pairing is finished.

WHY THIS EXISTS: the YoLink local hub migration on 2026-08-26 appears to have broken every Control-D2D binding between the nine water leak sensors and the main water valve. A wet sensor 8 failed to close the valve, and the valve was verified working minutes earlier by a manual test, which isolates the fault to the D2D binding rather than the valve.

Until those bindings are rebuilt the house has NO unattended automatic water shutoff. Home Assistant never closed the valve on a leak; it only announces, notifies and sirens. D2D was the entire automatic shutoff mechanism, and it is the only one that works with the power out and the internet down. A Close Water button was added to the leak notification on 2026-08-26 as a stopgap, but that requires Scott to see and tap a phone notification.

RE-PAIRING PROCEDURE, from YoLink's YS7906-UC manual. No app and no internet needed; it is all SET buttons on the devices.
1. Close the main water valve and confirm it reads closed. Do this ONCE. Nothing reopens it on its own, so it stays closed through all nine pairings.
2. On the leak sensor, hold SET for 5 to 10 seconds until the green LED blinks rapidly, then release.
3. On the valve controller, hold SET for 5 to 10 seconds until its green LED blinks rapidly, then release.
4. Pairing is confirmed when the LED stops blinking, which may be after only two or three blinks.
5. Repeat steps 2 and 3 for each of the nine sensors.
6. Open the valve when finished.

Test the FIRST pair before doing the other eight, so a broken procedure is not repeated nine times. Do not hold SET for 20 to 30 seconds; that is a factory reset.

This reminder repeats daily at 9:00 AM on purpose rather than firing once, because a single missed notification would leave a safety gap open indefinitely. Scott turns it off himself when the work is done. |
| Tablet Nightly Maintenance | Every evening at 19:00, clears the browser cache on both Galaxy Tab A9+ tablets, then performs a full device restart. After the restart delay, loads the start URL on both tablets. The bedroom tablet (A9+ 1) and office tablet (A9+ 2) run in parallel. |
| Unlock Front Door: UniFi Access Granted | When UniFi Access grants entry at the front door via any authentication method (PIN, NFC, face unlock, mobile app, or remote), unlock the front door deadbolt via Z-Wave. Triggered by the hass-unifi-access integration event entity via local WebSocket — no cloud dependency. |
| V2.2 Garage Presence Lighting Control | Controls garage ceiling lights and workbench light based on presence and PIR motion detection. Replaces V2.1 (disabled, preserved for rollback). Ceiling lights turn on when garage_presence_target_count > 0, and turn off after 60 seconds of no presence UNLESS input_boolean.workbench_occupied is on (meaning the workbench PIR sensor still detects activity). Workbench light (switch.workbench_light) turns on when binary_sensor.pir_ms_1_occupancy detects motion and turns off 5 minutes after motion clears; it also sets/clears input_boolean.workbench_occupied to prevent the ceiling lights from shutting off while someone is at the workbench. Night-time block (11:00pm-6:00am) applies to ceiling lights only, bypassed by input_boolean.garage_light_time_override. Time override resets at 6:00am daily. Manual override (input_boolean.garage_presence_override) bypasses the entire automation. |
| V2.3 Garage Presence Lighting Control | Controls garage ceiling lights (switch.garage_lights) and workbench light (switch.workbench_light) using layered presence and human confirmation logic to filter out pet false triggers (Rudy). Human presence is confirmed via any of: PIR motion (binary_sensor.pir_ms_1_occupancy), garage door opening, laundry room door opening, rear door opening. Confirmed presence sets input_boolean.human_in_garage which gates ceiling and workbench light activation. mmWave (sensor.garage_presence_target_count) holds lights on while present. Lights turn off 60 seconds after mmWave clears. Workbench light turns on with PIR motion and off 5 minutes after PIR clears. Mower guard (input_boolean.mower_cycle_active) prevents garage door open events from confirming human presence during mowing cycles. This guard previously pointed at input_boolean.david_mowie_mowing, which is a legacy orphaned helper that nothing writes to; it had restored stuck on since 2026-08-15, which silently disabled all garage-door human confirmation. Corrected 2026-08-20 to the live flag used by the 8 mower automations and 2 mower scripts. Manual override (input_boolean.garage_presence_override) bypasses all automatic logic and resets at 06:00 daily.

Three defects fixed in this revision. First, the human_in_garage reset was a 30 minute inline delay inside a parallel automation, which held an execution slot open for half an hour per confirming event and produced repeated Maximum number of runs exceeded warnings; it is now a dedicated numeric_state trigger with for 30 minutes. Second, workbench_motion_on appeared in the first choose branch, and because choose stops at the first match the dedicated workbench branch never executed, so PIR motion never actually turned the workbench light on; the two are now separate. Third, the reset condition compared sensor.garage_presence_target_count against the string 0 while the sensor reports 0.0, so it never matched; it is now a numeric_state condition. |
| Water Leak Alert - Notification Action Handler | Handles the Snooze and Dismiss buttons on the water leak notification sent by automation.water_leak_alert_1_triggered_response. Replaces the two separate handler automations, Water Leak Alert 2 - Snooze Handler and Water Leak Alert 3 - Dismiss Handler.

SNOOZE_LEAK turns input_boolean.leak_alert_snoozed on. DISMISS_LEAK turns it off. Behavior is carried over exactly unchanged from the two originals.

Mode is parallel with max 10 so a button press is always handled immediately even while another press is in flight. Both originals were mode single; since each branch is a single instant boolean write with no waiting, parallel cannot cause a race.

WHY THE ALERTING AUTOMATION IS NOT MERGED IN HERE: automation.water_leak_alert_1_triggered_response is mode restart and runs a long repeat loop that sounds the siren and re-notifies every 5 minutes. Merging these event triggers into it would mean that pressing Snooze or Dismiss restarts the automation and kills the running alert loop outright, silently changing what those buttons do. Merging the other direction, under mode parallel, would let a second leak sensor start a second concurrent siren loop instead of restarting the first. Neither is acceptable for a leak alarm, so the alerting automation stays standalone with its own mode restart.

KNOWN DEFECT IN THE ALERTING AUTOMATION, NOT CHANGED HERE: its repeat while condition is or(any sensor on, leak_alert_snoozed on). Because leak_alert_snoozed is ORed in rather than negated and ANDed, pressing Snooze does not suppress anything; it makes the loop continue even after every leak sensor has cleared, until Dismiss is pressed. The intended logic is almost certainly and(any sensor on, not snoozed). Flagged to Scott 2026-08-20, left untouched pending his decision.

CLOSE WATER BUTTON ADDED 2026-08-26. CLOSE_WATER calls valve.close_valve on valve.main_water_valve, waits up to 30 seconds for the valve to report closed, then sends a high priority confirmation push. If the valve does not confirm within 30 seconds the push instead warns that it must be checked manually, so a silent failure of the shutoff is never mistaken for success.

WHY THIS BUTTON EXISTS: Home Assistant had NO automatic water shutoff on a leak. The alerting automation only announces, notifies and sirens; nothing in the entire config closed the valve on a leak. Automatic shutoff was handled entirely by YoLink Control-D2D pairings between each leak sensor and the valve, operating at the radio level with no hub, internet or power required. On 2026-08-26 a wet sensor 8 failed to close the valve, indicating the local hub migration broke those D2D bindings, which left the house with no automatic shutoff at all. Scott chose a human-in-the-loop button over unconditional automatic shutoff so a false positive cannot cut the water while he is away. That is a deliberate decision, not an oversight. D2D remains the power-out and internet-out failsafe and is being re-paired separately using the SET buttons on the devices.

The snooze defect described above was fixed in the alerting automation on 2026-08-20; its repeat while condition is now and(any sensor on, not snoozed). |
| Water Valve Battery Low Alert | Fires when the main water valve battery sensor drops below 15%. Sends a critical mobile notification with battery type and quantity, creates a Google Calendar purchase reminder, and posts a persistent dashboard notification. |
| Weather - AI Weather Report (Hourly) | Generates a short two sentence weather narrative every hour and stores it in input_text.ai_weather_report for display on the Weather dashboard. Blends live WS90 backyard weather station readings with the next 8 hours of the Google Weather forecast, then sends both to ai_task.google_ai_task (Google Gemini, free tier). Modeled on the AI Weather Report card in the Google Weather app, which the Google Weather HA integration does not expose. If the AI call fails, for example a rate limit, the automation stops and the previous report stays on the card rather than blanking it. Also runs 2 minutes after a Home Assistant restart so the card is never stale after a reboot. |
| Wonkavator Speed Up After Layer 2 | Switches Wonkavator 3D printer speed to Ludicrous once layer 2 has completed (fires when current_layer becomes 3). Only runs when input_boolean.wonkavator_speed_boost_enabled is on, so it can be toggled per print. |
