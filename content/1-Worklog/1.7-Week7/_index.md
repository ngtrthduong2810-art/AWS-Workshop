---
title: "Worklog Week 7"
date: 2026-05-27
weight: 8
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives: Building the Core Security and Network Foundation

Entering the 7th week, we touch upon the two most critical pillars that determine the security and connectivity of any system in the Cloud: Identity Security and Isolated Network Architecture. The goal this week is to shift the mindset from merely "launching resources" to systematically "protecting and routing" them. Key objectives include:

- **Mastering the Authorization System (IAM):** Learn the overview of AWS Identity and Access Management (IAM) to understand the role of IAM in identity management and authorization on AWS.
- **Establishing Authentication Barricades:** Learn the authentication and account security mechanism with Multi-Factor Authentication (MFA) to protect the account from intrusion risks.
- **Executing Granular Permissions:** Practice creating and managing IAM Users, Groups, Roles, and Policies, while learning security and authorization principles according to the Principle of Least Privilege.
- **Architecting an Independent Virtual Network (VPC):** Learn the overview of Amazon Virtual Private Cloud (Amazon VPC) to understand the network architecture of Amazon VPC and its basic components that constitute a virtual data center.
- **Routing and Network Subnetting:** Practice creating and configuring VPCs, Subnets, Route Tables, and Internet Gateways to control the inbound and outbound network traffic flow.
- **Setting up Multi-layer Firewalls:** Practice configuring Security Groups and Network ACLs to protect servers at the network level, thereby improving security and network infrastructure management skills on AWS.

---

### Tasks to be Implemented this Week:

| Day | Deep-Dive Tasks | Start Date | End Date | Reference Sources |
| --- | --- | --- | --- | --- |
| Mon | - **IAM Foundational Research:** Read the AWS IAM workshop overview. <br> - Deepen theory to understand the role of IAM in AWS. <br> - Begin to prepare the practical environment. | 15/06/2026 | 15/06/2026 | https://000009.awsstudygroup.com/ |
| Tue | - **Identity and Authorization:** Learn about IAM Users, Groups, Roles, and Policies. <br> - Directly practice creating Users and Groups to organize virtual personnel. <br> - Grant permissions using Managed Policies to leverage standard AWS rule sets. | 16/06/2026 | 16/06/2026 | https://000009.awsstudygroup.com/ |
| Wed | - **Fortifying Account Security:** Learn about Multi-Factor Authentication (MFA). <br> - Directly configure MFA for the account. <br> - Research AWS security principles to form a DevSecOps mindset. | 17/06/2026 | 17/06/2026 | https://000009.awsstudygroup.com/ |
| Thu | - **Network Foundational Research:** Read the Amazon VPC workshop overview. <br> - Analyze theory and learn about VPC network architecture. <br> - Get familiar with network components such as IP, Subnet, Routing. | 18/06/2026 | 18/06/2026 | https://000010.awsstudygroup.com/ |
| Fri | - **Virtual Network Creation:** Proceed to create a Virtual Private Cloud (VPC). <br> - Partition the network by configuring Public and Private Subnets. <br> - Set up an Internet Gateway and Route Table to pave the way for Internet communication. | 19/06/2026 | 19/06/2026 | https://000010.awsstudygroup.com/ |
| Sat | - **Firewall Configuration:** Configure Security Groups and Network ACLs. <br> - Check the connection between resources using ping/ssh commands. <br> - Troubleshoot errors and complete the network configuration. | 20/06/2026 | 20/06/2026 | https://000010.awsstudygroup.com/ |
| Sun | - **Evaluation and Cleanup:** Check the created resources. <br> - Execute Cleanup Resources to optimize lab costs. <br> - Write a report and summarize the knowledge learned during the week. | 21/06/2026 | 21/06/2026 | https://000009.awsstudygroup.com/ <br> https://000010.awsstudygroup.com/ |

---

### Week 7 Results: Deep-Dive Theoretical Summary

#### 1. Security Architecture (AWS IAM & Account Security)
The first core knowledge I mastered was understanding IAM is the identity and access management service on AWS. I learned how to create and manage IAM Users, Groups, Roles, and Policies. My security mindset was upgraded by understanding the Principle of Least Privilege, ensuring every entity has exactly the right amount of permissions to work, no more, no less.

Additionally, I gained the ability to distinguish between AWS Managed Policies and Customer Managed Policies, and understood how to manage credentials and access rights. To protect the outermost boundary, I understand the role of Multi-Factor Authentication (MFA) and know how to configure MFA for an AWS account. Consequently, I firmly grasp and understand account security principles and credentials, specifically knowing how to protect the Root account and IAM Users.

