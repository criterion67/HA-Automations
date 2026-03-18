# Locks & Security

**Hardware:** 5x Wyze Lock (Zigbee via SLZB-06), 1x Tuya Zigbee siren

> Migrated from Wyze cloud to Zigbee2MQTT in March 2026. Entity IDs preserved, zero automation edits required.

| File | Description |
|------|-------------|
| `front_door_lock_*.yaml` | Front door lock/unlock notifications and NFC control. |
| `rear_door_lock_*.yaml` | Rear door lock/unlock notifications. |
| `sunroom_door_lock_*.yaml` | Sunroom door lock state notifications. |
| `laundry_room_door_lock_*.yaml` | Laundry room lock automations. |
| `bedroom_closet_door_lock_*.yaml` | Bedroom closet lock automations. |
| `zigbee_siren_*.yaml` | Security-triggered siren. Duration, volume, ringtone via ZHA. |
