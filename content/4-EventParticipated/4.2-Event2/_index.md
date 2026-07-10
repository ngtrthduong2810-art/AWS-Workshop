---
title: "Event 2"
date: 2026-05-23
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# "FCAJ Community Day - May 2026 Edition" Reflection Report

### Event Objectives

- Provide the latest macroeconomic picture of the Vietnamese IT market amidst the rapidly developing AI landscape.
- Deep dive into Prompt structuring methods for Context Optimization and mastering the inherent Randomness of LLMs.
- Demonstrate an enterprise data analysis assistant solution based on Amazon Q Business (QuickSight/Q Desktop) integrated with an MCP server.
- Recount the hands-on journey at the Hackathon and how to build an Enterprise-standard Multi-Agent system for the banking and finance sector.

### Speaker Lineup

- **Mr. Nguyen Gia Hung** - Solutions Architect at AWS Vietnam & Founder of FCAJ (Sharing on macroeconomic market orientation).
- **Mr. Tinh Truong** - Platform Engineer at Gothamic X (Sharing on LLM Context Optimization and Randomness techniques).
- **Mr. Hai Anh** - Solutions Architect at Pacific Vietnam (Sharing on Amazon Q Business & MCP).
- **Mr. Nguyen Han Thinh** - DevOps Engineer (Sharing on the Flat-rate Pricing mechanism and advanced security of Amazon CloudFront).
- **Ms. Uyen, Mr. Mach & Ms. Thao** - Hackathon Winner Team (Sharing on the 36-hour journey of developing the UTMorpho project).
- **Final Speaker (FinTech Engineer)** - FinTech Solutions Consultant at VPBank (Sharing on Multi-Agent architecture applied in banking).

### Key Highlights

#### 1. IT Market Positioning and New Career Opportunities in the AI Era

- **The "LED Bulb" Paradox and the Software Boom**: The history of the LED bulb offers a surprising lesson—when lighting costs dropped to 1/10, people didn't light less; they lit significantly more. The same applies to software: AI makes writing code cheaper than ever, and as a result, the global demand for software development will not shrink but explode fiercely. Vivid proof: even non-IT professionals (lawyers, doctors) can now win prizes at major Anthropic Hackathons.
- **A New Wave of Jobs - Fixing Junk Code & Platform Engineering**: When anyone can generate code using AI, the market will be flooded with MVP products or projects full of bugs or running unsteadily, unable to operate reliably. This opens up two rapidly growing long-term recruitment demands: engineers specializing in "cleaning up junk code" and system improvement, along with Platform Engineering teams building infrastructure automation platforms (IDP - Internal Developer Platform) for large-scale organizations.
- **Recruitment Reality in Vietnam**: Global tech corporations are still steadily opening Technical Hubs in Vietnam to hunt for local talent. The challenge for Vietnamese engineers: invest in confidence, English proficiency, practical business understanding (Domain knowledge), and the ability to create truly Production-ready products—instead of staying stuck on isolated demo projects.

#### 2. Context Optimization Techniques and Controlling LLM Randomness

- **The Error of Constant Context Switching**: A disastrous habit many people have: cramming all sorts of topics into a single chat session—from asking for travel itineraries and fixing CVs to writing code. Consequently, the Context Window is constantly shuffled, and the AI slips into a "hallucination" state much faster.
- **Temperature Mechanism and Logit Scores**: Fundamentally, an LLM is a "probabilistic engine"—it scores (logits) each candidate word that might appear next and selects based on probability. When dragging `Temperature = 0`, the word selection mechanism switches from Softmax to Argmax—always taking the highest-scoring word—making the answer deterministic and consistent across runs.
- **The Difference Between Cloud APIs and Local Hosts**: A little-known fact: even when setting `Temperature = 0`, calling the OpenAI or Amazon Bedrock API multiple times can still yield different results. Two culprits are behind this: parallel floating-point operations on GPUs causing decimal drifts during rounding, and vendors' commercial optimization techniques (Inference Optimization)—batching many short prompts from multiple users into a single processing run to save costs. If you want to control 100% absolute consistency, the only way is to self-host the model on Local infrastructure.

