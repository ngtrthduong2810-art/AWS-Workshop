---
title: "Worklog Week 5"
date: 2026-05-13
weight: 6
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives: Shaping the FinOps Mindset in Software Development

Entering the fifth week, the core objective is no longer just about operating infrastructure, but mastering cloud economics. For a developer, designing a robust system is not enough if it consumes too much budget. This week focuses on building a "financial defense system" through detailed objectives:

- **Explore the FinOps philosophy:** Gain a general understanding of how to manage costs on AWS using the AWS Budgets service. Deeply understand its role not just in monitoring, but in proactive control and alerting of AWS service usage costs.
- **Master budget deployment methods:** Practice creating a Budget using an available template to set up a budget quickly and accurately.
- **Separate monitoring layers:** 
  - Create a Cost Budget to directly track the cash flow of AWS usage costs on a monthly basis.
  - Create a Usage Budget to monitor AWS resource usage levels, specifically targeting services billed by running time (like EC2).
- **Approach enterprise cost optimization models:** Learn about Reservation Budgets to monitor the utilization of Reserved Instances, and explore Savings Plans Budgets to evaluate the utilization of Savings Plans.
- **Build an automated alerting system:** Configure alert thresholds and set up email notifications to ensure administrators receive alerts immediately when costs or usage approach risk thresholds.
- **System Analysis and Maintenance:** Evaluate effectiveness by checking Budget history, Budget health, and alert statuses. Simultaneously, practice cleanup (deleting created Budgets) after completing the lab to avoid being bothered by unnecessary notifications in the future.

---

### Tasks to be Implemented this Week:

| Day | Deep-Dive Tasks | Start Date | End Date | Reference Sources |
| --- | --- | --- | --- | --- |
| Mon | - **Foundational Research:** Read the workshop overview: Cost Management with AWS Budgets. <br> - Understand the architectural role of AWS Budgets in the AWS cost management strategy. <br> - Access the central AWS Billing and Cost Management console. <br> - Analyze and get familiar with the Budgets interface in the AWS Console. | 01/06/2026 | 01/06/2026 | https://000007.awsstudygroup.com/1-create-budget/ |
| Tue | - **Template Deployment:** Create a Budget using an available template. <br> - Analyze the benefits of selecting the Monthly cost budget template. <br> - Input identifier parameters: Budget name, monthly budget amount, and set the alert threshold. <br> - Evaluate the process by verifying the successful creation and viewing data in the Budget history. | 02/06/2026 | 02/06/2026 | https://000007.awsstudygroup.com/1-create-budget/ |
| Wed | - **Cost Budget Customization:** Create a Cost Budget using Customize mode for deep parameter intervention. <br> - Select the Cost budget type. <br> - Flexibly configure variables: Period, Budget effective dates, Budgeting method, and Budgeted amount. <br> - Configure Budget scope to apply comprehensively to All AWS services and calculate based on Unblended costs. | 03/06/2026 | 03/06/2026 | https://000007.awsstudygroup.com/2-cost-budgets/ |
| Thu | - **Alert Chain Setup:** Configure the alert threshold for the Cost Budget. <br> - Add an email address to receive automated alerts when costs exceed the threshold. <br> - Review the entire Cost Budget configuration. <br> - Create the Budget and verify its active status on the system. | 04/06/2026 | 04/06/2026 | https://000007.awsstudygroup.com/2-cost-budgets/ |
| Fri | - **Hardware Capacity Control:** Create a Usage Budget to directly monitor resource utilization instead of currency. <br> - Select Usage budget from Budget types. <br> - Configure Usage type groups filters, specifically focusing on EC2: ELB - Running Hours. <br> - Establish maximum usage hours limits and configure the corresponding alert threshold. | 05/06/2026 | 05/06/2026 | https://000007.awsstudygroup.com/3-usage-budget/ |
| Sat | - **Commitment Model Analysis:** Learn about the mechanism of Reservation Budgets applied to Reserved Instances. <br> - Learn about the mechanism of Savings Plans Budgets applied to Savings Plans. <br> - Practice or view instructions on creating RI Budgets and Savings Plans Budgets. <br> - Analyze how to configure coverage threshold, utilization threshold, and email alerts. | 06/06/2026 | 06/06/2026 | https://000007.awsstudygroup.com/4-reservation-budget/ <br> https://000007.awsstudygroup.com/5-saving-plans-budget/ |
| Sun | - **Evaluation and Cleanup:** Comprehensively check the list of created Budgets. <br> - Read and interpret metrics from Budget health and Budget history. <br> - Proceed to delete the Budgets created during the practice. <br> - Write a report recording results, difficulties, solutions, and extracted lessons. | 07/06/2026 | 07/06/2026 | https://000007.awsstudygroup.com/6-clean-up/ |

