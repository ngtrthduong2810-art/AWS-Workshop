---
title: "Worklog Week 8"
date: 2026-06-02
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 8 Objectives: Shifting the Mindset from ClickOps to ScriptOps

Entering the 8th week, the learning focus shifts from manual operations on the web interface (AWS Management Console) to controlling infrastructure with code commands. For a software engineer, mastering the command line is a mandatory stepping stone towards CI/CD automation. The deep-dive objectives include:

- **Discovering Command Line Power:** Learn the overview of the AWS Command Line Interface (AWS CLI) and understand the role of AWS CLI in managing AWS resources quickly and consistently.
- **Standard Environment Setup:** Install and configure AWS CLI on the computer, ensuring secure connectivity to the Cloud.
- **Controlling Infrastructure via Terminal:** Practice checking and managing resources using AWS CLI, completely replacing traditional mouse-click operations.
- **Multi-service Interaction:**
  - Practice working with Amazon S3 via AWS CLI to manage object storage.
  - Learn and use Amazon SNS with AWS CLI to operate pub/sub messaging systems.
  - Practice managing IAM using AWS CLI for security authorization.
  - Learn how to manage Amazon VPC with AWS CLI to query network architecture.
- **Flexible Resource Provisioning:** Initialize and manage Amazon EC2 using AWS CLI.
- **Cleanup Discipline:** Execute resource cleanup after completing the practice using CLI commands themselves to avoid incurring costs.

---

### Tasks to be Implemented this Week:

| Day | Deep-Dive Tasks | Start Date | End Date | Reference Sources |
| --- | --- | --- | --- | --- |
| Mon | - **Foundational Research:** Read the AWS CLI workshop overview. <br> - Evaluate and learn the role of AWS CLI in the automation process. <br> - Prepare the practical environment on the local operating system. | 22/06/2026 | 22/06/2026 | https://000011.awsstudygroup.com/1-introduction/ |
| Tue | - **Authentication Setup:** Install AWS CLI. <br> - Configure Access Key and Region via `aws configure`. <br> - Run API ping commands to check AWS CLI connection. | 23/06/2026 | 23/06/2026 | https://000011.awsstudygroup.com/2-prerequiste/ <br> https://000011.awsstudygroup.com/3-installation/ |
| Wed | - **Resource Exploration:** Use commands to check AWS resource information. <br> - Practice basic AWS CLI commands to get familiar with the `aws <command> <subcommand> [options]` structure. | 24/06/2026 | 24/06/2026 | https://000011.awsstudygroup.com/4-check-resource/ |
| Thu | - **Storage Administration (S3):** Practice managing Amazon S3 using AWS CLI. <br> - Create a Bucket via the command line. <br> - Run sync commands to upload and download data. | 25/06/2026 | 25/06/2026 | https://000011.awsstudygroup.com/5-cli-with-s3/ |
| Fri | - **Notification Administration (SNS):** Practice Amazon SNS using AWS CLI. <br> - Initialize the infrastructure by creating a Topic. <br> - Perform send and check Notification entirely via the terminal. | 26/06/2026 | 26/06/2026 | https://000011.awsstudygroup.com/6-cli-with-sns/ |
| Sat | - **Core Infrastructure Control:** Manage IAM using AWS CLI. <br> - Work with Amazon VPC to export network information. <br> - Directly initialize EC2 using AWS CLI by passing AMI and KeyPair parameters. | 27/06/2026 | 27/06/2026 | https://000011.awsstudygroup.com/7-cli-with-iam/ <br> https://000011.awsstudygroup.com/8-cli-with-vpc/ <br> https://000011.awsstudygroup.com/9-create-ec2/ |
| Sun | - **Evaluation and Cleanup:** Check the created resources. <br> - Perform Cleanup Resources via delete/terminate commands. <br> - Summarize the learned knowledge to consolidate Scripting skills. | 28/06/2026 | 28/06/2026 | https://000011.awsstudygroup.com/11-clean-up/ |

---

### Week 8 Results: Deep-Dive Theoretical Summary

#### 1. Automation Mindset with AWS CLI
I understand AWS CLI is a command-line tool that helps manage and automate AWS services. The biggest difference is that I understand the benefits of using CLI instead of the AWS Management Console in many cases (such as batch deployments, repeating tedious tasks, or integrating into bash scripts). To communicate with AWS, I know how to configure credentials to connect to the AWS account.

This process begins by installing AWS CLI on the operating system. The key is to establish a security profile by configuring the Access Key, Secret Access Key, Region, and Output Format (usually JSON for easy parsing). Finally, I know how to check the connection to the AWS account using CLI commands like `aws sts get-caller-identity`.

