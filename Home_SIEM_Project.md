# Home SIEM Lab

> A personal cybersecurity home lab focused on collecting, forwarding, analyzing, and responding to security events in a controlled environment.

## Project Status

- **Status:** `Setup In Progress`
- **Started:** `8/11/2026`
- **Primary Goal:** Build and document a functional home Security Information and Event Management (SIEM) environment.
- **SIEM Platform:** `Wazuh`
- **Virtualization Platform:** `VirtualBox`
- **Network Mode:** `Bridged`
- **Author:** `Orlando Flounory`

---

## 1. Project Overview

### Purpose

The purpose of this lab is to demonstrate my ability to learn technical skills, thorough documentation, and experiment with different platforms to better expose myself to the work I may be doing in my career in Cybersecurity. Having prior experience in network monitoring and configuration, I want to highlight my growth in scripting, Windows and Linux terminal applications, and technical documentation for my interest in both Network Engineering and GRC roles.

### Learning Objectives

- [ ] SIEM deployment and administration
- [ ] Log collection and aggregation
- [ ] Windows/Linux endpoint monitoring
- [ ] Network security monitoring
- [ ] Detection engineering
- [ ] Incident investigation
- [ ] Alert triage
- [ ] Basic threat hunting
- [ ] Documentation and reporting
- [ ] `[Additional objective]`

### Success Criteria

The project will be considered complete when:

- [ ] SIEM platform is deployed and accessible
- [ ] At least one Linux endpoint is forwarding logs
- [ ] At least one Windows endpoint is forwarding logs
- [ ] Network/security telemetry is being collected
- [ ] Logs are searchable from a centralized location
- [ ] At least `[X]` detections/alerts are configured
- [ ] At least `[X]` simulated security events have been investigated
- [ ] Findings are documented
- [ ] Final architecture diagram is completed

---

# 2. End-Goal Topology

The following represents the **target architecture** for the completed lab.

```text
                         HOME NETWORK / INTERNET
                                  |
                                  |
                           [Home Router]
                                  |
                                  |
                       +----------+----------+
                       |                     |
                    LAN / VLAN           Management
                       |                     |
          +------------+------------+        |
          |            |            |        |
          |            |            |        |
     [Windows PC]  [Linux VM]   [Other Host] |
          |            |            |        |
          +------------+------------+--------+
                       |
                       |
                [VirtualBox Host]
                       |
        +--------------+--------------+
        |                             |
        |        Virtual Network      |
        |                             |
        +--------------+--------------+
                       |
              +--------+--------+
              |                 |
              |                 |
        [SIEM Server]      [Log/Agent Hosts]
              |                 |
              |                 |
        +-----+-----+     +-----+-----+
        |           |     |           |
    Dashboard   Detection  Agents    Syslog
                Engine
              |
              |
        [Security Alerts]
              |
              v
       [Investigation / Response]
```

> **Note:** Will replace this topology with a more detailed diagram as the project develops.

### Planned Components

| Component | Role | OS | IP Address | Status |
|---|---|---|---|---|
| SIEM Server | Central log collection/analysis | `Wazuh` | `[IP]` | `Planned` |
| Windows Endpoint | Endpoint telemetry | Windows | `10.0.0.108` | `Planned` |
| Linux Endpoint | Linux telemetry | Ubuntu | `10.0.0.124` | `Planned` |
| Network Device | Network/security logs | `VirtualBox Host-Only Ethernet Adapter` | `192.168.56.1` | `Planned` |
| VirtualBox Host | Virtualization | `Ubuntu 25.04` | `10.0.0.124` | `Planned` |
| `[Additional Host]` | `[Role]` | `[OS]` | `[IP]` | `Planned` |

---

# 3. Network Design

## Network Configuration

- **Network Type:** Bridged Adapter
- **Network/Subnet:** `10.0.0.1/24`
- **Gateway:** `10.0.0.1`
- **DNS:** `75.75.75.75`
- **SIEM IP:** `[IP]`
- **Windows Endpoint IP:** `10.0.0.108`
- **Linux Endpoint IP:** `10.0.0.124`

### IP Address Plan

```text
Network: [Network/CIDR]

Gateway:       [IP]
SIEM Server:   [IP]
Windows Host:  [IP]
Linux Host:    [IP]
Other:         [IP]
```

### Connectivity Tests

- [ ] SIEM can reach gateway
- [ ] SIEM can reach Windows endpoint
- [ ] SIEM can reach Linux endpoint
- [ ] Endpoints can reach SIEM
- [ ] DNS resolution works
- [ ] Internet connectivity works where required
- [ ] Required SIEM ports are reachable

