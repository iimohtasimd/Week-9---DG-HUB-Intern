# 🔐 Week 9 — SOC Introduction & Snort IDS

## DG Interns Hub — Cyber Security Internship

This project was completed as part of **Week 9: SOC Introduction & Setup** of the DG Interns Hub Cyber Security Internship.

The objective of this project was to understand the fundamentals of a **Security Operations Center (SOC)** and build a basic network monitoring environment using **Snort Intrusion Detection System (IDS)**.

The lab uses **Kali Linux as the Snort sensor and traffic source** and **Metasploitable 2 as the intentionally vulnerable target** inside an isolated VirtualBox host-only network.

---

## 🎯 Objectives

The main objectives of this project were:

- Understand the fundamentals of a Security Operations Center (SOC)
- Understand L1, L2 and L3 SOC analyst roles
- Understand the difference between:
  - IDS
  - IPS
  - SIEM
- Configure a Linux-based monitoring environment
- Configure a host-only lab network
- Install and verify Snort IDS
- Test the Snort configuration
- Understand Snort rule structure
- Create custom ICMP and HTTP detection rules
- Generate test traffic
- Capture and analyze Snort alerts
- Document the complete lab with screenshots and reports

The report describes the project as a minimal monitoring setup focused on the preparation and detection stages of the incident lifecycle.

---

## 🏗️ Lab Architecture

```text
                 Internet
                    │
                 NAT Adapter
                    │
              ┌──────────────┐
              │  Kali Linux  │
              │              │
              │ Snort IDS    │
              │ Traffic Src │
              └──────┬───────┘
                     │
              Host-Only Network
               192.168.56.0/24
                     │
              ┌──────┴────────┐
              │ Metasploitable│
              │      2        │
              │ Apache Server  │
              └───────────────┘
```

### Components

| Component | Role |
|---|---|
| Kali Linux | Snort sensor and traffic source |
| Snort | Intrusion Detection System |
| Metasploitable 2 | Intentionally vulnerable target |
| VirtualBox | Virtualization platform |
| Host-only Network | Isolated lab communication |

The target is intentionally kept on the host-only network and is not connected through NAT or bridged networking.

---

## 🖥️ Environment

### Kali Linux

Kali Linux was used as the monitoring platform and Snort sensor.

The machine was configured with:

- NAT adapter for updates
- Host-only adapter for lab traffic
- Hostname: `soc-kali01`
- Host-only network: `192.168.56.0/24`

### Metasploitable 2

Metasploitable 2 was used as the target machine.

It was configured with:

- Existing `.vmdk` hard disk
- Host-only networking
- Apache web server
- Isolated lab environment

The project uses Metasploitable 2 because it provides a realistic web server and network services for generating safe test traffic.

---

# 🧠 SOC Fundamentals

## What is a SOC?

A **Security Operations Center (SOC)** is a combination of people, processes and technology responsible for continuously monitoring systems, detecting security events, investigating suspicious activity and coordinating response.

The SOC workflow used in this project can be summarized as:

```text
Monitoring
     ↓
Detection
     ↓
Triage
     ↓
Response
     ↓
Improvement
```

---

## 👨‍💻 SOC Analyst Roles

### L1 Analyst — Triage

The L1 analyst performs the initial investigation of alerts.

Typical activities include:

- Reviewing alerts
- Checking known-benign activity
- Gathering source and destination information
- Closing false positives
- Creating tickets for genuine events

### L2 Analyst — Incident Responder

The L2 analyst performs deeper investigation.

Typical activities include:

- Correlating logs
- Investigating affected hosts
- Determining incident scope
- Recommending containment
- Tuning detection rules

### L3 Analyst — Senior Analyst / Threat Hunter

The L3 analyst handles advanced security investigations.

Typical activities include:

- Threat hunting
- Malware analysis
- Digital forensics
- Detection engineering
- Post-incident analysis
- Mentoring L1 and L2 analysts

---

# 🛡️ IDS vs IPS vs SIEM

| Technology | Purpose |
|---|---|
| **IDS** | Detects suspicious activity and generates alerts |
| **IPS** | Detects suspicious activity and can block traffic |
| **SIEM** | Collects, normalizes and correlates security logs from multiple sources |

In this project
