---
title: "Worklog Week 6"
date: 2026-05-22
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives: Shaping the Observability Mindset in Infrastructure Operations

Entering the 6th week of this 12-week cloud journey, the core objective has shifted from deploying resources to establishing the "all-seeing eyes" for the entire architecture. As a software developer, deploying code to a server is not enough; maintaining and understanding the system's state is vital. The key objectives include:

- **Explore the monitoring platform:** Learn the general overview of Amazon CloudWatch and understand the role of CloudWatch in monitoring resources and applications on AWS.
- **Measure core performance:** Practice using CloudWatch Metrics to monitor system performance, thereby assessing the actual health status of servers and services.
- **Master data analysis tools:** Learn and flexibly apply advanced syntaxes to explore Search Expressions, Math Expressions, and Dynamic Labels to refine and transform raw data into meaningful indicators.
- **Exploit system logs:** Dive deep to discover CloudWatch Logs and the powerful CloudWatch Logs Insights. Push the boundaries by creating Metric Filters from log data, turning static text lines into dynamic charts.
- **Automate incident response:** Proceed to configure CloudWatch Alarms to monitor and alert on incidents, enabling the operations team to react in real-time before applications completely crash.
- **Visualize and Optimize:** Build CloudWatch Dashboards to visualize monitoring data, centralizing everything onto a single screen. Finally, execute resource cleanup after completing the practical exercises to optimize costs and enhance skills in monitoring and managing systems on AWS.

---

### Schedule and Implementation Tasks for the Week:

| Day | Deep-Dive Tasks | Start Date | End Date | Reference Sources |
| --- | --- | --- | --- | --- |
| Mon | - **Foundational Research:** Read the workshop overview of Amazon CloudWatch. <br> - Analyze theories to understand the role of CloudWatch in AWS as a centralized data hub. <br> - Prepare the practical environment by provisioning necessary resources. | 08/06/2026 | 08/06/2026 | https://000008.awsstudygroup.com/1-introduction/ |
| Tue | - **Exploit Metrics:** Begin to learn CloudWatch Metrics to collect numerical data. <br> - Directly view and analyze Metrics from running resources. <br> - Practice Search Expressions to accurately filter and search for deeply hidden indicators. | 09/06/2026 | 09/06/2026 | https://000008.awsstudygroup.com/3-cloud-watch-metric/ |
| Wed | - **Transform Data:** Practice Math Expressions to perform mathematical operations (add, subtract, calculate ratios) across multiple Metrics streams. <br> - Use Dynamic Labels so charts automatically display resource names instead of dry IDs. <br> - Visualize Metrics data to easily evaluate performance trends. | 10/06/2026 | 10/06/2026 | https://000008.awsstudygroup.com/3-cloud-watch-metric/ |
| Thu | - **Log Management:** Work with CloudWatch Logs to collect application outputs. <br> - Write log query commands using CloudWatch Logs Insights to search for root causes. <br> - Set up and create Metric Filters from Logs to count the occurrences of error keywords. | 11/06/2026 | 11/06/2026 | https://000008.awsstudygroup.com/4-cloud-watch-logs/ |
| Fri | - **Alerting Systems:** Create CloudWatch Alarms based on critical system thresholds. <br> - Integrate and configure SNS Notifications to push alert streams via email/SMS. <br> - Proactively check the operation of Alarms by simulating high workloads. | 12/06/2026 | 12/06/2026 | https://000008.awsstudygroup.com/5-cloud-watch-alarm/ |
| Sat | - **Information Centralization:** Build professional CloudWatch Dashboards. <br> - Customize by adding Metrics and Alarms to the Dashboard. <br> - Create a single interface to monitor centralized data. | 13/06/2026 | 13/06/2026 | https://000008.awsstudygroup.com/6-cloud-watch-dashboard/ |
| Sun | - **Maintenance and Summary:** Check the created resources throughout the process. <br> - Strictly execute Cleanup Resources to protect the AWS bill. <br> - Summarize the knowledge learned during the week to translate it into practical experience. | 14/06/2026 | 14/06/2026 | https://000008.awsstudygroup.com/7-clean-up/ |

---

### Week 6 Results: Deep-Dive Theoretical Summary

#### 1. Amazon CloudWatch Ecosystem Architecture
Through the research process, I understand Amazon CloudWatch is a system monitoring and observability service on AWS. It acts as a central nervous system, constantly listening to the infrastructure's heartbeat. By knowing how to collect and analyze data from Metrics and Logs, administrators can predict failure risks beforehand. Therefore, I fully understand the importance of monitoring resources and applications to ensure High Availability.

#### 2. Analyzing Measurement Data (CloudWatch Metrics)
Metrics are numbers that speak. I know how to view and analyze Metrics such as CPU Utilization or Network In/Out. However, when the system expands, manual searching is impossible. Thus, I understand how to use Search Expressions to filter data incredibly efficiently. Going beyond raw data, I can use Math Expressions to calculate Metrics data (e.g., calculating error rates with the formula `Errors / RequestCount`). To make the interface more human-friendly, I apply Dynamic Labels to display data more intuitively.