---

# 4. SIEM Platform

## Platform

**Selected SIEM:** `Wazuh`

### Version

`[Version]`

### Installation Method

`[VM / Docker / Bare Metal / Other]`

### VM Specifications

| Resource | Allocation |
|---|---:|
| vCPU | `2` |
| RAM | `8192 MB` |
| Storage | `40 GB` |
| Network Adapter | `Intel PRO/1000 MT Desktop (Bridged Adapter, Intel(R) Wi-Fi 6 AX200 160 MHz)` |
| OS | `Ubuntu 25.04 (Plucky Puffin) (64b-bit)` |

### Installation Notes

Configurations decisions were based on recommended prerequisites to run Wazuh Agent on the VM.

---

# 5. Log Sources

## Linux

**Host:** `[Hostname]`

Potential telemetry:

- `/var/log/auth.log`
- `/var/log/syslog`
- SSH authentication events
- Sudo activity
- User account changes
- Process activity
- `[Other]`

### Configuration

[Document how Linux logs are forwarded to the SIEM.]

---

## Windows

**Host:** `[Hostname]`

Potential telemetry:

- Windows Security Event Log
- System Event Log
- Application Event Log
- PowerShell logs
- Windows Defender events
- Authentication events
- Account management events
- `[Other]`

### Configuration

[Document the agent, configuration, event channels, and forwarding process.]

---

## Network Telemetry

Potential sources:

- Router logs
- Firewall logs
- DNS logs
- DHCP logs
- IDS/IPS logs
- Network flow data
- `[Other]`

### Configuration

[Document how network telemetry enters the SIEM.]

---

# 6. Data Flow

Document the path logs take from the source to the SIEM.

```text
[Endpoint]
    |
    | Logs / Events
    v
[Agent / Forwarder]
    |
    | Network
    v
[SIEM Collector]
    |
    v
[Parsing / Normalization]
    |
    v
[Search / Detection]
    |
    v
[Alert]
    |
    v
[Investigation]
```

### Data Flow Notes

[Explain which agents/forwarders are used and how data is processed.]

---

# 7. Detection Engineering

## Initial Detection Goals

Create detections for common security events.

| Detection | Data Source | Trigger | Severity | Status |
|---|---|---|---|---|
| Multiple failed logins | `[Source]` | `[Condition]` | Medium | Planned |
| Successful login after failures | `[Source]` | `[Condition]` | High | Planned |
| New user account | `[Source]` | `[Condition]` | Medium | Planned |
| Privilege escalation | `[Source]` | `[Condition]` | High | Planned |
| Suspicious PowerShell | `[Source]` | `[Condition]` | High | Planned |
| SSH brute force | `[Source]` | `[Condition]` | High | Planned |
| `[Custom Detection]` | `[Source]` | `[Condition]` | `[Severity]` | Planned |

### Detection Documentation Template

#### `[Detection Name]`

**Objective:**

[What behavior does this detection identify?]

**Data Source:**

`[Windows / Linux / Network / Other]`

**Detection Logic:**

`[Query / Rule / Logic]`

**Expected Result:**

[What should happen when the detection triggers?]

**False Positives:**

[Document expected benign activity.]

**MITRE ATT&CK Mapping:**

`[Technique / Sub-technique]`

---

# 8. Attack Simulation / Testing

Only perform simulations against systems you own or are explicitly authorized to test.

## Test 1 — Failed Authentication

**Objective:** Generate multiple failed authentication events.

- **Source:** `[Host]`
- **Method:** `[Method]`
- **Expected Log:** `[Event ID / Log Entry]`
- **Expected Alert:** `[Alert]`
- **Result:** `[Pass/Fail]`
- **Notes:** `[Notes]`

## Test 2 — New User

**Objective:** Generate a new local user account event.

- **Source:** `[Host]`
- **Method:** `[Method]`
- **Expected Log:** `[Event ID / Log Entry]`
- **Expected Alert:** `[Alert]`
- **Result:** `[Pass/Fail]`
- **Notes:** `[Notes]`

## Test 3 — Privilege Change

**Objective:** Generate an administrative privilege change.

- **Source:** `[Host]`
- **Method:** `[Method]`
- **Expected Log:** `[Event ID / Log Entry]`
- **Expected Alert:** `[Alert]`
- **Result:** `[Pass/Fail]`
- **Notes:** `[Notes]`

## Additional Tests