---

### Week 5 Results: Theoretical Survey and Summary

#### 1. Architectural Analysis of AWS Budgets & AWS Billing and Cost Management

**AWS Budgets System Architecture Mindset**
In a Cloud environment, resource provisioning occurs via a few lines of code or clicks. This leads to the risk of a "cost explosion" without a control mechanism. AWS Budgets is a service used to track costs, resource usage, and cost-saving commitments on AWS. It provides extreme flexibility, helping users set budgets by day, month, quarter, or year.

A crucial architectural finding: AWS Budgets only warns, it does not automatically stop services when exceeding the budget. This might seem like a flaw at first glance, but it is actually a "by design" choice by AWS. If a backend system serving thousands of users is suddenly shut down over a few dollars, the business damage would be far greater. Therefore, when costs or usage exceed the configured threshold, AWS Budgets can send alerts via email, delegating the incident response decision to humans. This proves AWS Budgets is suitable for beginners learning AWS because it helps control costs during lab practice, while remaining safe for production systems.

**Central AWS Billing and Cost Management Console**
This is the financial heart of the account. I learned how to access AWS Billing and Cost Management from the AWS Management Console. This interface doesn't just show the balance; I understand this is the area to manage cost information, bills, budgets, and cost alerts. Here, I know how to use the Budgets menu to create, view, edit, or delete Budgets and how to check the Budget status after successful creation.

#### 2. Budgeting Strategies (Template vs. Customize)

**Rapid Deployment with Templates**
In many cases, we only need a basic alert. Templates help create Budgets quickly with available configurations. By knowing to select "Use a template" for a simplified template, specifically "Monthly cost budget" to create a monthly cost budget, I saved a lot of operational time. The input fields only require entering the Budget name, monthly budget amount, and alert threshold. However, I also understand that templates are suitable when needing to quickly set up basic cost alerts. For complex systems, we must delve into Customize mode. Post-verification is always necessary by checking Budget history after successfully creating the Budget.

**Deep Customization with Cost Budget**
For higher granularity, Cost Budgets are used to track AWS usage costs via Customize mode. I mastered the process of creating a Cost Budget using Customize mode and selecting the Budget type as Cost budget.

This process requires an understanding of financial cycles:
- **Time cycle:** Configure Period including Daily, Monthly, Quarterly, or Annually.
- **Budget lifecycle:** I learned to distinguish between Recurring Budget and Expiring Budget. A Recurring Budget repeats periodically (for continuously running servers), while an Expiring Budget only applies for a specific time period (ideal for short-term testing or new feature deployments).
- **Allocation strategy:** Choose the Budgeting method between Fixed: fixed budget for each period, and Planned: budget can change month by month.
- **Monitoring Scope:** Choose Budget scope as All AWS services to track all AWS services, and specifically, choose Aggregate costs by Unblended costs. Unblended costs reflect the actual raw costs at the current moment, unskewed by averaged discount algorithms, providing the most transparent data. Finally, I know to add an alert threshold to receive an alert when costs reach a certain percentage of the budget.

#### 3. Shifting Perspective from Costs to Physical Resources (Usage Budget)

