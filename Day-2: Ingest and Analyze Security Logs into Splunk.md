# Day#2: Ingest and Analyze Security Logs into Splunk

---

## 🎯 Objective

In this lab, I:
- Learnt how to ingest and analyze SSH logs using Splunk.
- Detected failed and successful SSH authentication attempts.
- Identified unusual SSH activity that may indicate brute force or unauthorized access.

---

## 🖥️ Lab Setup

- ✅ **Splunk**: Already installed and accessible.
- ✅ **Data Source**: JSON-formatted Zeek-style SSH logs.
- 🌐 **Log File**: Download and upload to Splunk using the steps below.

📥 **[Download SSH Log file](https://raw.githubusercontent.com/0xrajneesh/30-Days-SOC-Challenge-Beginner/refs/heads/main/ssh_logs.json)**

---

## ⚙️ Steps to Upload SSH Log into Splunk

1. Go to Splunk Web → **Settings > Add Data**.
2. Choose **Upload** and select `ssh_logs.json`.
3. Set Source type: `json`.
4. Index: Choose `main`.
5. Finish the upload and confirm indexing.

---

## 🔍 Lab Tasks

Use SPL queries to complete the following analysis:

### ✅Task 1: List the top 10 endpoints with failed SSH login attempts
```spl
source="ssh_logs.json" index="main" sourcetype="json" auth_success=false
| stats count by "id.orig_h"
| sort -count
| head 10
```
### ✅Task 2: Find the number of total SSH connections
```spl
source="ssh_logs.json" index="main" sourcetype="json"
| stats count as total_ssh_connections
```
### ✅Task 3: Count all event types (successful, failed, no-auth, multiple-failed) seen in the logs
```spl
source="ssh_logs.json" index="main" sourcetype="json"
| stats count by event_type
```

## 📸Submission
<p align="center">
<img src="https://raw.githubusercontent.com/WWambui/Splunk-SIEM-Challenge/main/images/day2Task1.png" width="750"/>
<img src="https://raw.githubusercontent.com/WWambui/Splunk-SIEM-Challenge/main/images/day2Task2.png" width="750"/>
<img src="https://raw.githubusercontent.com/WWambui/Splunk-SIEM-Challenge/main/images/day2Task3.png" width="750"/>
</p>
