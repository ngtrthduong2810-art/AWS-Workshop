---
title: "Worklog Week 2"
date: 2026-04-24
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives: Establishing Network Infrastructure and Access Control

After familiarizing with basic concepts in the first week, week 2 focuses on building the "skeleton" of every system on AWS: Networking. The goal is not just to create a network, but to design it securely, efficiently, and cost-effectively. Deep-dive objectives include:

- **Explore the networking platform:** Learn the overview of Amazon VPC and core components in AWS network infrastructure (Subnet, Route Table, Internet Gateway, NAT Gateway).
- **Design High Availability (HA) architecture:** Set up a VPC network system distributed across 2 Availability Zones (AZs) meeting Public and Private Subnet standards.
- **Evaluate access methods:** Practice and compare 3 secure authentication and connection methods to a Private EC2 Instance: SSH via Bastion Host, EC2 Instance Connect (EIC) Endpoint, and AWS Systems Manager (SSM) Session Manager.
- **Master diagnostic tools:** Get familiar with the VPC Reachability Analyzer tool to check and debug the logical path of network traffic.
- **Budget Control (FinOps):** Enhance Cost Optimization thinking by managing and cleaning up cost-incurring network resources after completing the lab.

---

### Tasks to be Implemented this Week:

| Day | Deep-Dive Tasks | Start Date | End Date | Reference Sources |
| --- | --- | --- | --- | --- |
| Mon | - **Foundational Research:** Prepare AWS account, select Region `us-east-1`. <br> - Read overview documentation on Amazon VPC network and AWS VPN Site-to-Site. <br> - Prepare Key Pair and connection environment. | 27/04/2026 | 27/04/2026 | https://000003.awsstudygroup.com/vi/ |
| Tue | - **Core Network Design:** Set up core VPC infrastructure (CIDR `10.10.0.0/16`). <br> - Create 4 Subnets distributed across 2 Availability Zones (AZ 1a, 1b). <br> - Initialize and attach an Internet Gateway (IGW) to the VPC. | 28/04/2026 | 28/04/2026 | https://000003.awsstudygroup.com/vi/ |
| Wed | - **Network Traffic Routing:** Deploy a NAT Gateway in Public Subnet 1 in Zonal mode. <br> - Allocate and attach an Elastic IP to the NAT Gateway. <br> - Configure Route Tables for Public and Private Subnets. | 29/04/2026 | 29/04/2026 | https://000003.awsstudygroup.com/vi/ |
| Thu | - **Traditional Connection Testing:** Initialize Public and Private EC2 instances (t3.micro, Amazon Linux 2023). <br> - Perform traditional connection operation via SSH Jump through a Bastion Host. <br> - Check network activity of the Private Subnet via NAT Gateway using the internet ping command. | 30/04/2026 | 30/04/2026 | https://000003.awsstudygroup.com/vi/ |
| Fri | - **Advanced Network Diagnostics:** Use the VPC Reachability Analyzer tool to check network connectivity. <br> - Analyze the logical path of data packets between Public EC2 and Private EC2. | 01/05/2026 | 01/05/2026 | https://000003.awsstudygroup.com/vi/ |
| Sat | - **EIC Endpoint Deployment:** Initialize and configure the EC2 Instance Connect (EIC) Endpoint service in the Private Subnet. <br> - Configure Security Group and test direct connection to Private EC2 without going through public internet. | 02/05/2026 | 02/05/2026 | https://000003.awsstudygroup.com/vi/ |
| Sun | - **Zero Trust Deployment & Cleanup:** Configure IAM Role and set up 3 VPC Interface Endpoints to run SSM Session Manager. <br> - Practice direct Shell management connection via web browser. <br> - Proceed to clean up resources to optimize system costs. | 03/05/2026 | 03/05/2026 | https://000003.awsstudygroup.com/vi/ |

---

### Week 2 Results: Deep-Dive Theoretical Summary

