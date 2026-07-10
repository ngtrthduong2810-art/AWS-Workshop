---
title: "Event 1"
date: 2026-05-09
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# "FCAJ Community Day" Reflection Report

### Event Objectives

- Introduce neuroscience mechanisms (especially how Dopamine works) to help learners build motivation and maintain discipline on their self-study journey.
- Equip attendees with advanced Prompt Engineering techniques (Ultimate Prompt Engineering) to maximize efficiency when working with Large Language Models.
- Provide practical insights into career paths and the actual criteria businesses use to evaluate candidates, specifically tailored for 3rd and 4th-year IT students.
- Present the BMX software development method (BMM method)—how to systematically organize AI Agents to minimize hallucination.

### Speaker Lineup

- **Mr. Long** - Expert sharing on Brain-hacking techniques.
- **Mr. Thinh** - Ultimate Prompt Engineering.
- **Mr. Khang** - Solutions Architect at Cloud Kinetics (Over 3 years of experience in tech recruitment and engineering orientation).
- **Ms. Thao** - Software Developer at Vietnam International Bank (VIB).

### Key Highlights

#### "Brain-Hacking" Method to Make Learning as Addictive as Gaming/Social Media

- **The Dopamine Mechanism**: Interestingly, dopamine does not peak when we receive a reward—it spikes highest when the brain is *anticipating an upcoming reward*. This is the "secret formula" exploited by platforms like TikTok: users are hooked by the curiosity of not knowing what the next piece of content will be.
- **Applying it to learning through 4 stages**: Curiosity → Experimentation → Discovery → Satisfaction.
- **Core techniques**:
  - *Loss Aversion*: Use a wall calendar or a streak-counting app to record consecutive study days (similar to Duolingo or TikTok streaks). The regret of potentially losing a long streak becomes the motivation to sit at the desk, even for just 5–10 minutes.
  - *Tricking the Amygdala*: Faced with a mountain of knowledge, the brain's natural reflex is fear and avoidance. The solution is to break down the goal—instead of forcing yourself to study AWS for 5 continuous hours, just focus on a single service for 10-20 minutes.
  - *The 2-Minute Rule*: Anything that can be completed within 2 minutes (opening an exercise file, reading one page of a document) should be done immediately—this is the most effective way to break the procrastination loop.
  - *Feedback Systems & Gamification*: "Gamify" your own learning: design an experience point (XP) scale, a ranking system (Bronze, Silver, Gold, Orange based on the FCJ rank model), and prepare random lucky draw reward boxes after each study session to consistently nourish dopamine.

#### Ultimate Prompt Engineering Techniques

- **7 components of a standard Prompt**: Role, Instruction, Context, Input Data, Output Format, Examples, and Constraints.
- **Token Optimization**: LLMs do not read word by word but process them in subwords called tokens. A crucial point for Vietnamese businesses: for the same content, Vietnamese text passing through the Tokenizer usually consumes twice as many tokens as English—meaning API bills increase accordingly.
- **Advanced Reasoning Techniques**:
  - *Chain of Thought (CoT)*: Requesting the AI to present its reasoning step-by-step, thereby significantly improving the accuracy of the result.
  - *Tree of Thought (ToT)*: Organizing the reasoning process into a tree structure, combining DFS/BFS traversal algorithms so the model can self-compare multiple solution branches and choose the optimal path.
  - *Self-Consistency*: Making the model run multiple independent reasoning threads in parallel, then finalizing the answer based on the majority rule.
- **Case Study (Project Prompt Optimizer)**: An automated prompt optimization project running entirely on AWS Serverless architecture: CloudFront + S3 handling Frontend/CDN, Amazon Cognito managing users and JWTs, the API Gateway + AWS Lambda duo orchestrating traffic and business logic, DynamoDB storing prompt history with millisecond query latency, and Amazon Bedrock acting as a secure bridge to Foundation Models like Claude 3.5 Sonnet.

#### Career Orientation for Students ("Why haven't you started working yet?")

