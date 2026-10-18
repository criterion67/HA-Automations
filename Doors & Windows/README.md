# Doors & Windows

6 automation(s) in this category.

| Automation | Description |
|---|---|
| Attic Lights: Door Controlled | Attic light is switched on and off based on the open) closed state of either interior or garage attic doors. |
| Front Door Deadbolt: Aqara Button (B1) | Single press locks. Double press unlocks. |
| Front Door: Locked/Unlocked - Light Control | The foyer and hall lights will turn on or off based on the front door being unlocked or locked after sunset and before sunrise. |
| Garage Door position change notifications v2 | Announces and notifies on garage door open and close: flashes the bedroom alert light red on open and turns it off on close, plays TTS on the bedroom speaker, sends a phone notification, and runs an LED effect on the Bedroom Light Switch (Inovelli).

MOWER CYCLE BEHAVIOR (changed 2026-10-17). While input_boolean.mower_cycle_active is on, the automation still runs so the bedroom alert light and the Inovelli LED effect show that the garage door is open. Only the TTS announcement, the phone notification and the Living Room Floor Lamp 1 turn off are skipped, each wrapped in an if block gated on the flag being off. This replaced the old top level condition that suppressed everything, so a mower cycle no longer fires four TTS announcements and four notifications into the bedroom but still gives a visual.

NOTIFY WRAPPER 2026-09-22: every direct notify.mobile_app_* call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent, color, image, url and icon values, and target set to watch or bill where the call went to those devices. Delivery behavior is unchanged; channel and importance policy now lives in the shared scripts. |
| Garage Lights: Off when Door is locked | Turns off garage ceiling lights and workbench light (switch.workbench_light) when the laundry room door deadbolt is locked. Also clears input_boolean.workbench_occupied to reset workbench presence state. |
| Ring Door Chime |  |
