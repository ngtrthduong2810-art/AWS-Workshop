---
title: "Event 3"
date: 2026-06-13
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# "FCAJ Community Day - June 2026 Edition" Reflection Report

### Event Objectives
- **High-scale Architecture**: Introduce a scalable URL Shortener service architecture on the AWS ecosystem.
* **Data capability development orientation**: Analyze the practical work, core skill set, and mindset roadmap for a Data Analytics Engineer in multinational corporations (MNCs).
- **Decoding the practical DevOps role**: Assess the market landscape, income levels, recruitment demand, and immutable foundational skill sets of a professional DevOps engineer.
- **Connecting the value chain and citizenship mindset**: Share the journey from a curious student to an AWS technology partner, combining the "Do the right thing" philosophy to contribute to the national digital lifeblood.

### Speaker Lineup

- **Mr. Dinh Trung Kien** - Lead Developer at Startup.
- **Mr. Nguyen Minh Tho** - Student & Cloud Contributor.
- **Mr. Dat Pham** - Data Analytics Engineer at a Multinational Corporation.
- **Mr. Cuong Nguyen** - Process Engineer.
- **Mr. Trong H.Truong** - DevOps Engineer at Endava Vietnam.
- **Mr. Danh Hoang Hieu Nghi** - AI Engineer, AWS Community Builder & SBG Leader.

---

### Key Highlights

#### 1. Scalable URL Shortener architecture on AWS
- **The pain of traditional systems (Naive Flow)**: The traditional on-demand short code generation process often faces major issues with Read Latency, security vulnerabilities, Single Point of Failure, and difficulty scaling during traffic spikes.
- **Advanced Key Generation Service (KGS) architecture**:
  - *Separation of Concerns*: The Read path and Write path operate completely independently, optimized separately according to traffic characteristics.
  - *Pre-computation over On-demand*: Use Containers on **Amazon ECS** to pre-compute and generate short codes before receiving user requests. These codes are then continuously pushed into the **Amazon ElastiCache for Redis** queue via the `LPUSH key_queue` command.
  - *Lightning-fast initialization process*: When a user requests to shorten a link, the Backend service (SpringBoot running on ECS) simply executes the `RPOP` command to immediately fetch a pre-generated code from Redis and write the information to **Amazon DynamoDB** as the Primary Key (PK). This process happens instantly and completely eliminates the risk of code collisions (Collision-free).
  - *Cache-aside Pattern*: The Forward flow prioritizes looking up in the Redis Server cache first (Cache hit). The system only queries the DynamoDB database when a Cache miss occurs, minimizing load pressure and keeping latency to an absolute minimum.
  - *Defense at the Edge*: Push the entire **AWS WAF** security layer and **Amazon CloudFront** static distribution caching layer as close to the user as possible, stopping threats before they touch the system's core.

#### 2. Practical work and growth mindset of a Data Analytics Engineer at MNCs

- **Differences in work domains**:
  - At Tech/E-commerce companies (like Kamereo): Focus on building periodic reports to monitor operational performance, designing data trend Dashboards to detect anomalies, and coordinating across departments to find Root Causes to optimize GMV.
  - At manufacturing corporations (like Colgate-Palmolive): Participate in factory machinery and IoT equipment data projects to find opportunities for production cost optimization and equipment efficiency enhancement.
- **4 mandatory skills**: Critical thinking, coordinating communication skills, Data storytelling, and practical problem-solving capability.
- **5-step career path roadmap**: A mindset that doesn't overemphasize Titles but focuses on upgrading capabilities through each step: `Follower` (Checklist executor) $\rightarrow$ `Learner` (Proactive learner) $\rightarrow$ `Problem Solver` (Committed problem solver) $\rightarrow$ `System Thinker` (Panoramic systems thinker) $\rightarrow$ `Super Star` (Vision builder and leader).
- **No-Blame Post-Mortem culture**: Deeply portrays the tech culture at multinational corporations. When a severe system crash occurs, engineers sit together to review the source code, find infrastructure architecture loopholes to fix them at the root instead of criticizing or assigning blame to individuals.

