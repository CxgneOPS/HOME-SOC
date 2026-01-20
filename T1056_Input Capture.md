# T1056.001 – Input Capture: Keylogging

## Technique
Credential Access

## Behavior Observed
- Background keyboard monitoring
- User-mode execution
- No visible UI

## Common API References (Defensive Context)
- `SetWindowsHookEx`
- `GetAsyncKeyState`
- `GetKeyState`
- `GetMessage`, `PeekMessage`

## Detection Notes
- Long-running background process
- Repeated input API activity
- Often paired with persistence

## Defensive Takeaway
Input capture alone is subtle. Correlated behavior enables detection.
