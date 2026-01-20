## Technique
Defense Evasion

## Observed Behavior
- Legitimate-looking process names
- Names resembling system utilities
- Execution from non-standard directories

## Related API Context
- `GetForegroundWindow`
- `GetWindowText`
- `GetWindowThreadProcessId`

## Detection Notes
- Process name does not match execution path
- Unsigned binaries posing as system tools
- Behavioral mismatch with expected process role

## Defensive Takeaway
Masquerading increases dwell time but is often exposed through path and signature analysis.
