# Temperature & Humidity

3 automation(s) in this category.

| Automation | Description |
|---|---|
| Bathroom Humidity Fan Control | Controls hall bath and primary bath exhaust fans based on humidity sensors. Triggers: fan turns ON when humidity rises above 78% and stays there for 2 minutes (prevents false triggers from brief spikes). Fan turns OFF when humidity drops below 62% and stays there for 5 minutes (ensures room fully dries). A homeassistant_start trigger checks current humidity at startup so fans reflect correct state after a restart. Sensors: hall= sensor.temp_sensor_hall_bath_humidity, primary= sensor.temp_sensor_primary_bath_humidity. |
| Bedroom Fridge - Temp & Connectivity Alerts |  |
| CO2 Level Monitor | Changes Apollo sensor LED to purple when CO2 exceeds 1300ppm, returns to teal when below 1000ppm. |
