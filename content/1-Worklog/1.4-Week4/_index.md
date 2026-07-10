---
title: "Worklog Week 4"
date: 2026-05-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives: Building Data Architecture and Application Tier Separation

After mastering compute capacity (EC2), week 4 marks a significant milestone in designing a Tiered Architecture. The focus this week is separating the Data Tier from the Application Tier using a fully managed database service. Deep-dive objectives include:

* **Explore Database as a Service (DBaaS):** Discover the broad picture of Amazon RDS and its importance in cloud database architecture compared to self-hosted solutions.
* **Grasp Automated Management Mechanisms:** Clearly understand RDS core features including: managed service, automated backups, scalability, Multi-AZ architecture, and Read Replicas.
* **Provision Core Network for Data:** Proceed to set up the VPC network, Subnets, and configure Security Groups for both EC2 and RDS, ensuring the database is completely invisible to the Internet.
* **Secure Data Partitioning:** Build a DB Subnet Group to create a standard network space for deploying High Availability databases.
* **Architect the Application Environment:** Install and launch an EC2 virtual machine acting as the Application Server directly connecting to RDS.
* **Practical Data Deployment:** Establish the RDS Database Instance, concurrently collecting vital information like Endpoint, Port, and Username for system integration.
* **Continuous Integration:** Deploy the AWS FCJ Management application to the environment and configure environment variables to successfully communicate with the RDS database.
* **Ensure Business Continuity:** Familiarize with database backup, snapshot creation, and restore operations.
* **Financial Discipline:** Thoroughly delete initialized resources after completing the practical lab to optimize costs (FinOps).

---

### Tasks to be Implemented this Week:

| Day | Deep-Dive Tasks | Start Date | End Date | Reference Sources |
| --- | --- | --- | --- | --- |
| Mon | - **Foundational Research:** Read Amazon RDS introduction documents. <br> - Clarify the nature of OLTP systems, DB Instances, Endpoints. <br> - Categorize Database Engines (MySQL, PostgreSQL, Aurora, etc.). | 11/05/2026 | 11/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| Tue | - **Tiered Network Design:** Module 2.1: Create a VPC. <br> - Set up a VPC network including Public (for App) and Private Subnets (for DB). <br> - Span the architecture across multiple Availability Zones for redundancy. | 12/05/2026 | 12/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| Wed | - **Firewall Setup:** Module 2.2: Create EC2 Security Group & Module 2.3: Create RDS Security Group. <br> - Route Security Group chaining: RDS only accepts traffic from EC2. | 13/05/2026 | 13/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| Thu | - **Infrastructure Preparation:** Module 2.4: Create DB Subnet Group. <br> - Module 3: Create EC2 Instance (App Server). <br> - SSH connection into the server via MobaXterm. | 14/05/2026 | 14/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| Fri | - **Database Initialization:** Module 4: Create RDS Database Instance. <br> - Select engine, identify, allocate resources, and attach VPC/Security Group. <br> - Extract Endpoint and Port when in Available status. | 15/05/2026 | 15/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| Sat | - **Application Deployment:** Module 5: Application Deployment. <br> - Clone source code, install Node.js, configure `.env` environment variables. <br> - Initialize data tables and run the web app on port 5000. | 16/05/2026 | 16/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| Sun | - **Operations & Cleanup:** Module 6: Backup and Restore. <br> - Module 7: Thorough Clean up resources (EC2, RDS, Snapshot, SG, VPC). | 17/05/2026 | 17/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |

---

### Week 4 Results: Deep-Dive Theoretical Summary

#### 1. Managed Services Philosophy
Instead of installing MySQL on an EC2 instance myself (Self-managed), I thoroughly understand the power of Amazon RDS. It is a fully managed relational database service. RDS frees engineers from "undifferentiated heavy lifting" such as OS installation, security patching, or setting up backups. Consequently, the technical team can focus entirely on schema design and query optimization.

#### 2. Database Networking Architecture
A secure system is one that does not expose itself to the Internet. I mastered the concept of separating the application tier (Public Subnet - containing EC2) and the data tier (Private Subnet - containing RDS).
Specifically, the **DB Subnet Group** concept is crucial: it is a collection of subnets spanning at least 2 Availability Zones. This forces AWS to have space to allocate redundancy resources (Standby Replica) in a Multi-AZ architecture, ensuring high availability even if one physical data center fails.

#### 3. Security Group Chaining
This is the most valuable network security (NetSec) knowledge of the week. Instead of opening port `3306` of RDS to a specific IP range, I utilized the **Security Group Chaining** mechanism. I configured the RDS Security Group so that its Source is the ID of the EC2 Security Group. This principle creates a circle of trust: The database rejects all connections except those originating from my own application servers, establishing a solid Zero Trust architecture.

