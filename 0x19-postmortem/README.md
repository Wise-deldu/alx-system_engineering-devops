# Postmortem: Web Application Outage on June 20, 2024
## Issue Summary

**Duration of Outage:** June 20, 2024, from 14:15 to 15:45 GMT (1 hour 30 minutes)

**Impact:** The primary web application was completely down. Users experienced a "503 Service Unavailable" error when attempting to access the site. Approximately 90% of the user base was affected.

**Root Cause:** A misconfigured load balancer rule led to all traffic being directed to a single, overwhelmed server, causing it to crash.

## Timeline
14:15 GMT: Issue detected via automated monitoring alert indicating a spike in 503 errors.
14:16 GMT: On-call engineer notified and began initial investigation.
14:20 GMT: Verified issue by attempting to access the web application and confirming the 503 errors.
14:25 GMT: Initial assumption was a potential issue with the web servers. Restarted web servers.
14:35 GMT: No improvement after restarting web servers. Error persisted.
14:40 GMT: Escalated to the network engineering team for further investigation.
14:50 GMT: Network engineering team identified a recent configuration change to the load balancer.
15:00 GMT: Investigated load balancer configuration and found a misconfigured rule redirecting all traffic to a single server.
15:10 GMT: Corrected the load balancer rule to properly distribute traffic across all servers.
15:20 GMT: Began monitoring traffic distribution and server load.
15:45 GMT: Confirmed that the web application was fully functional and traffic was balanced across all servers. Declared incident resolved.
Root Cause and Resolution
Root Cause: The issue was caused by a misconfiguration in the load balancer settings. During a routine update to improve traffic distribution, a rule was mistakenly set to direct all incoming traffic to a single server. This server quickly became overwhelmed and crashed, leading to the "503 Service Unavailable" errors seen by users.

**Resolution:** The misconfigured rule was identified and corrected. The load balancer was reconfigured to evenly distribute traffic across all available servers. This action alleviated the load on the single server, allowing it to recover and the service to resume normal operations.

## Corrective and Preventative Measures
**Improvements/Fixes:**

Configuration Review Process: Implement a more rigorous review process for configuration changes, especially those involving critical components like load balancers.
Automated Configuration Validation: Develop automated tools to validate load balancer configuration changes before they are applied.
Enhanced Monitoring: Improve monitoring to detect uneven traffic distribution and server load imbalances earlier.

## Tasks:

**Task 1:** Develop and implement a checklist for reviewing critical configuration changes.
**Task 2:** Create automated scripts to validate load balancer configurations for common issues.
**Task 3:** Add new monitoring alerts to detect abnormal traffic patterns and server loads.
**Task 4:** Conduct a training session for engineers on the new configuration review process and tools.
**Task 5:** Schedule regular audits of load balancer configurations to ensure ongoing compliance with best practices.
By addressing these points, we aim to prevent similar incidents in the future and ensure a more robust and reliable web application for our users.