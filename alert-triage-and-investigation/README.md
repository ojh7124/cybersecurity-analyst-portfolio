# Summary 

* This directory contains individual alert triage and investigations of tickets in Jira, using Microsoft Sentinel.
* Each markdown file acts as an independent case study demonstrating...

---

## Lab Architecture & Environment

```text

+---------------------------------------------------------------------------+
|                     Virtual Lab Network (Host Laptop)                     |
|                                                                           |
|                          +---------------------+                          |
|                          |      RedTeam-01     |                          |
|                          |    (Attacker VM)    |                          |
|                          |   Atomic Red Team   |                          |
|                          |       IP: TBC       |                          |
|                          +----------+----------+                          |
|                                     | Simulated Attacks                   |
|               +---------------------+---------------------+               |
|               |                                           |               |
|               v                                           v               |
|    +---------------------+                     +---------------------+    |
|    |        DC-01        |                     |      Client-01      |    |
|    |     (AD Server)     |                     |     (Client VM)     |    |
|    |    Users + Depts    |                     |  Corporate Endpoint |    |
|    |    192.168.252.10   |                     |    192.168.252.20   |    |
|    +----------+----------+                     +----------+----------+    |
|               |                                           |               |
|               +---------------------+---------------------+               |
|                                     | Windows Event + Sysmon Logs         |
+-------------------------------------+-------------------------------------+
                                      |
                                      v
                +-------------------------------------------+
                |              Microsoft Azure              |
                |                                           |
                |    +---------------------------------+    |
                |    |     Log Analytics Workspace     |    |
                |    |         (Log Ingestion)         |    |
                |    +---------------------------------+    |
                |                     |                     |
                |                     v                     |
                |    +---------------------------------+    |
                |    |        Microsoft Sentinel       |    |
                |    |    (Analytic Rules + Alerts)    |    |
                |    +---------------------------------+    |
                |                     | Automation Rule     |
                |                     v                     |
                |    +---------------------------------+    |
                |    |        Logic App Playbook       |    |
                |    |    (Builds Documented Ticket)   |    |
                |    +---------------------------------+    |
                |                                           |
                +-------------------------------------------+
                                      | Ticket Created
                                      v
                     +---------------------------------+
                     |               Jira              |
                     |         (Alert Tickets)         |
                     +---------------------------------+
