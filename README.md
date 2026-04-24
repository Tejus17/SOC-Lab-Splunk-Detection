# 🛡️ Splunk SOC Lab – Brute Force Detection

##  About this project

I built a small SOC (Security Operations Center) lab using Splunk to understand how logs are collected and how attacks can be detected.

The main goal was to detect **failed login attempts (brute force attacks)** using Windows Event Logs.

---

##  What I set up

* Installed Splunk Enterprise on my PC
* Installed Splunk Universal Forwarder on another Windows laptop
* Connected both systems over the same network
* Enabled Windows Event Logs (Security + System)

---

##  Challenges I faced

* Forwarder was not connecting (network issue)
* Splunk service permission errors
* Logs were not appearing due to wrong config file (`inputs.conf.txt`)
* Queries not working because of wrong field names

Fixing these helped me understand how real troubleshooting works.

---

##  What I tested

### 1. Failed login attempts

I manually entered the wrong password multiple times on the Windows laptop to generate logs.

### 2. (Optional) Network scan

I used Kali Linux to run a basic Nmap scan just to simulate attacker behavior.

---

##  Detection in Splunk

### Basic search

```spl id="jz2n8v"
index=* (EventCode=4625 OR EventID=4625)
```

---

### Count of failed logins

```spl id="t1q3xo"
index=* (EventCode=4625 OR EventID=4625)
| stats count by host
```

---

### Activity over time

```spl id="c0a7l9"
index=* (EventCode=4625 OR EventID=4625)
| timechart count
```

---

##  What I observed

* Multiple failed login attempts were clearly visible
* I could see how frequently they were happening
* The timeline graph helped understand attack patterns

---

##  Dashboard

I created a simple dashboard with:

* Failed logins by host
* Login attempts over time

(Screenshots are in the /screenshots folder)

---

##  What I learned

* How SIEM tools like Splunk work
* How logs are collected and analyzed
* Basics of detecting brute-force attacks
* Importance of correct configuration and troubleshooting

---

##  Conclusion

This project helped me understand how real SOC analysts monitor systems and detect suspicious activity using logs.

---

##  Resume point

Built a SOC lab using Splunk to detect brute-force login attempts (Event ID 4625) and visualize activity using dashboards.