Looking solely at cash flow sometimes creates a lag in detecting system errors (e.g., an infinite loop generating millions of S3 requests). Therefore, a Usage Budget is used to track resource usage levels instead of cost amounts. I clearly analyzed the difference between Cost Budget and Usage Budget: Cost Budgets track costs, whereas Usage Budgets track resource usage.

The setup process involves selecting the Budget type as Usage budget. The key here is the classification ability by selecting Usage type groups to specify the type of resource to track. Within the lab scope, a Usage Budget can be used to track EC2: ELB - Running Hours. By setting the usage hours limit for the resource and configuring email alerts when usage exceeds the threshold, administrators can intervene right before the bill is generated. Ultimately, I understand Usage Budgets are useful for services billed by the hour like EC2, Load Balancers, or continuously running resources.

#### 4. Managing Long-term Commitments (Reservation & Savings Plans Budgets)

Although these packages are rarely purchased during learning, understanding them is the standard for a true Cloud Engineer.
- **Reservation Budget:** Understand Reservation Budgets are used to track Reserved Instances. Since Reserved Instances often require commitment or upfront payment, in the lab scope, one should only view the guide or practice at a demo level. This budget helps track coverage or utilization of Reserved Instances. Specifically, configuring the Coverage threshold to track the coverage level of Reserved Instances reveals what percentage of running servers benefit from the discounted rate. This proves Reservation Budgets are suitable for enterprise environments already using Reserved Instances for long-term cost optimization.
- **Savings Plans Budget:** Understand Savings Plans Budgets are used to track Savings Plans usage. This is a more flexible model, as Savings Plans is a commitment to use computing resources over a specific period in exchange for lower prices compared to On-Demand. This tool helps track the utilization threshold. If the utilization rate is low, the system will warn by configuring email alerts to receive notifications when Savings Plans usage does not meet expectations. In summary, Savings Plans Budgets are suitable when the system has stable compute needs over a long period.

#### 5. Alerting Systems, Health, and Cleanup Discipline

- **Alert System:** Understand alert threshold is a warning threshold set by percentage or specific value. To build a solid defense system, it's necessary to configure multiple alert levels, e.g., 50%, 80%, and 100%, and add an email to receive budget alerts. It should be clearly planned that the email recipient should be someone responsible for tracking costs or managing the AWS account, and one must always check the confirmation email or notification from AWS Budgets after configuration.
- **Diagnostics (Health & History):** Understand Budget health indicates the current status of the budget compared to the set level. For a comprehensive view, use Budget history to view cost or usage trends over time and observe budget status to assess whether the AWS account is overspending. A technical characteristic to note is that cost data on AWS may have latency, so it is necessary to wait a while for data to fully update.
- **Cleanup Discipline:** Understand cleanup is a necessary step after completing the lab. Knowing to delete created Budgets if only used for practice helps avoid system clutter. I also clearly understand the architectural nature that deleting AWS Budgets does not delete running resources in the AWS account because AWS Budgets is only a tracking and alerting tool, not an application processing resource. Finally, always check the Budgets list again after deletion to ensure no unnecessary alerts remain.

---

### Hands-on Experience: Step-by-Step Configuration Analysis

The practical process is divided into 6 modules, ranging from basic initialization to system cleanup.

**Module 1 — Establishing the First Line of Defense (Create Budget with Template)**
- Access the AWS Management Console.
- Search for and open the AWS Billing and Cost Management service.
- On the navigation bar, select Budgets in the left menu.
- Start the process by clicking Create a budget to begin creating a budget.
- Choose the quick method: Select Use a template (simplified).
- Here, I select the Monthly cost budget template as it covers monthly needs well.
- Enter the Budget name as required by the lab and enter the monthly budget amount as a safe limit.
- Configure the alert threshold to receive an alert when costs reach the threshold.
- Click Create budget to complete.
- Afterward, I verified that the Budget was successfully created and opened Budget history to view the budget history. This process helped me review the types of alerts available in the template.

