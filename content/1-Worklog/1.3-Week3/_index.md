---
title: "Worklog Week 3"
date: 2026-04-28
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives: Mastering Compute Capacity and Server Operations

After successfully building the network infrastructure last week, week 3 is a crucial step into deploying and operating Compute blocks on the cloud. The core objective is not just knowing how to turn a server on/off, but deeply understanding its lifecycle, how to optimize it, and instance-level security. Deep-dive objectives include:

- **Explore compute capacity:** Learn the overview of Amazon EC2 and its role in the Cloud infrastructure as the core processing engine of every application.
- **Build security barriers:** Practice creating VPCs and Security Groups for Linux and Windows Instances to establish strict server-level firewall rules.
- **System Operations:** Directly initialize, connect to, and manage EC2 Instances on AWS using the two most popular operating system platforms.
- **Master advanced administration:** Get familiar with basic operations: changing Instance Types, creating Snapshots, creating AMIs, and recovering access to ensure Business Continuity.
- **Practical Software Deployment:** Utilize the newly created environment to test deploy the AWS User Management application on Linux and Windows Servers, evaluating the differences between the two ecosystems.
- **Establish Operational Discipline (Governance):** Practice managing costs and EC2 usage rights using IAM Policies to prevent resource abuse.
- **Budget Optimization:** Maintain the habit of cleaning up resources after completing the lab to avoid incurring costs.

---

### Tasks to be Implemented this Week:

| Day | Deep-Dive Tasks | Start Date | End Date | Reference Sources |
| --- | --- | --- | --- | --- |
| Mon | - **Foundational Research:** Read the Introduction section of Amazon EC2. <br> - Grasp the workshop overview and practical architecture. <br> - Ensure readiness by preparing the AWS account, Region, Key Pair, and connection environment. | 04/05/2026 | 04/05/2026 | https://000004.awsstudygroup.com/ |
| Tue | - **Network & Security Creation:** Module 2.1: Create a Linux VPC. <br> - Module 2.2: Create VPC for Windows Instance. <br> - Module 2.3: Create Security Group for Linux Instance. <br> - Module 2.4: Create Security Group for Windows Instance. | 05/05/2026 | 05/05/2026 | https://000004.awsstudygroup.com/ |
| Wed | - **Windows Server Deployment:** Module 3.1: Launch Microsoft Windows Server 2022 Instance. <br> - Module 3.2: Connect from Computer to Windows Instance. <br> - Perform Remote Desktop checking and Windows login key pair operations. | 06/05/2026 | 06/05/2026 | https://000004.awsstudygroup.com/ |
| Thu | - **Linux Server Deployment:** Module 4.1: Launch Amazon Linux Instance. <br> - Module 4.2: Connect to Amazon Linux Instance. <br> - Proceed to practice SSHing into the Linux Instance using the key pair. | 07/05/2026 | 07/05/2026 | https://000004.awsstudygroup.com/ |
| Fri | - **EC2 Lifecycle Administration:** Module 5.1: Modify EC2 Instance Type. <br> - Module 5.2: Create and Manage EBS Snapshots. <br> - Exploit AMI power: Module 5.3: Create Custom AMI and Module 5.4: Launch Instance from Custom AMI. <br> - Troubleshooting: Module 5.5 - 5.7: Recover access and Remote Desktop Ubuntu. | 08/05/2026 | 08/05/2026 | https://000004.awsstudygroup.com/ |
| Sat | - **Application Deployment (Linux):** Module 6: Deploy AWS User Management Application on Amazon Linux. <br> - Build the environment: install LAMP Server, configure database, phpMyAdmin, Node.js, and deploy the app. | 09/05/2026 | 09/05/2026 | https://000004.awsstudygroup.com/ |
| Sun | - **Application Deployment (Windows) & Admin:** Module 7: Deploy Node.js Application on Windows EC2. <br> - Establish barriers: Module 8: Cost & Usage Governance with IAM. <br> - Financial Discipline: Module 9: Clean up resources. | 10/05/2026 | 10/05/2026 | https://000004.awsstudygroup.com/ |

