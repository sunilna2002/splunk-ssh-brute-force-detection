#🔐 SSH Brute-Force Detection with Splunk

## Project Overview
This project simulates a real-world security incident where an attacker performs an SSH brute-force attack against a Linux server. Using Splunk, I ingested authentication logs, identified the malicious activity, and created a monitoring dashboard.

## Key Skills Demonstrated
✔️ Splunk Search Processing Language (SPL)
✔️ Threat hunting and investigation
✔️ Dashboard creation and visualization
✔️ Log analysis and pattern detection
✔️MITRE ATT&CK framework mapping

## Attack Scenario
- **Attacker IP:** 203.0.113.45
- **Attack Type:** SSH brute-force (150+ failed attempts)
- **Target:** root user account
- **Duration:** ~2 hours on May 17, 2025
- **Result:** Attack failed; no successful breach

## MITRE ATT&CK Mapping
| Tactic | Technique |
|--------|-----------|
| Credential Access | T1110 - Brute Force |
| Discovery | T1046 - Network Service Scanning |

## Sample Searches Used

### Identify brute-force source
```bash
index=simulated "Failed password"
| rex "Failed password for \S+ from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
| where count > 50
```

### Attack timeline
```bash
index=simulated src_ip=203.0.113.45 "Failed password"
| timechart count
```

## Dashboard Panels
1. **Top 10 Attacking IPs** - Bar chart showing attacker with 150 attempts
2. **Attack Timeline** - Line chart showing attack concentration
3. **Most Targeted Usernames** - Pie chart showing root as primary target
4. **Successful Logins** - Baseline normal activity table

## How to Reproduce
1. Install Splunk (Free or Enterprise trial)
2. Create a script `log_generator.py` to create simulated attack log file named auth.log (On Ubuntu using Python Env)
3. Ingest auth.log into Splunk with sourcetype `linux_secure`
4. Import the dashboard or run the SPL queries

## Tools Used
- Splunk Enterprise (Free Trial)
- Python 3 (log generation)
- Ubuntu (WSL)

## Screenshots
![Dashboard](https://github.com/sunilna2002/splunk-ssh-brute-force-detection/blob/main/splunk_assets/TOP%20FAILED%20ATTEMPT.png)
![](https://github.com/sunilna2002/splunk-ssh-brute-force-detection/blob/main/splunk_assets/Time-wise%20Top%20Failed.png)

## Investigation Report
See [full report](https://github.com/sunilna2002/splunk-ssh-brute-force-detection/blob/main/splunk_assets/SSH%20Brute%20Report.pdf)

## Author
Sunil Rajpal- Google Cybersecurity Certification

## Date
21 May 2025