#### 1. Amazon VPC and Subnetting
The core concept I grasped is understanding VPC is a virtual private network that completely isolates your resources on the AWS cloud computing infrastructure. This provides security equivalent to a traditional on-premise data center.

I clearly distinguished the characteristics of a Public Subnet (attached to an Internet Gateway) and a Private Subnet (only connecting internally or to the internet via a NAT mechanism). This separation is crucial: servers directly interacting with users (like Web Servers) reside in the Public subnet, while Databases or sensitive backend logic must be hidden in a Private Subnet.

To control traffic flow, I understand the Route Table acts as a "signpost" system routing packets. Specifically, I noted the default route `10.10.0.0/16 -> local` ensures all internal traffic always travels through AWS's secure backbone infrastructure, preventing leakage to the public network.

#### 2. Connection Gateways: Internet Gateway and NAT Gateway
These two Gateways serve entirely different purposes:
- An Internet Gateway (IGW) acts as a two-way gate (Inbound and Outbound) allowing Public Subnets to connect directly to the public Internet.
- In contrast, a NAT Gateway is a one-way gate (Outbound-only) that helps servers in a Private Subnet go out to the Internet (to update software, download libraries, call APIs) but completely blocks reverse ingress from the outside. This is an excellent layer of protection. I also mastered the newly updated Availability mode configuration (Regional vs. Zonal) of the NAT Gateway and clearly understand the nature of fault tolerance (HA) in an actual Production environment.

#### 3. Connection Analysis with VPC Reachability Analyzer
When networks become complex, debugging with the `ping` command is insufficient. I know how to use the VPC Reachability Analyzer tool to analyze the "logical" network connectivity between cloud resources without actually sending data packets. This tool simulates the data path, helping to isolate and quickly debug barriers caused by misconfigurations in Route Tables, Security Groups, or Network ACLs (NACL).

#### 4. Evolution in EC2 Management Methods
I experienced the evolution of secure connection methods:
- **SSH Jump via Bastion Host (Traditional):** Use a Public EC2 instance as a transit station to connect. While effective, this solution requires users to manually manage key pair files, open port 22 to the internet, and strictly adhere to file permission configurations (`chmod 400`).
- **EC2 Instance Connect (EIC) Endpoint (Modern):** A virtual endpoint managed directly by AWS within the VPC, helping to establish an SSH session via AWS's internal backbone network. The biggest advantage is it's completely free, requires no Public IP, NAT Gateway, or Bastion host, and has built-in audit logging via CloudTrail.
- **SSM Session Manager (Zero Trust):** Allows accessing and opening an EC2 management terminal directly right on a web browser via the SSM Agent mechanism and an IAM Role (`AmazonSSMManagedInstanceCore`). This method achieves maximum security as it requires opening no inbound ports to the public Internet. However, it requires investing in fixed costs for Interface Endpoints (`ssm`, `ssmmessages`, `ec2messages`).

#### 5. Cost Optimization Discipline
Through the lab, I understand the importance of cost optimization thinking on the Cloud. Specifically, identifying silent budget-draining resources like NAT Gateways (~$32/month), Interface Endpoints, or hanging Elastic IPs not attached to any resource to perform timely cleanup.

---

### Hands-on Experience: Module Analysis

**Module 1 — Building Core VPC Network Infrastructure**
- Started by setting up a VPC network system with CIDR block `10.10.0.0/16` in the `us-east-1` (N. Virginia) region.
- To ensure high availability, I successfully allocated 4 Subnets evenly distributed across 2 Availability Zones (1a, 1b) meeting Public and Private Subnet configurations.
- Created and attached an Internet Gateway (IGW) directly to the VPC to grant internet access to the Public zone.
- Successfully initialized a NAT Gateway located in Public Subnet 1 in Zonal mode and associated it with an Elastic IP.
- Finally, I accurately configured the `Route table-Public` pointing the default route `0.0.0.0/0` to the IGW and the `Route table-Private` pointing route `0.0.0.0/0` to the NAT Gateway system.