#### 4. Application Integration and Configuration Management
I understand that an application should never hardcode database connection information into the source code. Using an `.env` file to load environment variables (DB_HOST, DB_USER, DB_PASS) at runtime makes the application flexible. When the RDS Endpoint changes (e.g., after restoring a snapshot), I only need to modify the `.env` file without having to recompile the source code.

#### 5. Disaster Recovery
I am highly aware of the difference between Automated Backups (cyclical automated backups supporting Point-in-time recovery) and Manual Snapshots (permanent manual backups created by users). An important operational lesson: when recovering (Restore) from a Snapshot, AWS does not overwrite the old database but creates an entirely new DB Instance with a new Endpoint.

---

### Hands-on Experience: Module Analysis

**Module 1 & 2 — Initializing Network Foundation and Firewalls**
- Started with setting up the virtual network space (VPC), declaring the IPv4 CIDR range, creating a Public Subnet for EC2, and a Private Subnet for RDS across 2 distinct Availability Zones.
- Built a Security Group for EC2 (App Tier) allowing Inbound ports `22`, `80`, `443`, and `5000`. Tightened security by only allowing SSH from my personal IP.
- Created a Security Group for RDS (Data Tier) opening port `3306`, specifying the Source as the ID of the EC2 Security Group.
- Created a DB Subnet Group, gathering Private Subnets to act as a secure launching pad for database initialization.

**Module 3 & 4 — Launching Application Server and Database**
- **App Server:** Launched an Amazon Linux 2023 virtual machine (`t2.micro` or `t3.micro`), attached the EC2 Security Group, and used a Key Pair to SSH via MobaXterm.
- **Database:** Launched the RDS Database Instance using the Standard Create option. Identified the DB, declared the Master user/password, and attached it to the newly created VPC, DB Subnet Group, and RDS Security Group. Monitored the state transition from `Creating` to `Available` and extracted the Endpoint connection string.

**Module 5 — Practical Application Deployment (Deployment)**
- SSHed into EC2, installed Git, Cloned the AWS FCJ Management project.
- Set up the Node.js runtime environment, installed npm dependencies and the MySQL client.
- Created an `.env` file to declare `DB_HOST` (the RDS Endpoint), `DB_NAME`, `DB_USER`, `DB_PASS`.
- Used the MySQL client to test direct connection to RDS, created the `first_cloud_users` database and `user` table, inserted sample data.
- Ran the `npm start` command and successfully tested web app access in the browser via port `5000`.

**Module 6 & 7 — Backup and Cleanup Discipline (FinOps)**
- Tested the Manual Snapshot creation feature and surveyed the Restore process into a new database cluster.
- Terminated the EC2 virtual machine.
- Deleted the RDS Database Instance (paying attention to unchecking the final snapshot creation to avoid hidden storage fees).
- Sequentially removed the DB Subnet Group, Security Group, Route Table, IGW, and finally the VPC to return a clean environment.

---

### Difficulties and Technical Barriers:

- **Database Connection Timeout:** Initially, the application couldn't connect to RDS. The most common cause is forgetting to configure the correct Source in the RDS Security Group (mistakenly choosing an IP instead of the EC2 Security Group) or mistakenly placing RDS in a Public Subnet.
- **Environment Variable Management:** Sometimes mistyping the Endpoint or missing the port in the `.env` file leads to the Node.js application throwing "Access Denied" or "Host not found" errors.
- **Initialization Latency:** The RDS creation process takes quite a bit of time (5-10 minutes). This can cause impatience, leading to rushed operations when the database is not truly in the `Available` state yet.
- **Resource Orphan Risks:** RDS is a fairly expensive service if left running in the background. Besides deleting the Instance, automated Snapshots retained after deleting the database will also incur EBS storage costs.

---

### Solutions and Best Practices:

- **Apply the "Security Group Chaining" Principle:** Always Double-check the RDS Inbound rules. Ensure absolutely no rule contains `0.0.0.0/0` on port 3306.
- **Log Debugging:** When the Node.js application errors out, build the habit of reading logs on the terminal (stdout/stderr) or using the `mysql -h <endpoint> -u admin -p` command from EC2 to ping-test the network connection before hunting for bugs in the code.
- **Waiting State Discipline:** Only perform Endpoint extraction and connection operations when the RDS Status turns green (`Available`).
- **Strict Cleanup Checklist:** When deleting RDS, the system usually asks "Create final snapshot?". For lab environments, this option must always be Unchecked. Check the "Snapshots" tab to ensure no residual backups are left behind.

---

### Optimal Directions for Next Week:

The architecture has taken clear shape. However, operating everything currently relies on manual "clicks" and lacks a holistic expenditure management mechanism.
- Moving into the next week, the focus will shift to **FinOps** with the AWS Budgets service to learn how to set up automated financial barriers.
- Understand the difference between cash flow control (Cost) and resource control (Usage).
- Prepare the foundation to eventually automate infrastructure instead of manually creating each Subnet, RDS, or EC2.