#### 3. Exploiting the Power of CloudWatch Logs
System logs contain every truth about an application. I understand how to collect and store Logs into Log Groups. The breakthrough is that when a system encounters an error, instead of reading millions of lines of text, I know how to query Logs using CloudWatch Logs Insights via SQL-like commands. Another excellent technique is creating Metric Filters from Log events, which automatically scans log streams, catches keywords like "Exception," and converts them into a real-time error-counting Metric.

#### 4. Automated Response with CloudWatch Alarms
Sitting and staring at a screen all day is impractical. I have thoroughly understood the operating mechanism of CloudWatch Alarms. This system operates on a state machine principle (OK, ALARM, INSUFFICIENT_DATA). By knowing how to set appropriate alert thresholds, alarms will be triggered if the system crosses safety boundaries. Accompanying this, configuring SNS to receive notifications when incidents occur is the final link, forwarding alert signals to the system engineer's inbox.

#### 5. Central Control Panel (CloudWatch Dashboards)
To solve the issue of fragmented information, I proceed to create a Dashboard to monitor the system. By displaying Metrics and Alarms on a single interface, administrators gain a "single pane of glass," immensely supporting the ability to monitor system performance in real-time.

---

### Hands-on Experience: Step-by-Step Deployment Simulation

**Module 1 — System Initialization (Introduction)**
- Access Amazon CloudWatch from the AWS console.
- Spend time to understand the architecture and main functions of CloudWatch through data flow diagrams.
- Begin to prepare the practical environment, provisioning a few EC2 instances as monitoring targets.

**Module 2 — Fine-tuning Measurement Data (CloudWatch Metrics)**
- Directly view Metrics of AWS resources to evaluate CPU consumption levels.
- Apply coding syntax to use Search Expressions, calling out internal network parameters.
- Deploy and practice Math Expressions to draw charts comparing average load and maximum load.
- Configure Dynamic Labels so chart labels automatically reflect server names instead of IP ranges.

**Module 3 — System Log Administration (CloudWatch Logs)**
- Create and manage Log Groups to separately categorize web server and database logs.
- Write queries to query Logs using Logs Insights, filtering out the 20 most recent 404 errors within the last hour.
- Set up and create Metric Filters to scan for the keyword "Error", turning it into a continuous counting indicator on the chart.

**Module 4 — Building the Alarm Barricade (CloudWatch Alarms)**
- Based on the newly created Metric Filter, I manipulate to create a new Alarm.
- Link with the messaging service by configuring SNS Notifications and confirming email subscriptions.
- Simulate an error on the server and check the Alarm status as it turns red, simultaneously checking the inbox.

**Module 5 — Visualizing Data (CloudWatch Dashboards)**
- Initialize a new Dashboard with a grid interface.
- Sequentially add Metrics and Alarms to the Dashboard using Line chart and Gauge widgets.
- Customize the display Widgets to highlight high-risk areas.

**Module 6 — System Cleanup Discipline (Cleanup Resources)**
- Review and check the created resources across all modules.
- Proceed to delete unnecessary resources (Dashboards, Alarms, Log Groups) to cut off storage charges.
- Confirm the completion of Cleanup resulting in a tidy console.

---

### Week 6 Results Evaluation:

- Understand the role of Amazon CloudWatch in AWS as an operational backbone.
- Know how to use Metrics, Logs, and Alarms proficiently.
- Have successfully practiced Search Expressions and Math Expressions to enhance chart analysis capabilities.
- Master the cycle of creating Metric Filters and CloudWatch Alarms.
- Successfully built a complete CloudWatch Dashboard with high application value.
- Thereby, enhance skills in monitoring and troubleshooting on AWS at a professional level.

---

### Analytical Difficulties and Barriers:

- **Linking Logic:** In the initial stages, it was hard to understand the relationship between Metrics, Logs, and Metric Filters. The process from raw logs to a warning chart requires seamless thinking.
- **Complex Syntax:** Using Search Expressions and Math Expressions was initially complicated due to their distinct language structures, making it very easy to mistype variables.
- **Logs Insights Querying:** Need time to get used to Logs Insights as it uses a hybrid syntax between SQL and Regex, requiring multiple trial and error attempts.
- **Notification Stream Configuration Risks:** Configuring SNS Notifications must be executed precisely. If the wrong Topic is selected or email Subscriptions are unconfirmed, even if the Alarm triggers, the notification will never reach the administrator.

---

### Solutions and Remediation:

- **Deep Research:** Carefully read workshop materials and AWS CloudWatch documentation to systematize concepts via diagrams.
- **Learning by Doing:** Turn theory into reflexes by practicing multiple times with Metrics and Logs across various simulated environments.
- **Partial Testing:** Always check the SNS configuration before testing Alarms by sending manual test messages via the SNS interface.
- **Knowledge Inheritance:** Actively refer to real-world examples from AWS Documentation to copy effective Logs Insights query templates, saving debugging time.

---

### Optimal Directions for Next Week:

The journey to conquer the Cloud will shift to one of its most critical pillars: Security.
- Shift research focus to explore AWS Identity and Access Management (IAM).
- Directly practice creating Users, Groups, and Policies based on the Least Privilege principle.
- Increase the difficulty level by learning the MFA mechanism and securing AWS accounts.
- Deeply study access rights management in a Cloud environment to ensure an impenetrable network architecture.
- Finally, continue to prepare evidence images and finalize the practical report for the upcoming week.