#### 2. Storage and Communication Operations (S3 & SNS)
For storage, I know how to create and manage S3 Buckets directly from the terminal. The operations to upload, download, and list objects in the Bucket happen quickly via the `aws s3` command group. Concluding the data lifecycle, I know how to delete data and Buckets using AWS CLI.

For the messaging system, I learned how to create an SNS Topic. Then, I set up receiving devices by registering a Subscription and proactively sending Notifications via AWS CLI.

#### 3. Core Infrastructure Administration (IAM, VPC & EC2)
- **Security:** Working with IAM via the command line helps me quickly list Users, Groups, and Policies. I can manage IAM information using CLI commands and understand how to use CLI to check access permissions of entities.
- **Network:** CLI allows exporting network structures in JSON format. I know how to check VPC information, list Subnets and Security Groups, and manage network resources via AWS CLI to support network troubleshooting.
- **Compute:** This is the most exciting part. Instead of going through multiple configuration screens, I initialized an EC2 Instance using AWS CLI with just a single command line containing the necessary flags. Afterward, I checked the Instance status and performed EC2 management operations from the command line.

---

### Hands-on Experience: Module Analysis

**Module 1 & 2 — Foundations (Introduction & Installation)**
- Started by reading introductory documents on AWS CLI and learning its architecture and operating principles (REST API requests).
- Proceeded to prepare the practical environment, download binaries, and install AWS CLI.
- Established personal identity by configuring AWS account information.
- Used commands to check version and connection.

**Module 3 & 4 — Exploration and Storage (Check Resource & S3)**
- Called APIs to check AWS resource information.
- Practiced basic AWS CLI commands and got familiar with CLI syntax.
- For the storage service, I used the `mb` (make bucket) command to create a Bucket.
- Used `cp` and `sync` to upload and download files. Finally, cleaned up by deleting data in the Bucket.

**Module 5 & 6 — Integration Services (SNS & IAM)**
- Initialized the pub/sub system by creating a Topic.
- Linked endpoints by creating a Subscription and sent a test notification.
- In IAM, I used commands to check Users, list Groups and Policies, and practiced other IAM commands to audit the system.

**Module 7 & 8 — Compute Infrastructure (VPC & EC2)**
- Exported network data by checking VPCs, viewing Subnets, and checking Security Groups.
- Provisioned compute resources using the `run-instances` command to initialize an EC2 Instance.
- Called the `describe-instances` command to check the Instance status and performed EC2 management using AWS CLI.

**Module 9 — Cleanup Discipline (Cleanup Resources)**
- Queried to check all created resources.
- Used `terminate` and `delete` commands to delete resources no longer in use.
- Reran `describe` commands to confirm the completion of Cleanup.

---

### Week 8 Results Evaluation:

- Completely understand the role of AWS CLI in managing AWS services.
- Proficiently executed the installation and configuration of AWS CLI.
- Successfully practiced managing Amazon S3 using CLI.
- Integrated and know how to use AWS CLI with Amazon SNS.
- Exploited data to manage IAM and VPC via the command line.
- Initialized and managed EC2 using AWS CLI rapidly.
- Overall, I have enhanced my skills in using AWS CLI to automate administrative tasks on AWS.

---

### Difficulties and Technical Barriers:

- **Machine Language Barrier:** Initially unfamiliar with AWS CLI syntax and parameters, especially parameters passed as JSON arrays.
- **Memory Conflict:** The vast ecosystem of commands makes it easy to confuse the commands of individual AWS services (e.g., `aws s3` vs. `aws s3api`).
- **Permission Errors:** Cannot execute commands because some operations require appropriate IAM Permission configurations.
- **CLI Inconvenience:** Unlike a GUI, remembering resource names and IDs when operating with CLI is time-consuming (e.g., having to copy/paste VPC IDs, Subnet IDs).

---

### Solutions and Remediation:

- **Build Muscle Memory:** The only way to get good at CLI is to practice AWS CLI commands regularly.
- **Exploit Documentation:** Instead of memorizing, I learned to consult the AWS CLI Command Reference when needed or use the `help` flag.
- **Security First:** Always check IAM Policies before performing operations to ensure the Access Key has sufficient privileges.
- **Build a Personal Library:** Proactively take notes on commonly used commands for convenience during practice.

---

### Optimal Directions for Next Week:

The automation journey will reach a new height. Typing individual CLI commands is still somewhat manual (Imperative). Next week, we will transition to a Declarative model:
- Shift research focus to learn about AWS CloudFormation.
- Apply programming skills to practice creating infrastructure as code.
- Design and deploy AWS resources using Templates (YAML/JSON).
- Learn about Stack management and updating infrastructure safely and controllably.
- Finally, prepare evidence images and complete the practical report for the upcoming week.