**Module 2 — Touching Deep Settings (Create Cost Budget)**
- Return to AWS Billing and Cost Management.
- Select Budgets in the left menu and click Create budget.
- This time, in the Budget setup section, select Customize to manually fine-tune.
- In Budget types, select Cost budget and click Next to continue.
- In the Set your budget section, enter the Budget name as `Monthly`.
- Choose an appropriate Period, for example, Monthly.
- Under Budget effective dates, I am required to categorize: choose Recurring Budget if you want the budget to repeat, or choose Expiring Budget if you only want it to apply once.
- Next is configuring the Budgeting method: choose Fixed if you want the same budget for each period, or choose Planned if you want to set different budgets for each month.
- Enter the Budgeted amount according to the desired cost level.
- For a comprehensive view, in Budget scope, select All AWS services.
- Ensure transparency by selecting Unblended costs under Aggregate costs by.
- Click Next to move to the alert configuration step.
- Select Add an alert threshold.
- Enter the alert percentage, e.g., 80% or 100%, and enter the email to receive alerts.
- Review the entire configuration before clicking Create budget to complete. Finally, confirm that the Budget appears in the Budgets list.

**Module 3 — Binding Physical Resources (Create Usage Budget)**
- Go back to Budgets in AWS Billing and Cost Management and click Create budget.
- Select Customize, but under Budget types, select Usage budget and click Next to continue.
- Enter a name for the Usage Budget.
- In the Budget against section, select Usage type groups. This is a crucial step to select the type of usage to track, e.g., EC2: ELB - Running Hours.
- Proceed to configure Set budget amount with these details: choose Period as Daily, Monthly, Quarterly, or Annually; choose Budget renewal type as Recurring or Expiring; choose Budgeting method as Fixed or Planned.
- Then, enter the maximum usage hours you want to track and keep the default configuration in Budget scope if it suits the lab.
- Click Next to configure alerts.
- Select Add an alert threshold.
- Enter the alert percentage compared to the usage budget and enter the email to receive notifications.
- Review the configuration and click Create budget to complete.
- Monitor the system by checking Budget health to see current usage against the limit and opening Budget history to track usage trends.

**Module 4 & 5 — Simulating Enterprise Governance (Create RI & Savings Plans Budgets)**
- For RI: Access AWS Billing and Cost Management > Select Budgets > Click Create budget.
- In Budget setup, select Customize > Select Reservation budget > Click Next.
- Enter a Budget name for the Reservation Budget.
- Configure the Coverage threshold to track the coverage level of Reserved Instances.
- Configure Budget scope according to the lab instructions.
- In the Alert setting section, enter the email to receive alerts. Review the information and click Create budget.
- Verify the Reservation Budget was created. An important extracted lesson: note that within the lab scope, it is not mandatory to purchase Reserved Instances as it may incur costs or require payment commitments.
- For Savings Plans: Access AWS Billing and Cost Management > Select Budgets > Click Create budget > Select Customize > In Budget types, select Savings Plans budget > Click Next.
- Enter a Budget name for the Savings Plans Budget.
- Configure the Utilization threshold to track Savings Plans usage.
- Keep Budget scope at default if appropriate for the lab.
- In the Alert setting section, enter the email to receive alerts. Review the entire configuration and click Create budget to complete.
- Check the newly created Budget in the list. Similar to RI, note that Savings Plans usually involve long-term usage commitments, so in a learning environment, you should only perform operations according to instructions or view demos.

**Module 6 — System Cleanup Discipline (Clean Up Resources)**
- Access AWS Billing and Cost Management and select Budgets in the left menu.
- Check the list of Budgets created during the lab.
- Select the Budget to delete and choose Action.
- Click Delete. In the confirmation dialog, click Delete to complete.
- Repeat the process for the remaining Budgets created during the practice.
- Check the Budgets list again after deletion.
- This step reinforces theoretical knowledge: note that deleting a Budget only removes the tracking and alerting configuration, and does not affect running AWS resources.

---

### Week 5 Results Evaluation:

