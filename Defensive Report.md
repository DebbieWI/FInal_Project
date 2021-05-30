# Blue Team: Summary of Operations
## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior


 ### Network Topology
The following machines were identified on the network:
- Name of Hypervisor / Host Machine
  - Operating System:Microsoft Windows
  - Purpose: Hypervisor / Gateway
  - IP Address: 192.168.1.1
- Name of ELK
  - Operating System:Linux
  - Purpose: Elasticsearch, Logstash, Kibana Server
  - IP Address: 192.168.1.100
- Name of Capstone
  - Operating System: Linux
  - Purpose: Basic HTTP Server (this is a red herring)
  - IP Address192.168.1.105
- Name of Target 1
  - Operating System: Linux
  - Purpose: HTTP Server (also wordpress site)
  - IP Address192.168.1.110
- Name of Target 2
  - Operating System: Linux
  - Purpose: HTTP Server
  - IP Address: 192.168.1.115

### Description of Targets

The target of this attack was: Target 1 192.168.1.110
Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:
 - Excessive HTTP Errors 
 - HTTP Request Size Monitor 
 - CPU Usage Monitor 

### Monitoring the Targets**
Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

### Excessive HTTP Errors
Alert 1 is implemented as follows:
 - Metric: http.response.status_code > 400
 - Threshold: 5 in last 5 minutes
 - Vulnerability Mitigated: By creating an alert, the security team can identify attacks & block the ip, change the password, & close or filter the port 22
 - Reliability: No, this alert does not generate a lot of false positives. This alert is highly reliable in identifying brute force attacks.

### HTTP Request Size Monitor
 Alert 2 is implemented as follows:
 - Metric: http.request.bytes
 - Threshold: 3500 in last 1 minute
 - Vulnerability Mitigated: By controlling the number of http request size through a filter it protects against DDOS attacks
 - Reliability: No, this alert doesn't generate a lot of false positives because it is reliable.

### CPU Usage Monitor
 Alert 3 is implemented as follows:
 - Metric: system.process.cpu.total.pct
 - Threshold: 0.5 in last 5 minutes
 - Vulnerability Mitigated: By controlling the CPU usage percentage at 50%, it will trigger a memory dump of stored information is generated
 - Reliability: Yes this alert can generate a lot of false positives bc the cpu can spike even if there is not an attack.

