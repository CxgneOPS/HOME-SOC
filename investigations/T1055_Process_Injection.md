## Technique
Defense Evasion / Privilege Escalation

## Scope Note
This technique is referenced for detection awareness only.  
No process injection is demonstrated in this project.

## Observed Behavior
- Suspicious parent-child process relationships
- Unexpected memory access patterns
- Execution within trusted processes

## Detection Notes
- EDR memory access alerts
- Process ancestry anomalies
- Deviation from known-good baselines

## Defensive Takeaway
Process injection is detectable through memory and lineage telemetry when proper monitoring is enabled.
