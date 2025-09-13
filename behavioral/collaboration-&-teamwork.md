# Collaboration & Teamwork

## Questions
1. Give an example of a time when you worked well in a team.  
2. Tell me about a time when you had to collaborate with others to chieve a goal.
   
## Story 1: Deliveroo – GDPR Data Purge Framework

**Situation**  
- Company needed to implement a GDPR Data Purge framework for its legacy Ruby monolith with a **Q3 deadline** (one quarter to complete).  
- No single team owned the monolith → ownership distributed across **Restaurants, Riders, and Consumers**.  
- Multiple teams involved:  
  - **Legal** → defined data categories and retention policies.  
  - **Analytics** → identified data to be purged and provided utilities in Go.  
  - **Finance** → clarified requirements for financial data retention.  
  - **Engineering domain teams** → Restaurants (me), Riders, Consumers.  
- Technical stack mismatch: Analytics utilities only available in **Go**, but monolith built in **Ruby**.  
- Different data categories had different retention rules (e.g., financial vs. general restaurant info).  
- Analytics team would publish purge data via **SQS messages**, with utilities for S3 backup, rollback, and retention.

**Task**  
- Deliver a **unified purge framework** to ensure GDPR compliance.  
- Coordinate across six different teams to avoid fragmented approaches.  
- Bridge technical gap between **Go utilities** from Analytics and **Ruby-based monolith**.  
- Ensure consistent compliance handling across all domains, including special rules for financial data.  
- Provide a solution that minimized disruption to ongoing monolith work.  

**Action**  
- Initially, each domain engineer scoped their own purge solution → created duplication and risk of inconsistency.  
- In early syncs, raised concerns that this would result in **three divergent implementations**, increasing audit risk.  
- Identified this as a turning point and **proposed a unified framework**.  
- Stepped up to own the **Technical Design Document (TDD)**: captured requirements, defined architecture, and clarified ownership boundaries.  
- Acted as **primary backend engineer** for Restaurants while coordinating with Staff Engineers from Riders and Consumers.  
- Drove alignment by systematically following up with Legal and Finance on retention rules.  
- Designed a two-part solution:  
  - A **Ruby service** in the monolith exposing get/delete/restore APIs.  
  - A **Go service** consuming SQS messages, calling Ruby APIs, and leveraging Analytics utilities for backup and rollback.  
- Ensured reviewers signed off on TDD → all teams started from the same blueprint.  

**Result**  
- Delivered a **unified GDPR purge framework design** adopted by all three domain teams.  
- Avoided duplication and fragmentation by creating **one standardized compliance pattern**.  
- Built the solution as a separate service → minimized disruption to ongoing monolith work.  
- Enabled integration of Analytics Go utilities despite Ruby constraints.  
- Reduced maintenance overhead and **lowered audit/compliance risk** through consistency.  
- Legal and Finance teams praised the single standardized process → easier to audit, less risky.  
- Framework became a **repeatable blueprint** for future compliance initiatives.  
- Lesson: at Staff level, the biggest contribution was not coding, but **creating alignment, shared ownership, and an org-wide scalable solution**.  

---

### Paragraph Version

At Deliveroo, we faced a critical Q3 deadline to implement a GDPR-compliant data purge framework for our legacy Ruby monolith. The challenge was complex: no single team owned the application, so ownership was distributed across the Restaurants, Riders, and Consumers domains. Six groups were involved overall — Legal, Analytics, Finance, and three engineering domain teams. Legal defined data categories and retention policies, Analytics provided purge utilities in Go and published data to be purged via SQS, Finance clarified requirements for financial data, while the engineering teams had to integrate this into the monolith. The technical mismatch made things harder: Analytics’ utilities were in Go, while the monolith was in Ruby, and different data categories had different retention rules.  

Initially, each domain engineer began scoping their own purge solution, but in early sync meetings it became obvious that this was leading to duplication and inconsistency. We were on track to create three different approaches to the same compliance problem, which would have created audit risk and long-term maintenance headaches. Recognizing this as a turning point, I stepped up to propose a unified framework and took ownership of drafting the technical design document. In it, I captured requirements, defined a common architecture, and clarified ownership boundaries. I then actively followed up with Staff Engineers from Riders and Consumers, as well as with Legal and Finance stakeholders, to align on retention policies and data handling rules.  

The final design used a two-part solution: a Ruby service in the monolith exposing get/delete/restore APIs, and a Go service that consumed SQS messages, called the Ruby APIs, and leveraged Analytics’ utilities for S3 backup and rollback. By driving consensus and getting reviewers to sign off on the TDD, all teams could start execution from the same blueprint.  

The result was a unified purge framework that all three domain teams adopted. This avoided fragmentation, reduced audit risk, and minimized disruption to ongoing monolith work by keeping the solution as a separate service. The framework became a reusable blueprint for future GDPR compliance initiatives, which Legal and Finance particularly appreciated because they only had to audit a single consistent process. For me, the key lesson was that at the Staff level, collaboration isn’t just about working well with others — it’s about creating clarity, building alignment, and enabling scalable solutions across organizational boundaries.  
