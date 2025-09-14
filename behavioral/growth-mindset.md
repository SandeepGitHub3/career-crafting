# Growth Mindset / Personal Development

## Questions
1. Tell me about a time you realized you needed to change your leadership style.
2. Describe a situation where you identified a personal gap and how you addressed it.
3. What’s an example of how you’ve grown in your role over the past year?
4. Give me an example of when you had to let go of control to help your team succeed.

## Story 2: UpGrad – Real-Time Leaderboard with Kafka & Redis

**Situation**  
- Tech Lead (IC) at an education platform, leading two junior engineers on the learner engagement team.  
- Tasked with building a **real-time leaderboard** to rank learners by daily reading time and boost course completion rates.  
- Scale challenge: cohorts of 250–300 learners, many active simultaneously during peak hours.  
- Traditional PostgreSQL aggregation queries too slow for real-time needs → latency and scalability risks.  
- Critical cohorts launching soon, so solution needed to be reliable and production-ready.  

**Task**  
- Design and implement a **scalable leaderboard system** that aggregated reading times and updated rankings in real time.  
- Solve both **data aggregation** and **fast querying/sorting** challenges.  
- Ensure the solution scaled across multiple cohorts, not just one.  
- Close personal **knowledge gaps** in distributed streaming and Redis data structures.  

**Action**  
- Explored traditional DB approaches (views, Lambdas, DynamoDB) but found them insufficient.  
- Hit a bottleneck: could solve either aggregation or querying, not both at scale.  
- Recognized knowledge gap in **Kafka Streams** and **Redis beyond caching**.  
- Proactively sought guidance from the architect during lunch → got suggestion to pair Kafka Streams with Redis.  
- Researched extensively, read docs, ran experiments to upskill quickly.  
- Built solution:  
  - **Kafka Streams** consumed and aggregated reading time data in real time.  
  - Aggregates periodically flushed into **Redis Sorted Sets**, which automatically ranked learners for fast queries.  
- Delivered system for upcoming cohort launches.  
- Created a **GitHub exercise/training module** to teach the approach.  
- Shared with team → later adopted as a **training resource across multiple teams**; some teams even reused the Kafka+Redis pattern for their own needs.  

**Result**  
- Successfully delivered a **real-time leaderboard** that scaled across multiple cohorts and met latency requirements.  
- Feature launched on time for critical cohorts, improving learner engagement and motivation.  
- Personally grew by mastering Kafka Streams and Redis as a data store.  
- Impact extended beyond my project:  
  - GitHub exercise became a **cross-team learning tool**.  
  - Other teams used it to train engineers and in some cases, **adopted the same design pattern**.  
- Reflection: Growth mindset at Staff level is about more than closing your own knowledge gaps — it’s about **seeking feedback, learning fast, and turning personal growth into organizational capability**.  


### Paragraph Version

At UpGrad, I was leading two junior engineers on the learner engagement team, and we were tasked with building a real-time leaderboard to rank 
learners by daily reading time. The scale challenge was significant: 250–300 learners per cohort, many active simultaneously during peak evening 
hours. Our traditional PostgreSQL approach couldn’t handle the latency requirements — aggregation queries were too slow — and with important 
cohorts launching soon, we needed a scalable solution fast.  

I initially explored traditional approaches like database views, DynamoDB, and Lambdas, but none could solve both the aggregation and 
querying challenges at scale. I realized I had a knowledge gap in distributed streaming and Redis beyond basic caching. Instead of struggling 
in isolation, I approached our architect casually during lunch, and he suggested exploring Kafka Streams with Redis. That opened a new direction 
for me. I dived into research, studied the documentation, and ran experiments until I was confident enough to build.  

The final solution used Kafka Streams to consume and aggregate reading time data in real time, flushing results into Redis Sorted Sets 
that automatically ranked learners. This provided lightning-fast queries while handling scale across cohorts. The system launched on time, 
supported hundreds of learners per cohort, and met all latency requirements during peak hours.  

The biggest lesson came afterwards: I turned my personal growth into organizational growth. I created a GitHub exercise to explain the approach, 
which my juniors used to learn Kafka and Redis. Over time, the exercise spread beyond our team — other teams used it as a training resource, 
and some even adopted the Kafka+Redis pattern for their own real-time systems.  