**Module 2 — Testing Traditional Connection Authentication via Bastion Host**
- Successfully launched 2 EC2 Instances (`t3.micro`, Amazon Linux 2023) including one Public instance (`10.10.1.131`) and one Private instance (`10.10.3.142`) sharing the `aws-keypair-v2` key pair.
- Configured transit SSH from my personal computer through the Bastion Host to access the terminal into the Private EC2. Here, I executed the secure command `chmod 400` for the `.pem` key file.
- Ran the test command `ping -c 4 google.com` on the Private instance to confirm network packets pass through the NAT Gateway and receive a successful response.

**Module 3 — Network Connectivity Debugging with VPC Reachability Analyzer**
- Initialized an analysis to check the data flow path from the Public EC2 instance to the Private EC2 instance.
- By doing so, I checked Security Group rules and received a system analysis result indicating a `Reachable` state.

**Module 4 — Deploying Connection Solution using EC2 Instance Connect (EIC) Endpoint**
- Created an EIC Endpoint (`eice-0f7c...`) located in the Private Subnet network range.
- Proceeded to update the Inbound rule on the Private EC2's Security Group, only accepting port 22 access originating from the EIC Endpoint's own Security Group.
- Established direct SSH connection to the Private EC2's operating system from the AWS Console without going through the public internet environment or Bastion Host.

**Module 5 — Establishing Zero Trust Solution with SSM Session Manager**
- Created an IAM Role granting cloud system management rights containing the `AmazonSSMManagedInstanceCore` managed policy and attached it directly to both EC2 servers.
- Established 3 VPC Interface Endpoints (`ssm`, `ssmmessages`, `ec2messages`) using AWS PrivateLink located in the Private Subnet, enabled the Enable DNS name option, and opened inbound port 443 for the entire `10.10.0.0/16` network range.
- Logged in to control the Private EC2 server via the Session Manager feature directly on the web browser interface without needing a key pair or opening an SSH port.

**Module 6 — Executing Resource Cleanup**
- Performed deletion of the NAT Gateway to stop hourly system charging.
- Completely released empty Elastic IPs to avoid incurring costs for hanging IP resources.
- Completely deleted the 3 SSM VPC Interface Endpoints established for the lab.
- Retained the core VPC system and EIC Endpoint (completely free) to reuse for upcoming weekly labs.

---

### Difficulties and Technical Barriers:

- **Routing Logic:** Easily confused about the operational nature and how to configure routing tables between an Internet Gateway (two-way) and a NAT Gateway (one-way).
- **File Security Errors:** Encountered SSH connection refusal error `WARNING: UNPROTECTED PRIVATE KEY FILE!` when copying the `.pem` key pair file to the transit Bastion Host but forgetting to reconfigure file permissions.
- **Internal Service Configuration (VPC Endpoints):** The SSM Agent system on the Private EC2 failed to successfully register to the Systems Manager service because the user forgot to tick the "Enable DNS name" option when creating Interface Endpoints.
- **Financial Risks (FinOps):** High risk of incurring large silent Billing invoices from hourly-charged resources like NAT Gateway (~$32/month) and Interface Endpoints if one carelessly forgets to turn off/delete them after completing the lab.

---

### Solutions and Remediation:

- **Visual Thinking:** Systematized knowledge by drawing a mind map of traffic flow from the internet environment through each gateway and subnet to deeply grasp the infrastructure structure.
- **OS Security Compliance:** Complied with Linux system security standards, immediately running the command `chmod 400 aws-keypair-v2.pem` right after uploading the key pair file to the server.
- **Double-check:** Carefully read lab instructions, checked VPC DNS resolution attributes in detail, and accurately configured inbound port 443 for endpoint Security Groups.
- **Cleanup Discipline:** Established a systematic resource cleanup checklist after every study session, thoroughly checking the Billing Dashboard periodically to detect and proactively prevent non-terminated resources.