- **AI Amplification Effect**: AI acts like a megaphone—lazy, superficial people will get worse (copy-pasting machine-generated code without understanding it), while those with a solid foundation will double or tenfold their productivity. Recruitment reality: businesses would rather choose a 6-7 point candidate who thinks with their own mind, than a 9-10 point submission done by AI where the candidate stumbles and cannot explain it when asked.
- **Thinking "Why" instead of "What"**: Don't stop at "how to finish the assignment" (What)—ask yourself "Why choose this architecture/service?", "What are the trade-offs here?". Repeating the "Why" question at least 5 times is the way to dig down to the root of any problem.
- **Integrity & Long-term Vision**: A worker with integrity, when given 10 requirements, will independently dissect 20-30 additional edge cases to handle them thoroughly—doing the right thing even when no one is watching. For fresh graduates, prioritize accumulating long-term experience rather than getting caught up in the starting salary figure.
- **The 3-Circle Work Model & 5 Benefits**: The ideal job lies at the intersection of three circles: what you love, what the business requires you to do right, and the benefits you receive. A job brings 5 values: Salary, Experience, Network, Knowledge, and Promotion.
- **The 5 Candidate Evaluation Criteria of Businesses**: Attitude (the #1 factor for Freshers), Education, Experience, Exposure, and Talents.

#### BMX Software Development Method with AI Agents

- **Concept**: BMX (Through Method for Agile Development) is an open-source method that brings AI workflows into the traditional Agile framework: the system is operated by AI Agents taking on independent roles—PM, Architect, PO, Scrum Master, Developer, Reviewer/QA.
- **Minimizing Hallucination**: When cramming all requirements into a single chat window, the Context Window bloats excessively, causing the AI to get confused and generate incorrect code. BMX resolves this by breaking down the PRD (Product Requirement Document) and System Architecture into neat, independent Epics and Stories.
- **Operational Mechanism**: Each Story goes through a strictly human-controlled state chain (Draft → Approved → Review → Done). The Developer Agent is only allowed to receive and implement Approved Stories; next, the Reviewer Agent and QA Agent run continuous testing loops until the error rate reaches 0. The core philosophy of the method: don't manage source code—write excellent Documents, and leave the optimal automated code generation to the AI.

### Key Takeaways

#### Design Thinking

- **Foundation-first approach**: There's no need to conquer all 200–300 services in the AWS ecosystem—deeply and firmly mastering the 5 core foundational services is enough of a springboard to design architectures for almost any problem.
- **Architectural critical thinking**: Maintain a thought process of continuous questioning with "Why" when working with AI—do not easily accept the first answer, to avoid falling into the hallucination trap of large language models.

#### Technical Architecture

- Mastered the **7 components of an advanced Prompt structure** and know how to apply them to daily work to improve the quality of AI responses.
- Understood the cost nature of operating LLM systems through the **Token calculation mechanism**—especially the double cost gap when processing Vietnamese compared to English.
- Clearly visualized how to **orchestrate multiple AI Agents** according to the BMX model: dividing modules, packaging separate Context Windows for each specialized Agent, ensuring each task is executed independently without cross-impacting other features.

#### Modernization Strategy

- **Document-driven development strategy**: Shifting the focus from "writing code" to "writing standard technical documents"—so the automated code generation capability of AI Agents can be maximized.
- **Long-term experience accumulation strategy**: Learning to embrace mistakes as an inevitable part and viewing one's career through a long-term vision, rather than just focusing on immediate financial goals.

### Application to Work

- **Restructuring daily Prompt workflows**: Incorporating the full set of 7 structural components (Role, Instruction, Context, Constraints...) into the workflow with Gemini/ChatGPT to significantly improve output quality.
- **Applying "Why" thinking to current projects**: Proactively raising and resolving additional edge cases for features under development—a way to forge integrity through practical work.
- **Building a self-study discipline chain**: Combining the calendar-marking/streak (Loss Aversion) method with the 2-minute rule to maintain the habit of learning new technologies (services like AWS Lambda, Bedrock) regularly for at least 15-30 minutes every day.
- **Researching the BMX method**: Downloading and testing BMX from GitHub in personal or group projects, evaluating the effectiveness of task separation and source code management using AI Agents.
- **Promoting team collaboration skills**: Boldly participating and sharing at community Tech Meetups—both honing presentation and critical thinking skills, and expanding my professional network.

### Event Experience

Attending the **"FCAJ Community Day"** workshop was a truly valuable experience for me: the event both expanded my technical vision (Advanced Prompts, AI Agents, Serverless) and delivered very "real" career orientation lessons from industry seniors. A few memorable highlights:

#### Learning from Highly Specialized Speakers

- The frank, unembellished sharing from Mr. Khang (Cloud Kinetics) and Ms. Thao (VIB) about the actual corporate environment helped me clear up many misconceptions—about the true value of grades, and the consequences of relying on AI when taking recruitment tests.

#### Practical Technical Experience

- Witnessed firsthand a demo of the Serverless architecture for the Prompt Optimizer project featuring Amazon Bedrock, DynamoDB, and Lambda.
- First time being exposed to advanced prompt engineering concepts like Tree of Thought (ToT) and Chain of Thought (CoT) through highly visual, step-by-step mind maps.
- Grasped how an AI Agent ecosystem operates systematically through the lens of the BMX method—from Planning to Review/QA, each role is separated scientifically.

#### Applying Modern Tools

- Learned how to stand in the position of mastering AI tools to multiply productivity, instead of becoming a victim of AI Amplification. Knowing how to utilize AI at full capacity for brainstorming and idea development, while the core thinking always remains in my hands.

#### Networking and Exchange

- The event atmosphere was open and highly connective, encouraging students to actively ask questions and debate without hesitation. The workshop gave me great motivation to confidently share knowledge with the community without fear of being wrong—because "mistakes are a part of the experience accumulation journey."

#### Lessons Learned

- The one who reaches the finish line on the self-development journey is not the smartest person, but the most persistent one who knows how to create a good learning environment for themselves.
- AI will not replace programmers—but programmers who understand the core issues and master AI tools (advanced prompts, AI Agent models) will replace those who do not.
- Maintain integrity in everything you do, ask the "Why" question for every technical decision, and always view your career path with a long-term vision.

#### Some Event Photos

- ![Evidence photo: participating in event](</images/4-EventParticipated/Event1/event1(0).jpg>)
- ![Evidence photo: participating in event](</images/4-EventParticipated/Event1/evt1(1).jpg>)