#### 3. Amazon Q Business Ecosystem & Next-Generation Data Analysis Assistant

- **Building Extensions with MCP (Model Context Protocol)**: Modern AI Agents cannot just stop at generating text responses—they must be able to take Action. Through MCP ports, Agents can directly schedule meetings, automatically send emails, or connect straight into enterprise systems like Jira, Confluence, Microsoft Cloud, and Google Suite.
- **Automated Data Analysis Assistant**: With Amazon Q Business (or QuickSight Desktop), an enterprise employee with zero BI (Business Intelligence) knowledge just needs to drop a raw Excel data file in—the system instantly self-analyzes and builds a completely visual Dashboard in an incredibly short time.

#### 4. Case Study: UTMorpho Project Wins Hackathon in 36 Continuous Hours

- **An Idea Solving a Real Pain Point**: The team did not chase after flashy macro ideas but targeted a very specific pain point for developers: whenever they want to fix a tiny detail on an AI-generated interface, they are forced to ask the AI to regenerate everything from scratch—wasting both time and Tokens.
- **UTMorpho's Multi-Agent Architecture**: The project runs on AWS Serverless architecture with 3 specialized Agents coordinating smoothly:
  - *Agent 1 (Vision Agent)*: Receives images/sketches from the user's camera, extracting the content into a structured JSON file.
  - *Agent 2 (Layout Agent)*: Reads the JSON file and calculates the CSS structure, layout arrangement, and component dimensions.
  - *Agent 3 (Design Agent)*: Receives the output of Agent 2, compiles it into complete HTML/CSS code, and displays it in real-time (Streaming UI).
- **Highlight Features**: Equipped with a visual Editor allowing developers to drag, drop, and move component positions right on the displaying interface, while simultaneously exporting a public HTML link to share with colleagues for review.

#### 5. Enterprise-Standard Multi-Agent Architecture for Banking Operations (VPBank Practice)

- **Business Problem - Credit Evaluation for Startups**: The traditional loan approval process requires financial reports for 3 consecutive years and physical collateral—a door almost completely shut for Startups that only own intellectual property and have been operating for just 3-6 months. Proposed solution: a multidimensional analysis Multi-Agent system based on non-traditional data sources.
- **Specialized Multi-Agent System Design**:
  - *Credit Committee Agent (Manager/Orchestrator)*: Holds the council chair—distributing tasks to member Agents and synthesizing the final report.
  - *Financial Analyst Agent*: Specializes in deep analysis of the enterprise's short-term financial reports and cash flows.
  - *Market Research Agent*: Evaluates market share (TAM, SAM, SOM), competitors, and related market trends.
  - *Team Evaluator Agent*: Collects data and appraises the capability of the Founders team via technology profiles and their footprints on Twitter(X), LinkedIn, Facebook.
  - *Risk Assessor Agent*: Bears the most crucial role—monitoring the operational boundaries of all other Agents, applying two-way data filtering (Input/Output filtering) to prevent confidential information leaks and block Prompt Injection attacks, complying with the strict standards of the State Bank.

### Key Takeaways

#### Design Thinking

- **Business-Driven Mindset**: Every technology solution in large enterprises must pass a 4-question test before design begins: Who uses it? What are they using? Why do they have to use it? When is the right time to deploy?
- **Separation of Concerns Mindset**: Each AI Agent should carry out exactly one specialized role, clearly defined through its own Backstory and System Prompt—this both prevents Context Window overload and helps the model distribute its Attention most efficiently.

#### Technical Architecture

- Mastering the **Determinism control mechanism** of LLMs through the `Temperature`, `Top P`, and `Repeat Penalty` parameters—adjusting flexibly depending on whether the output needs to be creative (text) or absolutely precise (JSON/Code).
- Deeply understanding the **AWS Backbone & PoP (Points of Presence)** internal network infrastructure behind CloudFront: how the CDN consolidates requests across multiple tiers to shield the Origin Server from volumetric DDoS or Syn Flood attacks using the Syn Proxy feature.
- Clearly recognizing the value of Infrastructure as Code management with **Terraform**: controlling resource versions and reproducing the entire system across multiple AWS Regions.

