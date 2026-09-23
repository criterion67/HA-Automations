# Temperature & Humidity

3 automation(s) in this category.

| Automation | Description |
|---|---|
| Bathroom Humidity Fan Control | Controls hall bath and primary bath exhaust fans based on humidity sensors. Triggers: fan turns ON when humidity rises above 78% and stays there for 2 minutes (prevents false triggers from brief spikes). Fan turns OFF when humidity drops below 62% and stays there for 5 minutes (ensures room fully dries). A homeassistant_start trigger checks current humidity at startup so fans reflect correct state after a restart. Sensors: hall= sensor.temp_sensor_hall_bath_humidity, primary= sensor.temp_sensor_primary_bath_humidity. |
| Bedroom Fridge - Temp & Connectivity Alerts | Two branches. HOT: bedroom fridge temperature above 50F for 30 minutes. Repeats hourly with a chime, a TTS announcement on the bedroom group and an alarm_stream push. Deliberately loud, because food is spoiling. OFFLINE: the temperature sensor reads unavailable or unknown for 30 minutes. Chime and TTS as before, but the phone push was moved to the Quiet Notices channel at low importance on 2026-08-31 at Scott request. A sensor connectivity fault is not a spoilage emergency and must not use the Android alarm audio stream, which bypasses silent mode and Do Not Disturb.

NOTIFY WRAPPER 2026-09-22: every notify.mobile_app_pixel_9 call was replaced by script.notify_alert (or script.notify_clear for clear_notification) with the same message, title, tag, channel, importance, priority, ttl, actions, sticky, persistent and icon values. Delivery behavior is unchanged; channel and importance policy now lives in the shared script. |
| CO2 Level Monitor | Changes Apollo sensor LED to purple when CO2 exceeds 1300ppm, returns to teal when below 1000ppm. |