#### 3. The comprehensive picture of a DevOps Engineer in reality
- **Market and income in Vietnam (2025 - 2026)**: According to survey reports from ITviec and JT1 Salary Guide, DevOps Engineer and Cloud Engineer roles always remain in the group with the highest recruitment demand and salaries in the market. Income ranges from **16 - 28 million VND/month** for Juniors and can reach **65 - 100 million VND/month** for Lead/Expert levels.
- **Prejudice vs. Reality**: DevOps is not just someone who writes a few CI/CD pipelines, configures Docker/Kubernetes, or sits on call at midnight. The Scope of work heavily depends on the company's size, departmental structure, and the maturity of the enterprise's infrastructure.
- **"Fundamentals Stay"**: Technological tools can change constantly over time, but foundational knowledge will always remain. A good DevOps engineer must master root skills: Linux Operating System, Networking basics, Programming languages (Python/Golang), System Thinking, and the ability to ask *"Why"* before learning *"How"*.

### Key Takeaways

#### Design Thinking

- **Pre-computation mindset**: Learned how to shift heavy, real-time bottleneck-prone tasks into asynchronous background tasks, preparing resources in advance to serve end-users with the lowest latency.
- **No-Blame mindset**: Understood that system failures are due to flaws in processes or architecture; building an open post-incident discussion culture is key to upgrading the stability of the entire organization.

#### Technical Architecture

- Mastered the **KGS (Key Generation Service)** deployment model combining Redis (in-memory) and DynamoDB to handle high-load problems and prevent data duplication.
- Understood how to distribute operational performance metrics (Fulfillment, Last Mile Cost, Fill Rate) through visual data analysis Dashboards.
- Clearly distinguished security defense layers at the cloud edge through the combination of AWS WAF, CloudFront, and AWS KMS.

#### Modernization Strategy

- Comprehended the shift chain from "Getting it done" to "Doing it to global standards". For the physical supply chain, it's complying with GMP, GSP, GDP; for the digital supply chain and cloud infrastructure, it's mandatory to achieve rigorous certifications like ISO 27001, SOC 2, and GDPR.

### Application to Work

- **Apply Cache-aside in projects**: Set up an additional Redis Cache layer in front of the main Database of personal Backend applications to optimize API response speeds.
- **Build a System Thinker mindset**: When writing code or configuring systems, form the habit of evaluating whether this change cross-impacts other modules or cloud resource costs (FinOps).
- **Focus on Fundamentals**: Dedicate more time to deeply learn the Linux kernel, advanced network administration commands, and Git branching strategies instead of just rote-learning automation tool syntaxes.
- **Practice the "Do the right thing" philosophy**: Forge strong internal self-governance, work with a spirit of service to solve real-world social problems, and aim to shoulder large digital systems after graduation.

### Event Experience

- Attending the **“FCAJ Community Day - June 2026 Edition”** event on June 13, 2026, brought an extremely explosive and practical series of technological experiences.

#### Learning from highly specialized speakers

- Extremely engaging sharings from highly experienced seniors. The advice of *"Using AI to elevate skills, not to turn off your brain"* from the DevOps speakers awakened me to the self-study methodology in the new technology era.

#### Practical technical experience

- Received detailed analysis of a large-scale, high-load AWS infrastructure architecture diagram. Dissecting each request flow from Route 53, passing through the ALB, and load balancing down to Fargate and Redis services helped me deeply understand what a High Availability system is.

#### Applying modern tools

- Gained access to actual operational Dashboard templates in enterprises, thereby understanding how to turn dry, raw data rows into meaningful stories that support the board of directors in making accurate business decisions.

#### Networking and exchange

- The event was incredibly cozy, featuring an in-person discussion space and online networking sessions via Google Meet with over 30 companion members. Discussing and listening to the concerns and developmental orientations from AWS Community Builders significantly expanded my professional network.

#### Lessons learned

- All trendy tools and technologies will become obsolete over the years; only foundational knowledge and strong systems thinking are the keys to helping an engineer adapt to any market fluctuations.
- Always proactively learn through practice (Hands-on Labs) and give back to the community (Share Back) to continuously elevate personal value on the technology map.

#### Some photos when participating in the event

![Evidence photo: participating in event](</images/4-EventParticipated/Event3/event3(0).jpg>)
![Evidence photo: participating in event](</images/4-EventParticipated/Event3/evt3(1).jpg>)

> In short, the event brought an extremely sharp and comprehensive technological lens. These are not just supplementary knowledge for the internship report, but also a compass helping me clearly define the path to becoming a proper and internationally standard cloud solutions engineer.