#### Modernization Strategy

- **ROI (Return on Investment) Measurement Strategy**: To get Enterprise leadership to nod yes to an AI project, you must speak with specific numbers (Numbers speak louder than words)—what the payback period is, how much money it saves the business annually—not just present a fancy tech demo.
- **Continuous Testing Strategy**: The path to bringing an AI system to Production standard in a rigorous environment is dynamic testing, testing deep down to downstream services—ensuring the system stands firm in any scenario where AI generates incorrect formats.

### Application to Work

- **More mindful Temperature parameter configuration**: Proactively setting `Temperature = 0` or `0.1` whenever the AI needs to generate highly structured formats like JSON/HTML in current projects—drastically reducing bracket and comma deviation errors.
- **Applying preventative Multi-Agent architecture**: No longer cramming the whole process into a single chat window—problems will be broken down into independently operating sub-agents (mimicking the UTMorpho model), accompanied by a management Agent positioned above to cross-check results.
- **Enhancing application security**: Building sensitive data filtering layers (Input/Output filtering) using AWS Lambda right at the data transmission gateway into large language models, meeting the organization's internal security regulations.
- **Transitioning to Terraform infrastructure management**: Initiating Terraform scripting for the system's CloudFront and S3 services, gradually replacing manual configurations (Click engineering) on the Console—making version management easier and API Keys/Access Keys periodic rotation more convenient.
- **Focusing on foundational Backend knowledge**: Persistently honing core Software Engineering mindsets, firmly grasping data structures and API contracts—because AI is just a tool to help build products faster, while the engineer's systems thinking is the ultimate deciding factor.

### Event Experience

Attending the **"FCAJ Community Day"** workshop this time was a massive cognitive boost for me. The event stepped completely outside the framework of textbook knowledge to bring "flesh and blood" stories distilled from the real corporate environment. A few unforgettable highlights:

#### Learning from Highly Specialized Speakers

- The speakers from AWS Vietnam, VPBank, VIB, and Gothamic X showed me the real gap between doing personal projects at home and operating products serving millions of customers in the Banking industry—where information security and compliance are always the top priority.

#### Practical Technical Experience

- Truly "mind-opening" observing AI Agents coordinating under a Multi-Agent model: automatically and comprehensively analyzing the market, from financial metrics and social media data to the profiles of individual business founders.
- Uncovered the harsh truth behind the cost-optimization algorithms of major Cloud providers—and understood why AI still yields random results even when the temperature is set to zero.

#### Applying Modern Tools

- Witnessed data being visualized using just a few simple Vietnamese commands through the Amazon Q Business and QuickSight demo. The MCP (Model Context Protocol) truly opens up a new era—where engineers can craft genuine "extended arms" for artificial intelligence.

#### Networking and Exchange

- The organizers very skillfully connected attendees across different floors (even those on the 36th floor via the Lucky Draw system). The event ignited a spirit of proactively initiating conversations, seeking collaborators, and infused young students with a powerful motivation for teamwork.

#### Lessons Learned

- AI is dragging software development costs to unprecedented lows—market demand will therefore explode, and massive opportunities will belong to those possessing good enough systems thinking to solve big problems.
- Absolutely do not abuse AI by copy-pasting verbatim (Ctrl+C & Ctrl+V) without understanding the source code's nature—the price to pay in a corporate Production environment is exceptionally high.
- For a technology system, "running" has never been the finish line—it must run **safely**, **reliably**, and truly **bring value to users**.

#### Some Event Photos

![Evidence photo: participating in event](</images/4-EventParticipated/Event2/event2(0).jpg>)
![Evidence photo: participating in event](</images/4-EventParticipated/Event2/evt2(1).jpg>)

> Looking back at the entire event, the value received did not just stop at the deep technical knowledge of Prompt Engineering or software development models in the AI era—what resonated most was the fire of passion, the spirit of self-study discipline, and a proper professional mindset passed down to the next generation of tech engineers.