---

### Week 3 Results: Deep-Dive Theoretical Summary

#### 1. Cloud Computing Architecture (Amazon EC2)
The most important foundational knowledge I grasped is understanding Amazon EC2 is a service providing virtual servers on AWS. It's not just a computer; EC2 allows creating, configuring, connecting to, and managing servers on demand with unlimited scalability. The flexibility of EC2 lies in its ability to run various operating systems such as Amazon Linux, Ubuntu, and Windows Server. I noticed EC2 is often used to deploy web servers, backends, test databases, internal applications, or lab environments.

What dictates EC2's power is the Instance Type. I understood that the Instance Type determines the CPU, RAM, network, and processing capabilities of the server. Unlike physical servers, on the Cloud, you can stop the instance then change the Instance Type when you need to upgrade or downgrade the configuration (Scale Up/Down) in just a few minutes. Therefore, choosing the Instance Type should be based on actual needs and costs.

#### 2. Server-Level Firewalls (Security Group) and Secure Connections
Even though the server is in a VPC, it still needs direct protection. I understood VPC is a virtual private network used to isolate resources on AWS and know how to create separate VPCs for Linux Instances and Windows Instances. More importantly, I understand a Security Group operates as an instance-level firewall (Stateful firewall).

Access control requires high precision. I know how to open appropriate ports for each protocol:
- **Remote Administration:** SSH: `22` for Linux and RDP: `3389` for Windows.
- **Web Application Access:** HTTP: `80` for web servers and HTTPS: `443` for secure web traffic.

Regarding identity authentication, Key Pairs are used for authentication when accessing EC2. The operating mechanism differs by OS: for Linux, use the `.pem` file to SSH; whereas for Windows, use the key pair to decrypt the password then connect using Remote Desktop. A valuable lesson learned is that if you lose the key pair, you need to use recovery methods like Systems Manager or attach the volume to another instance to salvage data.

#### 3. Backup, Recovery, and Environment Packaging (Snapshot & AMI)
In a production environment, data is the lifeline. I thoroughly understand the EBS Snapshot mechanism used to back up volumes in a point-in-time format. To rapidly deploy identical server fleets, Custom AMIs are used to create an image from an already configured instance. Consequently, we can launch new instances from the AMI to reuse the installed environment without needing to reconfigure from scratch (Golden Image).

#### 4. Compliance and Cost Governance
Granting unrestricted server creation rights will lead to financial disaster. I know how to use IAM Policies to limit service usage rights. Specifically, I can restrict EC2 creation by Region, Instance Family, or Instance Type (e.g., only allowing t3.micro creation for learning). Furthermore, I can control resource deletion rights by IP or time to prevent sabotage. Through this, I understand the importance of governance to avoid resource abuse and cost overruns.

---

### Hands-on Experience: Module Analysis

**Module 2 — Infrastructure Preparation (Preparation)**
- Designed the network by creating a VPC for the Linux Instance and creating a VPC for the Windows Instance.
- Managed risk by creating a Security Group for Linux: set rules allowing SSH from my personal IP (blocking all unknown IPs completely) and allowing HTTP if needing to run a web server.
- Similarly, created a Security Group for Windows: configured to allow RDP from my personal IP and adhered to the security principle of not opening `0.0.0.0/0` if unnecessary.

**Module 3 & 4 — Launching Multi-Platform Servers**
- **Windows:** Started by selecting the Microsoft Windows Server 2022 AMI and selecting an Instance Type appropriate for Free Tier or labs. I assigned a Key Pair to be able to retrieve the password and configured the Security Group to allow RDP. After initializing the Windows EC2 Instance, I performed password decryption using the key pair file and connected to the Windows Instance using Remote Desktop.
- **Linux:** A similar but more streamlined process. Selected the Amazon Linux AMI, selected an appropriate Instance Type, assigned a Key Pair, and configured the Security Group to allow SSH. After initializing the Linux EC2 Instance, I used terminal commands to SSH connect to the instance.