For me, this reinforced that a growth mindset at the Staff level is not just about closing your own gaps. It’s about recognizing limits, 
seeking the right input, learning fast, and then scaling that learning so the whole organization grows with you.  
   
## Story 2: Deliveroo – Restaurant Churn Project (Post-Leave Bottleneck)

### Bullet-Point STAR (Staff-Level Reframed)

**Situation**  
- Senior Software Engineer at Deliveroo, leading the **Restaurant Churn project** to disable inactive restaurants.  
- Designed the entire technical approach and documented it before taking a month-long marriage leave.  
- Three junior engineers in India implemented the project while I was away, with support for reviews and unblockers.  
- When I returned, the project went live, but **all post-launch stakeholder questions** from product and account managers were funneled through me.  
- I had unintentionally become the **single point of failure** → bottlenecked stakeholder communication and blocked my ability to focus on higher-impact initiatives (e.g., GDPR retention).  

**Task**  
- Break the dependency chain where all queries went through me.  
- Empower the junior engineers to **directly handle stakeholder questions**.  
- Build sustainable processes that reduced reliance on a single person.  
- Free myself to focus on **Staff-level responsibilities**: architectural work, compliance initiatives, and mentoring.  
- Create visibility and growth opportunities for the junior engineers.  

**Action**  
- **Created a dedicated Slack channel** for churn discussions, bringing product, account managers, and engineers together → eliminated fragmented DMs.  
- Wrote **lightweight documentation** showing how to troubleshoot common issues → reduced repetitive questions.  
- Established a **rotation system** for handling stakeholder queries → each engineer took turns as first responder.  
- Encouraged and coached juniors to **ask clarifying questions** and engage directly with stakeholders.  
- Modeled conversations at first, then deliberately stepped back, only intervening for edge cases.  
- Practiced **letting go of control**, adapting to different working styles (e.g., teammates preferring detailed comments vs. self-documenting code).  
- Pushed myself beyond introversion to **mentor more actively**, focusing on encouragement, reassurance, and trust-building.  

**Result**  
- Within one sprint (~2 weeks), junior engineers were **independently handling stakeholder questions** without escalation.  
- Account Managers and Product Managers began recognizing juniors as **subject-matter experts**, giving them visibility and trust.  
- Stakeholders benefited from **faster responses** since they no longer had to wait for me.  
- I freed significant time to focus on **cross-team GDPR compliance work** and learning new technologies.  
- The **process became scalable**: a repeatable model for distributing stakeholder communication that outlasted me.  
- Personal growth: learned that at Staff level, growth mindset means **changing leadership style — stepping back, empowering others, and building systems that scale team capacity instead of relying on individual heroics**.  

---

### Paragraph Version

At Deliveroo, I was leading the Restaurant Churn project to identify and disable inactive restaurants. Before taking a month of marriage leave, 
I designed the entire technical approach and documented it so that three junior engineers in India could implement it. When I returned, 
the project had gone live successfully, but I quickly discovered a problem: all stakeholder questions from product and account managers were 
being directed to me. This created a bottleneck — if I was unavailable, no one could answer, and it prevented me from focusing on higher-level 
architectural work such as the GDPR data retention project.  

I realized that my leadership approach needed to evolve. Instead of continuing to act as the sole point of contact, I made it my priority to 
enable the junior engineers to take ownership of stakeholder communication. I created a dedicated Slack channel to centralize discussions, 
wrote lightweight documentation to reduce repetitive queries, and established a rotation system so each engineer could practice being the 
first responder. I modeled conversations at first, then deliberately stepped back, only joining for complex cases. I encouraged them to ask 
clarifying questions directly to stakeholders and reassured them that curiosity was a strength, not a weakness. This was a growth moment for 
me as well: as a natural introvert, I pushed myself to mentor more actively and to let go of control, trusting different working styles.  

Within just one sprint, the junior engineers were independently handling all stakeholder questions. Stakeholders benefited from faster responses, 
and Account Managers began to recognize the juniors as go-to experts, boosting their confidence and visibility. For me, the biggest change was 
that I freed up significant time to focus on strategic work, while also realizing that leadership at the Staff level is about stepping back and 
building systems that empower others. This experience taught me that personal growth isn’t just about learning new technologies — it’s about 
evolving your leadership style to scale your team’s effectiveness beyond your own direct contributions.  
