# Investigation 01: Initial Access via Brute Force 

## Executive Summary
This investigation analyzes a successful authentication attack targeting a local account (`HelpDesk_User`) over Server Message Block (SMB / Port 445). Telemetry reveals a sequence of rapid failed logon attempts immediately followed by a successful authentication event, indicating a successful credential brute-force attack.

---

## 1. Hypothesis
* If a brute-force attack occurred, I expect to see multiple rapid failed logon events (`4625`) originating from a single source IP, followed by a successful logon (`4624`) once the correct password was discovered.

---

## 2. SPL Query

` ` `
index=* (EventCode=4625 OR EventCode=4624) "HelpDesk_User" | sort _time | table _time, Source_Network_Address, EventCode, Account_Name, Account_Domain, Logon_Type, Logon_Process, Sub_Status
` ` `

<img width="1920" height="670" alt="Screenshot (1)" src="https://github.com/user-attachments/assets/034a5cbe-2cdc-438f-b154-45a380cae2ba" />

---

## 3. Key Artifacts & IOCs

* **Target Account:** `HelpDesk_User`
* **Source IP:** `192.168.71.1`
* **EventCode Pattern:** 3x Event Code `4625` (Failed Logon) within a 4-second window, followed immediately at `17:55:35` by Event Code `4624` (Successful Logon).
* **Logon Type:** `3` (Network Logon). This confirms the authentication occurred remotely over SMB (Port 445).

---

## 4. Conclusion

* **Verdict:** True Positive
* **Severity:** High
* **Framework Mapping:** MITRE ATT&CK T1110.001 (Brute Force: Password Guessing)
* **Summary:** Validated successful brute force attack against local account `HelpDesk_User` originating from IP `192.168.71.1` via SMB (Port 445).
