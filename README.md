# Purple-team-ad-lab
Pentesting against Windows Active Directory and analyzing IOC's
plunk Purple Team AD Homelab (Setup)
Overview

This repository documents my Splunk purple team homelab environment. The goal is to simulate common attack behavior in a safe lab and validate detections using Windows telemetry in Splunk.

Lab Components

Domain Controller (Windows Server): AD DS + DNS, Sysmon enabled, Windows Event Logs shipped to Splunk

Workstations (Windows Enterprise x2): Sysmon enabled, Windows Event Logs shipped to Splunk

Splunk Server (Ubuntu): Splunk Enterprise (Search Head + Indexing)

Kali Linux: lab-only testing / validation

Logging Pipeline

Sysmon + Windows Event Logs → Splunk Universal Forwarder → Splunk Receiver (TCP 9997) → dashboards/detections (future work)

Network Topology




Proof of Ingestion (Screenshots)

Sysmon index created

screenshots/splunk-sysmon-index.png

Sysmon events arriving from hosts

screenshots/splunk-sysmon-events.png

Windows Security log events arriving (logons)

screenshots/splunk-security-events.png

Notes / Tuning

Sysmon is tuned to reduce noise (ex: excluding Splunk Universal Forwarder binaries from ProcessCreate where appropriate).

This repo is currently documenting setup. Detections, dashboards, and incident writeups will be added next.
