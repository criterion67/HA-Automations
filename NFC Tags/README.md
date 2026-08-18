# NFC Tags

13 automation(s) in this category.

| Automation | Description |
|---|---|
| Doorbell - Delivery Vehicle AI Notification | Fires on three triggers, each handled differently. The parcel box and mailbox contact sensors are treated as near certain deliveries, so those notify unless the AI recognizes a resident collecting items rather than a courier leaving them. A vehicle detection on the Driveway 2 camera is treated as unproven, so it only notifies when the AI positively identifies a delivery. All paths send three frames (driveway wide shot, front porch, and the downward package camera) to LLM Vision on Google Gemini for a structured JSON verdict. The prompt leads with a location rule: carriers never pull into the driveway, they stop on the street, so any vehicle in the driveway is a resident or visitor vehicle and is ignored. It also lists where packages turn up, namely the parcel box, in front of the door, beside the white porch column, and on the sidewalk. Nothing is written to the timeline automatically; only a passing verdict creates an LLM Vision event labeled Package and pushes a notification to the Pixel. The pushed notification image now follows the trigger: the mailbox and driveway triggers attach the Driveway 2 snapshot, which is the only view that actually shows the mailbox and the street where carriers stop, while the parcel box trigger keeps the front porch snapshot. The title likewise varies by trigger so mail reads as mail rather than as a package. A fourth trigger listens to the UniFi Protect package detection event on the G6 Pro doorbell package camera, which covers the case a courier leaves a box on the porch floor without opening the parcel box and without their vehicle tripping the driveway detector. That trigger ignores the unknown and unavailable states so a restart cannot fire it, is treated as near certain like the parcel box, and attaches a fresh snapshot of the downward package camera. The vision prompt was revised on 2026-08-17 to name image 3 as the authoritative doorstep view when it disagrees with the porch view, and to stop requiring signs of recent activity, since the package detection path often snapshots an empty frame after the courier has already left. A package now counts on presence alone, and resident_retrieving requires a person to actually be visible. |
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
