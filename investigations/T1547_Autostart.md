## Technique
Persistence

## Observed Behavior
- Execution across system reboots
- Execution on user logon
- Persistence created shortly after initial execution

## Common Autostart Locations
- Registry Run keys
- Scheduled tasks
- Startup folder entries

## Detection Notes
- Event ID 4698 (Scheduled task creation)
- Event ID 4657 (Registry modification)
- User-level persistence is high-signal
- Persistence is often louder than payload activity

## Defensive Takeaway
Persistence mechanisms are frequently the most reliable detection point for keylogging activity.