**Module 5 — Advanced EC2 Administration (Amazon EC2 Basic)**
- Practiced hardware flexibility by changing the Instance Type.
- Ensured data safety by creating and managing EBS Snapshots.
- Packaged the application by creating a Custom AMI from the configured EC2 Instance and successfully launching a new EC2 Instance from the Custom AMI.
- Honed troubleshooting skills: learned how to recover access to a Windows Instance and learned how to recover access to a Linux Instance. Simultaneously, tested Remote Desktop practice into Ubuntu EC2 with a GUI.

**Module 6 & 7 — Practical Application Deployment**
- **On Linux:** I manually installed the LAMP Web Server, then verified Apache/PHP was running smoothly. Continued to configure the database server, install phpMyAdmin, and install Node.js on Amazon Linux. Finally, I deployed the AWS User Management application and tested the application's basic CRUD functions.
- **On Windows:** Tested a different ecosystem by installing XAMPP on the Windows Instance and installing Node.js on the Windows Instance. I proceeded to deploy the AWS User Management Application on Windows Server and tested the application via the browser to compare performance.

**Module 8 & 9 — Risk Management and Cleanup (Governance & Clean up)**
- Directly wrote IAM JSON to create an IAM Policy limiting service usage by Region, create a Policy limiting EC2 by Instance Family, along with creating a Policy limiting EC2 by Instance Type. I also created a Policy managing allowed EBS Volume types. To prevent accidental resource deletion, I created a Policy limiting resource deletion rights by company IP and created a Policy limiting resource deletion rights by time.
- In the final step, I terminated EC2 Instances no longer in use, deleted unnecessary EBS Volumes, deleted Snapshots if no longer needed, and deleted AMIs created during the lab. To complete the process, I deleted Security Groups, VPCs, or auxiliary resources if no longer needed and carefully checked the Billing Dashboard after cleanup.

---

### Difficulties and Technical Barriers:

- **Tangled Network Architecture:** For beginners, initially, it's easy to confuse VPC, Subnet, and Security Group when designing isolated architectures.
- **Authentication Security:** Complex operation when connecting to a Windows Instance, requiring password decryption using the exact key pair. Meanwhile, when SSHing into Linux, it's easy to get an error due to incorrect permissions on the `.pem` file.
- **Traffic Flow:** If the wrong port or source IP is opened in the Security Group, connection is impossible (Time out error).
- **Financial Risks:** Some resources like EBS Snapshots, AMIs, Elastic IPs can incur costs if forgotten to be deleted, as they operate in the background even if the server is stopped.
- **Programming Environment:** When deploying the app, one might encounter package, firewall, port, or database connection errors, demanding system troubleshooting skills.

---

### Solutions and Best Practices:

- **Design Thinking:** Always use pen and paper to re-check the network architecture before launching an instance to ensure accurate routing flows.
- **Naming Convention:** Avoid "orphaned" resources by naming resources clearly according to a format (e.g., `fcj-linux-vpc`, `fcj-windows-vpc`, `fcj-linux-sg`, `fcj-windows-sg`).
- **Zero-Trust Security:** Resolutely only open SSH/RDP to personal IPs, restrict opening to the entire Internet (0.0.0.0/0).
- **OS Security Compliance:** With Linux, run the key pair permission command before SSH. The mandatory command is: `chmod 400 first-kp.pem` to lock read/write access from other users.

---

### Optimal Directions for Next Week:

The journey to conquer the Cloud will transition into the cost optimization and automated alerting phase.
- Approach the AWS Budgets financial management system to set up deep financial barriers.
- Learn how to differentiate between Cost Budgets and Usage Budgets.
- Explore Amazon CloudWatch to set up Alarms based on the consumption performance of EC2 servers.
- Prepare the foundation to build a CloudWatch Dashboard, visualizing the health of the entire infrastructure built over the past 3 weeks.