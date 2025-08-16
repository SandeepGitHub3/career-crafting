# Career Journey Raw Notes

## Current State
- Senior Software Engineer at Deliveroo.
- ~16–17 years of experience, primarily in backend technologies.
- Ideally should have been at Staff/Senior Staff Engineer level, but personal and professional reasons (discussed later) slowed progression.

---

## 1. Infosys (2008–2012)
- Joined as a campus recruit after graduation.
- Role: Beginner-level software engineer.
- Worked on **Finacle** (Infosys’s proprietary banking product).
- Tech stack: proprietary framework, not transferable to outside companies.
- Felt stuck — not learning market-relevant/open-source technologies.
- Tried learning Java to prepare for switching companies.
- Reflections:
  - Did job as told, not very passionate or hardworking.
  - Admitted lack of maturity, regrets not using time better.
  - Relationship issues with strict lead and manager — poor rapport.

---

## 2. Wipro (2012–2013/14) – Client: Morgan Stanley
- Worked onsite at **Morgan Stanley** (investment banking).
- High-pressure environment compared to Infosys.
- Learned:
  - Handling production issues.
  - Writing test evidence and detailed documentation.
  - Exposure to rigorous standards and accountability.
- Mentorship: supportive lead engineer and kind colleagues.
- Challenges:
  - Stressful workload.
  - Pay disparity (same workload as Morgan Stanley FTEs but paid much less as Wipro contractor).
- Duration: ~1.5 years.
- Left due to high stress, cracked interview at J.P. Morgan.

---

## 3. J.P. Morgan (≈2013/14 – 2018/19)
- Duration: ~5 years.
- Initial manager (US-based) was empathetic, supportive. Small team, low visibility.
- Asked to move to higher visibility team → transitioned but kept supporting old product.
  
### Repo Owner Conflict (Accruals Project)
- Faced delays from repo owner (slow reviews, last-minute changes).
- Initially frustrating, but responded by:
  - Improving PR quality.
  - Fixing flaky tests.
  - Addressing long-standing repo issues.
  - Adding improvements that even taught repo owner new techniques.
- Outcome: repo owner eventually **publicly praised work** in meeting.
- Lesson: conflict resolution through **competence, persistence, professionalism**.

### Feedback & Growth
- Growth stalled at one point.
- Manager’s feedback: **“Speak up more, make presence felt.”**
- Introverted by nature — usually silent in meetings, camera off.
- Response:
  - Started contributing actively in meetings.
  - Ran a knowledge session on **distributed tracing** in microservices.
- Built visibility, was on path to promotion but eventually moved on.

- Reason for Leaving: wanted to join a **product company**. Joined UpGrad.

---

## 4. UpGrad (≈2019 – 2022)
- First **product company** experience.
- Shift from being least experienced at JPM to most experienced → high expectations.
- Team expected faster delivery and possible move into engineering manager track.
- Chose to stay technical.

### Projects & Achievements
1. **Microservice Extraction**
   - Extracted service from monolith to its own DB.
   - Used feature flags despite leadership hesitation.
   - Delivered with minimal downtime.

2. **Learner Progress Service Proposal**
   - Proposed splitting monolith services (content vs learner progress).
   - Wanted dynamic progress tracking (accounting for page length, videos).
   - More realistic metrics than static completion tracking.
   - Initiative deprioritized, but showed vision/product awareness.

3. **Video View Tracking**
   - Needed view tracking for short videos.
   - Compared YouTube’s complex model but built simpler, faster version.
   - Prioritized **time-to-market** over “perfect” solution.

4. **Real-Time Leaderboard**
   - Rank learners by reading time across cohorts (80–250+ learners).
   - Challenges: scale + low latency.
   - Solution:
     - Publish reading times to Kafka.
     - Kafka Streams aggregate in windows.
     - Store results in Redis SortedSets for fast leaderboard queries.
   - Delivered successfully, created internal **learning exercise/game** for team.

5. **Mentorship**
   - Mentored junior engineer who grew significantly → promotion.
   - Another engineer had **attitude issues** (lateness, disengagement).  
     - Tried candid conversations, offered support.
     - Issues persisted → escalated to manager.
     - Learned: **skills can be trained, attitude issues are harder**.

- Recognition: became go-to technical expert for Director of Engineering.
- Got retention bonus + extra ESOPs.
- Career Aspiration: aimed for Principal/Architect, but felt technical growth needed.
- Left during strong post-COVID market. Got Deliveroo offer (London, later India).

---

## 5. Deliveroo (2022 – Present)

### Phase 1: Joining & Probation
- Applied for Staff Engineer, downleveled to Senior SE.
- Backend engineer in Salesforce-heavy team → skill mismatch.
- Probation: no major deliveries, stuck in discussions → placed on **PIP**.
- Recovered by:
  - Working with temporary team, delivering critical work.
  - Positive feedback helped clear probation.

### Conflict with Polish Colleague
- Teammate from sister backend team, technically strong, junior in title.
- Very critical in PR reviews, highly respected.
- Believed his feedback contributed to PIP.
- Built relationship by:
  - Adapting coding practices to his standards.
  - Accepting valid technical feedback.
  - Building rapport via casual conversations.
- Result: smoother collaboration, better delivery, mutual respect.
- Later reframed: also mentored **two junior backend engineers** to adapt to his standards, shielding them from harsh reviews and raising team-wide quality.

### Mentorship
- Fresh grad: hesitant to engage cross-team, coached to independence → promoted.
- Attitude issue engineer: disengaged, late, resistant → tried empathy, escalated when needed.

### Projects
1. **Project Churn**
   - First use of **Salesforce Event Bridge** in team.
   - Owned implementation, worked with product + Salesforce engineers.
   - Delivered successfully despite challenges.

2. **Pay for Performance**
   - Business logic hidden in large SQL query from analytics team.
   - Reverse engineered logic, designed production system with AWS Lambda + Step Functions + DynamoDB.
   - Staff engineer feedback led to design change (Postgres → DynamoDB).
   - Project not implemented due to ROI, but design remains for future.

3. **GDPR Data Purge Framework**
   - Cross-team GDPR compliance project.
   - Collaborated with staff engineers across Riders, Consumers, Restaurants.
   - Led TDD, coordinated stakeholders.
   - Framework based on Snowflake queries + Kafka consumers + deletion jobs.

4. **Compliance Sweep Automation**
   - Rebuilt compliance sweep process with AWS Step Functions + Lambda.
   - Used AI-assisted development to speed delivery.
   - Delivered scalable solution first time.

5. **Operational Excellence Initiative**
   - Service had very low operational excellence score.
   - Broke down issues, created backlog.
   - Incrementally fixed flaky tests, failing builds.
   - Improved score and gained team trust.
   - Manager started assigning high-visibility projects.

---

## Key Learnings Across Career
- **Infosys:** Learned regret of not pushing harder; importance of transferable skills.  
- **Wipro:** Learned rigor and documentation discipline, but pay disparity taught me to value roles where expectations and rewards align.  
- **J.P. Morgan:** Learned conflict resolution through competence, importance of visibility and speaking up.  
- **UpGrad:** Learned to take initiative, balance speed vs perfection, mentor juniors, and propose long-term architectural vision.  
- **Deliveroo:** Learned resilience (PIP recovery), staff-level collaboration (cross-team GDPR work), and the importance of uplifting juniors to handle conflicts and standards.