This week's practice sequence significantly improved my FinOps awareness:
- Completed learning about the AWS Budgets service in AWS cost management.
- Know how to create a budget using available templates for quick alert setup.
- Created a Cost Budget to track AWS usage costs by month.
- Created a Usage Budget to track AWS resource usage levels.
- Understood the difference between Cost Budget and Usage Budget.
- Grasped the purpose of Reservation Budgets in tracking Reserved Instances.
- Grasped the purpose of Savings Plans Budgets in tracking Savings Plans.
- Know how to configure alert thresholds and email notifications for Budgets.
- Know how to check Budget health and Budget history to assess the budget status.
- Know how to clean up Budgets created in a lab environment.
- Thereby gaining a clearer realization of the importance of cost control when practicing on AWS.

---

### Difficulties Encountered During System Analysis:

- **Interface Complexity:** The Billing and Cost Management interface has many sections, making it initially easy to confuse Bills, Cost Explorer, and Budgets. Distinguishing between the past (Explorer) and the future (Budgets) requires good categorization skills.
- **Ambiguity between Concepts:** It's necessary to clearly distinguish Cost Budget and Usage Budget because these two types of Budgets track two different sets of information.
- **UX Operational Errors:** When configuring a Usage Budget, you must select the correct Usage type group to track the right resource type. With thousands of services, one wrong click renders the Budget meaningless.
- **Account Limitations:** Some new AWS accounts may not fully display Budget types other than Cost Budgets.
- **Data Latency:** Cost and usage data on AWS may update slowly, so immediately after creating a Budget, full data might not be visible. This often causes a psychological panic effect when setting up the system.
- **Abstract Nature of Commitment Systems:** The RI Budget and Savings Plans Budget sections are confusing because they relate to long-term usage commitment models.
- **Operational Risk (Alert Fatigue):** If multiple alerts are configured or the wrong email is entered, the user may not receive desired alerts, or conversely, get spammed with emails leading to alert fatigue.
- **Fundamental Knowledge Gaps:** It is crucial to note that AWS Budgets only alerts; it does not automatically stop services when the budget is exceeded. Misunderstanding this can lead to severe financial consequences.

---

### Solutions and Extracted Best Practices:

- **Proactive Learning:** Read each step in the workshop carefully before operating on the AWS Console.
- **Systematize with Notes:** Note down the purpose of each type of Budget to avoid confusion:
  - Cost Budget is used to track costs.
  - Usage Budget is used to track resource usage levels.
  - Reservation Budget is used to track Reserved Instances.
  - Savings Plans Budget is used to track Savings Plans.
- **Information Risk Control:** When configuring alerts, enter the correct email and check the inbox to confirm receipt of notifications.
- **Build Multi-tier Alert Strategies:** You should set multiple alert levels such as 50%, 80%, and 100% to proactively control costs.
- **Safe Practice:** Avoid making arbitrary financial commitments. Absolutely do not purchase Reserved Instances or Savings Plans in a learning account unless formally required.
- **System Operation Discipline:**
  - After completing the lab, you must delete the practice Budgets to avoid receiving unnecessary notifications.
  - Check the Billing Dashboard again after each lab session to detect abnormal costs.
  - Combine AWS Budgets with the habit of resource cleanup to limit unexpected costs.

---

### Optimal Directions for Next Week:

The FinOps journey doesn't stop at setting limits (Budgets) but expands into advanced analysis and detection. Upcoming research topics include:
- Continue to learn more deeply about AWS Billing and Cost Management.
- Research AWS Cost Explorer further to analyze costs by service, time, and account.
- Learn how to use the AWS Free Tier Dashboard to track free limits, maximally protecting the learning budget.
- Learn AWS Cost Anomaly Detection to detect abnormal costs (applying Machine Learning to data detection).
- Research more about AWS Organizations and how to manage costs for multiple AWS accounts (Multi-account architecture).
- Practice building the habit of checking the Billing Dashboard after every lab.
- Finally, always ensure the preparation of evidence images, operation notes, and result reviews to complete the report for the following week.