#### 2. Network Infrastructure Architecture (Amazon VPC & Network Security)
I understand the architecture and functions of Amazon VPC, which acts as a miniature data center in the cloud. Grasping the concept of CIDR Blocks, Subnets, and IP addresses helped me plan the network space logically. Furthermore, I understand the role of the Internet Gateway and Route Table in guiding data packets, enabling me to clearly distinguish between Public Subnets and Private Subnets.

Regarding the protection of network traffic, I understand the function of Security Groups (operating at the instance level) and understand the operating mechanism of Network ACLs (operating at the subnet level). I know how to configure Inbound and Outbound rules to strictly control data ingress and egress. Ultimately, I understand the principles of building secure network systems on AWS.

---

### Hands-on Experience: Module Analysis

**Module 1 — AWS IAM**
- Log in and access the IAM service.
- Create IAM Users and Groups, organizing users into function-based groups.
- Assign permissions using Managed Policies instead of granting permissions directly to individuals.
- Create an IAM Role to grant temporary permissions to services (e.g., EC2) to call APIs.
- Enhance security by configuring Multi-Factor Authentication (MFA) via an Authenticator app.
- Check access permissions to confirm the policies work correctly.

**Module 2 — AWS Security**
- Spend time to learn about security principles on AWS.
- Set up and configure secure authentication methods.
- Strictly apply the principle of least privilege in all policies.
- Proactively check the account security configuration via the IAM Security Status.

**Module 3 — Amazon VPC**
- Read documentation to learn about Amazon VPC architecture.
- Directly initialize a Virtual Private Cloud with a custom CIDR range.
- Separate the architecture by creating Public and Private Subnets.
- Open communication channels by configuring an Internet Gateway and setting up Route Tables.

**Module 4 — Network Security**
- Create and configure Security Groups to open ports 22 (SSH) and 80 (HTTP).
- Add a network defense layer by setting up Network ACLs.
- Launch virtual machines and check network connectivity.
- Use diagnostic tools to verify the operation of network components.

**Module 5 — Cleanup Resources**
- Ensure no hidden costs are generated by checking all created resources.
- Delete resources that are no longer used in the correct order (delete Instances -> delete Subnets/IGW -> delete VPC).
- Confirm the completion of the cleanup process.

---

### Week 7 Results Evaluation:

- Understood the role of AWS IAM in identity management and authorization.
- Successfully created and managed IAM Users, Groups, Roles, and Policies.
- Successfully configured Multi-Factor Authentication (MFA).
- Understood AWS account security principles.
- Successfully created and configured Amazon VPC.
- Set up Public Subnets, Private Subnets, Route Tables, and Internet Gateways to form a closed network system.
- Configured Security Groups and Network ACLs to protect the system.
- Thereby, improved skills in managing security and network infrastructure on the AWS platform.

---

### Difficulties and Technical Barriers:

- **Identity Concepts:** Initially, it was hard to distinguish between IAM Roles and IAM Users in some use cases.
- **Authorization Mechanisms:** Due to the abundance of policy types, I was initially confused between Managed Policies and Inline Policies.
- **Multi-layer Firewalls:** Distinguishing between Security Groups and Network ACLs was still unclear (one is stateful, the other is stateless).
- **Network Planning:** It took time to understand how Route Tables and CIDR Blocks work because it requires complex subnet mask calculations.
- **Troubleshooting:** Encountered some connection errors due to incorrect network configurations (forgot to attach the Route Table to the Subnet or accidentally blocked ports in NACL).

---

### Solutions and Remediation:

- **Supplement Theory:** Read the AWS Study Group materials and AWS Documentation carefully to systematize knowledge.
- **Skill Practice:** Practice creating Users, Groups, Roles, and Policies multiple times to get used to the interface and authorization logic.
- **Visualization:** Draw VPC architecture diagrams to easily visualize connection flows, ensuring no gateways are missed.
- **Inspection Checklist:** Before testing the network, thoroughly check Route Tables, Security Groups, and Network ACLs before testing.
- **Standard Compliance:** Resolutely apply the Least Privilege principle during the authorization process, even if granting full (Admin) rights seems like an easier way to bypass initial errors.

---

### Optimal Directions for Next Week:

After building the network and security infrastructure via the Console interface, the next step is to move towards automation and professional operations using the Command Line.
- Learn about the AWS Command Line Interface (AWS CLI).
- Proceed to install and configure AWS CLI on a personal computer.
- Upgrade skills by practicing managing AWS resources using the command line.
- Integrate and work with Amazon S3, SNS, IAM, VPC, and EC2 via AWS CLI.
- Finally, always prepare evidence images and complete the practical report for the following week.