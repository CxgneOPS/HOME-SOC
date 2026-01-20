## Technique
Credential Access

## Observed Behavior
- Background monitoring of keyboard input
- User-mode execution
- No visible user interface
- Continuous runtime

## Common API References (Defensive Context)
- `SetWindowsHookEx`
- `GetAsyncKeyState`
- `GetKeyState`
- `GetMessage`
- `PeekMessage`

## Detection Notes
- Long-running background process
- Repeated input-related API usage
- Often paired with persistence techniques
- Difficult to detect without correlation

## Defensive Takeaway
Input capture alone is subtle.  
Detection becomes reliable when combined with persistence and execution context.
