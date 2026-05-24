---
title: "Worklog Week 1"
date: 2026-04-20
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:

- Get familiar with the internship environment and members of the First Cloud Journey program.
- Understand fundamental concepts of Cloud Computing and the AWS service ecosystem.
- Gain a clear understanding of AWS global infrastructure, management tools, and cost optimization strategies.

- Create an AWS Free Tier 2025 account and receive the full $200 credit.
- Complete hands-on labs related to account setup, security, and budget management.

---

### Weekly Tasks:

| Day | Tasks | Start Date | End Date | Resources |
|-----|------|------------|----------|-----------|
| 2 | - Get familiar with FCJ members <br> - Review internship rules and regulations | 20/04/2026 | 20/04/2026 | https://www.notion.so/Group-description-TP-HCM-347df829a730809a8f63d39505644917 |
| 3 | - Module 01-01: What is Cloud Computing? <br> - Module 01-02: What Makes AWS Different? <br> - Module 01-03: How to Start Your Cloud Journey <br> - Module 01-04: AWS Global Infrastructure | 21/04/2026 | 21/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Module 01-05: AWS Service Management Tools <br> - Module 01-06: Cost Optimization & Working with AWS Support <br> - Module 01-07: Practice and Additional Research <br> - **Hands-on:** <br>&nbsp;&nbsp;+ Lab01-01: Create AWS Account <br>&nbsp;&nbsp;+ Lab01-02: Set up Virtual MFA Device <br>&nbsp;&nbsp;+ Lab01-03: Create Admin Group and Admin User <br>&nbsp;&nbsp;+ Lab01-04: Account Verification Support | 22/04/2026 | 22/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | - **Budget Practice:** <br>&nbsp;&nbsp;+ Lab07-01: Create Budget from Template <br>&nbsp;&nbsp;+ Lab07-02: Create Cost Budget <br>&nbsp;&nbsp;+ Lab07-03: Create Usage Budget <br>&nbsp;&nbsp;+ Lab07-04: Create Reserved Instance Budget <br>&nbsp;&nbsp;+ Lab07-05: Create Savings Plans Budget <br>&nbsp;&nbsp;+ Lab07-06: Clean up Budgets <br> - **Support Practice:** <br>&nbsp;&nbsp;+ Lab09-01: AWS Support Plans <br>&nbsp;&nbsp;+ Lab09-02: Types of Support Cases <br>&nbsp;&nbsp;+ Lab09-03: Change Support Plan <br>&nbsp;&nbsp;+ Lab09-04: Manage Support Cases | 23/04/2026 | 23/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Complete 5 tasks to earn $200 credit: <br>&nbsp;&nbsp;+ Launch EC2 Instance (+$20) <br>&nbsp;&nbsp;+ Amazon Bedrock Playground (+$20) <br>&nbsp;&nbsp;+ Set up AWS Budgets (+$20) <br>&nbsp;&nbsp;+ Create Lambda Web App (+$20) <br>&nbsp;&nbsp;+ Create RDS Database (+$20) <br> - Additional research: AWS Well-Architected Framework | 24/04/2026 | 24/04/2026 | https://000001.awsstudygroup.com/ <br> https://docs.aws.amazon.com/wellarchitected/ |
---

### Week 1 Results:

#### Knowledge

**Module 01-01 — What is Cloud Computing?**

- Understand Cloud Computing concepts: on-demand, pay-as-you-go.
- Differentiate service models: IaaS, PaaS, SaaS.
- Understand deployment models: Public Cloud, Private Cloud, Hybrid Cloud.

**Module 01-02 — What Makes AWS Different?**

- AWS is the world’s leading cloud provider with 200+ services.
- Key advantages: high availability, security, flexibility, cost efficiency.
- Understand core service groups:
  - Compute (EC2, Lambda)
  - Storage (S3, EBS)
  - Networking (VPC, Security Group)
  - Database (RDS, Aurora)
  - AI/ML (Amazon Bedrock)

**Module 01-03 — How to Start Your Cloud Journey**

- Understand the AWS learning path from beginner to advanced.
- Learn about AWS Free Tier 2025:
  - $100 credit upon account creation
  - Additional $100 from completing 5 tasks
  - Two options: Free Plan (6-month protection) and Paid Plan (full access)

