# NFC Tags

13 automation(s) in this category.

| Automation | Description |
|---|---|
| Doorbell - Delivery Vehicle AI Notification | Fires on three triggers, each handled differently. The parcel box and mailbox contact sensors are treated as near certain deliveries, so those notify unless the AI recognizes a resident collecting items rather than a courier leaving them. A vehicle detection on the Driveway 2 camera is treated as unproven, so it only notifies when the AI positively identifies a delivery. All paths send three frames (driveway wide shot, front porch, and the downward package camera) to LLM Vision on Google Gemini for a structured JSON verdict. The prompt leads with a location rule: carriers never pull into the driveway, they stop on the street, so any vehicle in the driveway is a resident or visitor vehicle and is ignored. It also lists where packages turn up, namely the parcel box, in front of the door, beside the white porch column, and on the sidewalk. Nothing is written to the timeline automatically; only a passing verdict creates an LLM Vision event labeled Package and pushes a notification to the Pixel. |
| NFC - Bedside Lamps Toggle | Toggles bedside lamps on/off. Located under C-table top. |
| NFC - Closet Deadbolt Toggle | NFC tag toggles closet door deadbolt. Located underneath the closet light switch faceplate on the top. |
| NFC - Front Door Deadbolt is scanned |  |
| NFC - Front Door Deadbolt Toggle | NFC tag toggles front door deadbolt. Located ? |
| NFC - Garbage Can is scanned |  |
| NFC - HVAC filter change reset |  |
| NFC - Laundry Room Door Deadbolt is scanned |  |
| NFC - Laundry Room Door Deadbolt Toggle | NFC tag toggles Laundry Room Door Deadbolt. Located ? |
| NFC - Rear Door Deadbolt is scanned |  |
| NFC - Sunroom Door Deadbolt is scanned |  |
| NFC - Toggle Garage Door from Keypad | When NFC tag is scanned, open/close garage door. Located in keypad on garage door frame. |
| NFC - Toggle Garage Door from Truck | NFC tag on dashboard will toggle garage door and lock/unlock laundry room door with failsafe notification. |