- [ ] `[Test]`
- [ ] `[Test]`
- [ ] `[Test]`

---

# 9. Incident Investigation

Use this section to document investigations generated by the lab.

## Incident `[ID]`

**Date:** `[YYYY-MM-DD]`

**Alert:** `[Alert Name]`

**Severity:** `[Low / Medium / High / Critical]`

**Affected Host:** `[Hostname/IP]`

### Initial Observation

[What initially triggered the investigation?]

### Timeline

| Time | Event | Source | Significance |
|---|---|---|---|
| `[Time]` | `[Event]` | `[Source]` | `[Why it matters]` |
| `[Time]` | `[Event]` | `[Source]` | `[Why it matters]` |

### Investigation

[Describe the queries, logs, and evidence reviewed.]

### Findings

[What happened?]

### Response

[What action was taken?]

### Lessons Learned

[What did you learn or change?]

---

# 10. Dashboards

## Dashboard 1 — Security Overview

Planned panels:

- [ ] Events over time
- [ ] Authentication failures
- [ ] Authentication successes
- [ ] Top source IPs
- [ ] Top affected hosts
- [ ] Alerts by severity
- [ ] Alerts by detection
- [ ] `[Additional panel]`

## Dashboard 2 — Windows Security

- [ ] Failed logins
- [ ] Successful logins
- [ ] Account changes
- [ ] PowerShell activity
- [ ] Privilege changes
- [ ] `[Additional panel]`

## Dashboard 3 — Linux Security

- [ ] SSH activity
- [ ] Failed authentication
- [ ] Sudo activity
- [ ] User changes
- [ ] `[Additional panel]`

---

# 11. Automation

Document automation used to improve the lab.

### Automation `[Name]`

**Purpose:**

[What repetitive task does this automate?]

**Technology:**

`[Python / PowerShell / Bash / API / Other]`

**Input:**

`[Input]`

**Output:**

`[Output]`

**Status:**

`[Planned / In Progress / Complete]`

---

# 12. Troubleshooting Log

| Date | Problem | Investigation | Solution | Lesson |
|---|---|---|---|---|
| `[Date]` | `[Problem]` | `[What you checked]` | `[Fix]` | `[Lesson]` |
| `[Date]` | `[Problem]` | `[What you checked]` | `[Fix]` | `[Lesson]` |

---

# 13. Security Considerations

- [ ] Credentials are not stored in Git
- [ ] Secrets are stored securely
- [ ] Management interfaces are restricted
- [ ] Firewall rules are documented
- [ ] Lab systems are isolated appropriately
- [ ] Only authorized systems are tested
- [ ] Logs do not expose unnecessary sensitive information
- [ ] Backups are configured where appropriate

---

# 14. Project Milestones

- [ ] **Milestone 1:** VirtualBox networking configured
- [ ] **Milestone 2:** SIEM server deployed
- [ ] **Milestone 3:** Linux endpoint connected
- [ ] **Milestone 4:** Windows endpoint connected
- [ ] **Milestone 5:** Log ingestion verified
- [ ] **Milestone 6:** Initial detections created
- [ ] **Milestone 7:** Attack simulations performed
- [ ] **Milestone 8:** Investigations documented
- [ ] **Milestone 9:** Dashboards created
- [ ] **Milestone 10:** Final architecture documented

---

# 15. Skills Demonstrated

Update this section as the project progresses.

- `SIEM Administration`
- `Log Management`
- `Security Monitoring`
- `Detection Engineering`
- `Incident Response`
- `Threat Hunting`
- `Windows Security`
- `Linux Security`
- `Network Security`
- `Virtualization`
- `[Skill]`
- `[Skill]`

---

# 16. Final Project Summary

### What I Built

[Write a concise summary of the completed environment.]

### Technologies Used

`[Technology]` · `[Technology]` · `[Technology]`

### Key Accomplishments

- [Accomplishment]
- [Accomplishment]
- [Accomplishment]

### Biggest Challenge

1. Working with VirtualBox was a learning curve from working with VMWare from undergraduate courses. It took me a while to understand how to configure the Ubuntu VM and to know why certain settings were applied.


### What I Learned

[Summarize the most important technical lessons.]

### Future Improvements

- [ ] `[Improvement]`
- [ ] `[Improvement]`
- [ ] `[Improvement]`

---

## Project Links

- **GitHub Repository:** `[Link]`
- **Architecture Diagram:** `[Link]`
- **Documentation:** `[Link]`
- **Demo:** `[Link]`
- **Portfolio Page:** `[Link]`
