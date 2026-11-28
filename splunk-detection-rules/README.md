# Summary 

* This directory contains individual detection rules using Splunk.
* Each markdown file acts as an independent case study demonstrating detection engineering, rule deployment, alert configuration, and validation. 

---

## Lab Architecture & Environment

```text

+-------------------------------------------------------------+
|              Virtual Lab Network (Host Laptop)              |
|                                                             |
|                   +---------------------+                   |
|                   |      Kali Linux     |                   |
|                   |    (Attacker VM)    |                   |
|                   |     192.168.71.1    |                   |
|                   +----------+----------+                   |
|                              | Simulated Attacks             |
|                              v                              |
|                   +---------------------+                   |
|                   |      Windows 11     |                   |
|                   |     (Target VM)     |                   |
|                   |    192.168.71.128   |                   |
|                   +----------+----------+                   |
|                              | Windows Event + Sysmon Logs  |
|                              v                              |
|                   +---------------------+                   |
|                   |  Splunk Enterprise  |                   |
|                   |   (Log Ingestion)   |                   |
|                   +---------------------+                   |
|                                                             |
+-------------------------------------------------------------+
