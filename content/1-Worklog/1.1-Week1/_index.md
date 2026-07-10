---
title: "Worklog Week 1"
date: 2026-04-14
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Core Objectives: Bootstrapping the Cloud-Native Mindset

The first week is the most crucial stepping stone for transitioning from a traditional On-premises mindset to a flexible Cloud environment. The goal is not just to use tools, but to understand the architectural core:
- Proactively integrate into the working environment and connect with members of the First Cloud Journey project.
- Build a solid knowledge foundation of Cloud Computing and explore the diverse AWS service ecosystem.
- Dive deep into the global infrastructure architecture, master management tools, and practice cost optimization thinking (FinOps) from day one.
- Successfully set up a 2025 AWS Free Tier account and conquer the $200 support credit milestone to create a safe financial buffer for future labs.
- Accurately execute core labs centered around account setup, security enhancement, and budget monitoring to form standard operational discipline.

---

### In-Depth Implementation Log:

| Day | Deep-Dive Tasks | Start Date | End Date | Reference Documents |
| --- | --- | --- | --- | --- |
| Mon | - **Cultural Integration:** Network and get acquainted with the FCJ team. <br> - Thoroughly study the regulations and operational rules at the internship site to ensure a professional workflow. | 20/04/2026 | 20/04/2026 | https://www.notion.so/Group-description-TP-HCM-347df829a730809a8f63d39505644917 |
| Tue | - **Foundational Research:** Explore Module 01-01: The Nature of Cloud Computing. <br> - Analyze Module 01-02: AWS's Position and Differentiation compared to competitors. <br> - Explore Module 01-03: Planning the Cloud Conquest Roadmap. <br> - Explore Module 01-04: Decoding AWS Global Infrastructure to understand how to design highly available systems. | 21/04/2026 | 21/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| Wed | - **Tools and Security:** Study Module 01-05: AWS Management Tools Handbook. <br> - Study Module 01-06: Cost Optimization Strategy & Interacting with AWS Support. <br> - Module 01-07: Deep dive research and practical application. <br> - **Practical Deployment:** <br>&emsp;+ Lab01-01: Successfully initialize an AWS account. <br>&emsp;+ Lab01-02: Set up Virtual MFA protection layer. <br>&emsp;+ Lab01-03: Delegate permissions via creating an Admin group & user. <br>&emsp;+ Lab01-04: Test the authentication Support request process. | 22/04/2026 | 22/04/2026 | https://000001.awsstudygroup.com/ <br> https://000002.awsstudygroup.com/ |
| Thu | - **Execute Budget Management (FinOps):** <br>&emsp;+ Lab07-01: Rapidly deploy Budgets via Templates. <br>&emsp;+ Lab07-02: Configure Cost Budgets with alert thresholds. <br>&emsp;+ Lab07-03: Set up Usage Budgets to monitor resources. <br>&emsp;+ Lab07-04: Monitor commitments via RI Budgets. <br>&emsp;+ Lab07-05: Manage Savings Plans Budget packages. <br>&emsp;+ Lab07-06: Perform a clean up of all Budgets after testing. | 23/04/2026 | 23/04/2026 | https://000001.awsstudygroup.com/ |
| Fri | - **Conquer Challenges:** Complete 5 challenges to unlock $200 credit: <br>&emsp;+ Operate an EC2 Instance (+$20). <br>&emsp;+ Experience AI with Amazon Bedrock (+$20). <br>&emsp;+ Configure AWS Budgets alerts (+$20). <br>&emsp;+ Initialize a Lambda Web App (+$20). <br>&emsp;+ Deploy an RDS Database (+$20). <br> - Expand knowledge on architectural standards: AWS Well-Architected Framework. | 24/04/2026 | 24/04/2026 | https://000001.awsstudygroup.com/ <br> https://docs.aws.amazon.com/wellarchitected/ |

---

### Week 1 Milestones and Achievements: Deep-Dive Theoretical Summary

#### Core Knowledge Arsenal

**1. The Nature of Cloud Computing**
- Deeply grasp the Cloud philosophy: flexible payment with the pay-as-you-go model and instant provisioning via on-demand resource supply.
- Clearly delineate the management levels of service models: IaaS, PaaS, and SaaS.
- Identify differences in control and security between deployment methods: Public, Private, and Hybrid Cloud.

**2. AWS Dominance and Ecosystem**
- Recognize the massive scale of the AWS platform with an ecosystem exceeding 200 services.
- Analyze the core advantages that make AWS renowned: strict security, high availability, flexible elasticity, and cost-efficiency.
- Systematize services into key groups for easy architectural reference:
  - Compute capability: EC2, Lambda.
  - Storage space: S3, EBS.
  - Networking: VPC, Security Group.
  - Database: RDS, Aurora.
  - Artificial Intelligence (AI/ML): Amazon Bedrock.

**3. Roadmap Planning and Free Tier Exploitation**
- Outline the AWS skills development journey from newbie to expert.
- Detail the 2025 AWS Free Tier incentive policy:
  - Immediately pocket a $100 credit after successfully clicking to create an account.
  - Know how to hunt for an additional $100 credit via 5 practical labs.
  - Evaluate the pros and cons between the Free Plan (safe for 6 months) and Paid Plan (unlocks all service barriers) to make an appropriate registration decision.

