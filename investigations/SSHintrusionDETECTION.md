## Executive Summary

A simulated attack was conducted from a Kali Linux host against an Ubuntu server monitored by Wazuh. The objective was to evaluate the effectiveness of existing detections for reconnaissance activity, authentication failures, brute-force attempts, and successful SSH access.

The exercise successfully generated authentication failure alerts, brute-force detections, and successful SSH login events. However, reconnaissance activity and post-authentication command execution were not detected, revealing visibility gaps within the current monitoring configuration.

---

## Results

### Successful Detections

- SSH authentication failures
- Repeated password guessing activity
- Successful SSH authentication
- Source IP attribution for successful access

### Detection Gaps

- Host discovery
- Port scanning
- Service enumeration
- Post-authentication command execution

---

## Scenario

An external host was suspected of attempting unauthorized SSH access to a Linux server.

### Analyst Objectives

- Identify reconnaissance activity
- Identify authentication failures
- Determine if access was obtained
- Evaluate visibility gaps in current monitoring

---

## Environment

### Attacker

| Field | Value |
|---------|---------|
| Hostname | CXattack |
| IP Address | 192.168.56.20 |
| Operating System | Kali Linux |

### Target

| Field | Value |
|---------|---------|
| Hostname | cxsoc |
| IP Address | 192.168.56.10 |
| Operating System | Ubuntu Linux |

### Monitoring

| Field | Value |
|---------|---------|
| Platform | Wazuh |
| Version | 4.14.5 |

---

## Attack Timeline

| Step | Activity | Detection Status |
|--------|------------|------------------|
| 1 | Host Discovery | ❌ Not Detected |
| 2 | Port Scanning | ❌ Not Detected |
| 3 | Service Enumeration | ❌ Not Detected |
| 4 | Failed SSH Authentication Attempts | ✅ Detected |
| 5 | Brute Force Activity | ✅ Detected |
| 6 | Successful SSH Authentication | ✅ Detected |
| 7 | Post-Authentication Activity | ❌ Not Detected |

---

## Detection Analysis

### Reconnaissance

#### Evidence

- Host discovery performed against target
- Port scan conducted
- Service enumeration performed

#### Findings

| Service | Port | Status |
|----------|------|---------|
| SSH | TCP/22 | Open |
| HTTPS | TCP/443 | Open |

##### Service Identification

- OpenSSH identified on TCP/22

#### Detection

No alerts were generated during the reconnaissance phase.

##### Visibility Gap

Reconnaissance activity was successfully performed against the target without generating detections in Wazuh.

---

### Authentication Attempts

#### Evidence

- Failed login attempt for `root`
- Failed login attempt for `admin`
- Failed login attempt for `wazuh`
- Multiple failed password attempts observed

#### Detection

| Rule ID | Description |
|----------|-------------|
| 5760 | SSH authentication failure |
| 5710 | Multiple authentication failures |
| 2502 | Linux authentication failure |

#### MITRE ATT&CK

| Technique | ID |
|------------|------|
| Password Guessing | T1110.001 |

#### Assessment

Wazuh successfully detected failed authentication attempts and generated alerts associated with SSH login failures. Correlation rules provided visibility into repeated password-guessing behavior.

**Detection Status:** ✅ Successful

---

### Successful Access

#### Evidence

- Accepted password for `cxsoc-admin`
- Source IP: `192.168.56.20`

#### Detection

| Rule ID | Description |
|----------|-------------|
| 100001 | Successful SSH Login Detected |

#### MITRE ATT&CK

| Technique | ID |
|------------|------|
| Valid Accounts | T1078 |

#### Assessment

Wazuh successfully detected the successful SSH login event and captured the originating source IP address, confirming that access to the target system was obtained.

**Detection Status:** ✅ Successful

---

## Findings

### Successful Detections

The monitoring stack successfully detected multiple stages of the SSH attack lifecycle, including:

- Failed SSH authentication attempts
- Repeated password guessing activity
- Successful SSH authentication
- Source IP attribution for successful access

### Detection Gaps

The following attacker activities were not detected during testing:

- Nmap host discovery
- Port scanning activity
- Service enumeration
- Post-authentication command execution

These gaps limit visibility into both the reconnaissance phase and attacker actions following initial access.

---

## Recommendations

1. Deploy `auditd` to provide command execution and process monitoring on Linux systems.
2. Implement network monitoring solutions such as Zeek or Suricata to detect reconnaissance activity.
3. Expand custom Wazuh SSH detection rules to improve alert fidelity and coverage.
4. Improve post-authentication visibility through enhanced auditing and process telemetry.
5. Consider automated response actions such as temporary IP blocking after excessive authentication failures.

---

## Conclusion

The monitoring stack successfully detected authentication-related activity, including failed login attempts, brute-force behavior, and successful SSH access. However, significant visibility gaps remain in detecting reconnaissance activity and post-authentication actions.

Future improvements should focus on expanding Linux auditing capabilities and incorporating network-based monitoring solutions to provide greater coverage across the attack lifecycle.

---

## Skills Demonstrated

- Security Monitoring
- Wazuh Administration
- Linux Log Analysis
- SSH Investigation
- Threat Detection
- Detection Engineering
- Incident Analysis
- MITRE ATT&CK Mapping
- Security Operations (SOC)

---

## Tools Used

- Wazuh 4.14.5
- Ubuntu Linux
- Kali Linux
- OpenSSH
- VirtualBox
- Nmap

---

## Future Enhancements

- Deploy auditd for Linux process visibility
- Add Zeek for network telemetry
- Add Suricata IDS monitoring
- Create custom reconnaissance detection rules
- Build ATT&CK-aligned dashboards
- Validate detections for privilege escalation techniques
- Expand testing to persistence and lateral movement scenarios