**Module 01-04 — AWS Global Infrastructure**

- AWS operates across multiple Regions and Availability Zones worldwide.
- Understand Region, AZ, and Edge Location concepts.
- Learn how to choose the appropriate Region (latency, cost, compliance).

**Module 01-05 — AWS Service Management Tools**

- AWS Management Console (web interface)
- AWS CLI (command line)
- AWS SDK (integration with code)
- AWS CloudShell

**Module 01-06 — Cost Optimization & AWS Support**

- Cost management tools: AWS Budgets, Cost Explorer, Cost & Usage Reports.
- Cost-saving strategies: Reserved Instances, Savings Plans, Spot Instances.
- AWS Support plans: Basic, Developer, Business, Enterprise.
- How to create and manage support cases.

**Additional Research — AWS Well-Architected Framework**

- 6 pillars: Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, Sustainability.

---

#### Hands-on Practice

**Lab01-01 — Create AWS Account:**

- Access [aws.amazon.com/free](https://aws.amazon.com/free) and create a new account.
- Select **Paid Plan** for full service access.
- Receive $100 credit after successful account creation.
- 📸 _Evidence: AWS Console after first login._  
- 📸 _Evidence: Billing Console showing $100 credit._

**Lab01-02 — Set up Virtual MFA Device:**

- Enable MFA for root account using an authenticator app.
- 📸 _Evidence: MFA successfully enabled screen._

**Lab01-03 — Create Admin Group and User:**

- Create IAM Group `AdminGroup` with `AdministratorAccess`.
- Create IAM User and assign to group.
- 📸 _Evidence: IAM Users and Groups in Console._

**Lab01-04 — Account Verification Support:**

- Practice contacting AWS Support for account verification.
- 📸 _Evidence: Support case created successfully._

**Lab07 — AWS Budgets Practice:**

- Create various budgets: Cost, Usage, RI, Savings Plans.
- Configure email alerts.
- Clean up resources after practice.
- 📸 _Evidence: Budgets list in AWS Console._

**Lab09 — AWS Support Practice:**

- Explore support plans and case types.
- Create and manage support cases.
- 📸 _Evidence: Support case dashboard._

---

#### $200 Credit Tasks

- **Task 1 — Launch EC2 Instance (+$20):**
  - Create EC2 instance `Test Instance`
  - Configure Security Group and key pair (`first-kp`)
  - Terminate after use (clean up)
  - 📸 _Evidence: EC2 instance running_

- **Task 2 — Amazon Bedrock Playground (+$20):**
  - Use **Claude 3 Haiku** model
  - Test prompts
  - 📸 _Evidence: Bedrock response_

- **Task 3 — Set up AWS Budgets (+$20):**
  - Create cost budget with alerts
  - 📸 _Evidence: Budget created_

- **Task 4 — Create Lambda Web App (+$20):**
  - Create Lambda function from blueprint
  - Delete after use
  - 📸 _Evidence: Lambda created_

- **Task 5 — Create RDS Database (+$20):**
  - Create Aurora PostgreSQL database
  - Delete after use
  - 📸 _Evidence: RDS Available_

- 📸 _Final Evidence: Billing Console showing full $200 credit_

---

#### Challenges & Solutions

**Challenges:**

- Confusion between Free Plan and Paid Plan.
- Authorization error when accessing Amazon Bedrock.
- Difficulty navigating AWS Console initially.
- Confusion between different Budget types.

**Solutions:**

- Reviewed documentation before account setup.
- Submitted AWS Support case for Bedrock allowlisting.
- Practiced regularly to become familiar with the Console.
- Studied each Budget type and practiced step-by-step.

---

#### Evidence

- 📸 AWS Console (first login)
- 📸 $100 credit in Billing
- 📸 MFA enabled
- 📸 IAM setup
- 📸 Budgets created
- 📸 Support cases
- 📸 EC2 running
- 📸 Bedrock response
- 📸 Lambda created
- 📸 RDS available
- 📸 Full $200 credit

---

#### Lessons Learned

- Gained a solid understanding of Cloud Computing and AWS ecosystem.
- Always enable MFA and use IAM users instead of root account.
- Set up Budgets early to avoid unexpected costs.
- Always clean up resources after use.
- AWS Well-Architected Framework is essential for designing cloud systems.