**4. Decoding Global Infrastructure**
- Visualize AWS's physical network through Regions and Availability Zones (AZs) spanning the globe.
- Solidify definitions of Regions, AZs, and Edge Locations in the CDN network.
- Formulate a strategic Region selection mindset based on factors: network latency, budget, and legal boundaries (data compliance).

**5. Management Tools Handbook & Cost Optimization**
- Get familiar with visual operations via the AWS Management Console web interface.
- Access the power of automation capability through AWS CLI and programming via SDKs, along with the convenience of the AWS CloudShell browser environment.
- Explore the trio of cost-gatekeeping tools: AWS Budgets, Cost Explorer, and Cost & Usage Reports.
- Learn intelligent purchasing through long-term commitments with Reserved Instances, Savings Plans, and Spot Instances.
- Categorize Support tiers (Basic, Developer, Business, Enterprise) and practice opening a standard technical support ticket.

**6. Deep Dive Research — Well-Architected Framework**
- Engrave the 6 pillars of perfect system design (Best Practices): Operational Excellence, Security, Reliability, Performance, Cost Optimization, and Sustainability. This is the indispensable compass for any future Cloud architecture blueprint.

---

### Hands-on Experience: From Theory to Operation

**Initialization and Base Security Module:**
- **Lab01-01:** Manually accessed [aws.amazon.com/free](https://aws.amazon.com/free) to register an account. I decisively chose the **Paid Plan** to ensure the practice process was not limited. Immediately after, I successfully recorded a $100 credit automatically loaded into the system.
- **Lab01-02:** To protect supreme control rights, I immediately set up an MFA protection shield for the root account via the Authenticator app.
- **Lab01-03:** Adhering to the principle of least privilege, I built an `AdminGroup` and granted this group supreme `AdministratorAccess` power. Then, I initialized a separate IAM User and placed it in the group to use for daily tasks instead of using the Root account.
- **Lab01-04:** Simulated a real-world scenario and proceeded to open a successful account verification case to get familiar with the Support operational process.

**Financial Management Module (AWS Budgets):**
- **Lab07-01 to 07-06:** Comprehensively practiced the cost management system. Started by rapidly deploying a Budget via a Template, then manually configured a Cost Budget with an email alert mechanism when thresholds are exceeded. Continued to operate a Usage Budget to measure resources (compute hours, GB capacity), and deployed advanced Budgets for RI and Savings Plans. Finally, I ensured the clean up principle by deleting all Budgets after testing.

**Campaign to Unlock $200 Credit (5 Challenges):**
- **Challenge 1 (EC2):** Successfully launched an EC2 instance named `Test Instance`, with precise operations from selecting the AMI to configuring the Security Group. I created and downloaded a `first-kp` key (RSA format, .pem) for remote access. Most importantly, I thoroughly cleaned up (Terminated) the resource immediately upon completion and marked the first milestone as complete.
- **Challenge 2 (AI/ML):** Accessed the Bedrock control center and successfully invoked the **Claude 3 Haiku** model. I injected use case data and test-ran a prompt to view the response, thereby hitting the second challenge milestone.
- **Challenge 3 (FinOps):** Cast a protective net with a Cost budget directly connected to my personal email.
- **Challenge 4 (Serverless):** Super-fast deployment of a Lambda function (`http-function-url-tutorial`) from an available blueprint repository, and adhered to the discipline of ruthlessly cleaning up the function immediately after testing.
- **Challenge 5 (Database):** Successfully erected an Aurora cluster (PostgreSQL compatible) using the Easy Create feature. Once the system ran stably, I wiped the DB instance and cluster clean to cut incurred costs.

---

### Operational Difficulties & Solutions Perspective

**Obstacles:**
- Stood frozen for a moment due to confusion between choosing the Free Plan or Paid Plan during the registration phase for fear of incurring unintended costs.
- Blocked by system authorization errors when trying to invoke the Claude 3 Haiku model on Amazon Bedrock.
- Quite overwhelmed and clumsy navigating the massive AWS Console interface during the first few clicks.
- Vague on determining when to use which Budget (Cost, Usage, RI, Savings Plans) in practical scenarios.

**Tactics for Resolution:**
- Stopped to read the feature comparison table between the two Plans very carefully before deciding to ensure the learning path wouldn't be hindered.
- Facing the AI access rights error, I proactively created a Support case (Account & billing > Bedrock Allowlisting) and patiently waited for AWS approval after 24 hours.
- Compensated for unfamiliarity with diligence: clicked and navigated repeatedly on the interface for the brain to memorize service locations.
- Revisited theoretical documents, cross-referenced each Budget type, and slowly re-did each lab myself to deeply understand the nature of cash flow in the Cloud.

---

### Week 1 Experience Summary

- Clearly felt the power of the Cloud platform and understood why AWS is dominating the tech game.
- Formed supreme security awareness: Must **enable MFA** immediately and absolutely hide the Root account, only using an IAM User for daily tasks.
- Engraved the financial lesson: **Setting up a Budget is the first thing to do** to avoid shock when receiving a bill.
- Trained the reflex to **"clean up thoroughly"** resources (like terminating virtual machines, deleting databases) as soon as practice is done.
- Realized that the AWS Well-Architected Framework is the indispensable compass for any future system design blueprint.