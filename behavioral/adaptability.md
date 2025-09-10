# Adaptability

## Story 1: Deliveroo - Restaurant Status Approval Flow

**Situation**  
- Joined Deliveroo as a **Senior Engineer** after 12+ years working primarily in Java and backend stacks.  
- Deliveroo’s systems were built in **Golang, Ruby, and Scala**, none of which I had prior experience with.  
- Company had not yet established an **India entity** when I accepted the offer → risky, ambiguous environment.  
- First project: compliance-critical **restaurant enable/disable flow** required stronger auditability and accountability.  
- Legacy Ruby monolith lacked audit controls: anyone could flip restaurant status via UI; user IDs not tracked.  
- This was risky for the business, especially when restaurants were disabled for **food safety or legal violations**.  

**Task**  
- Ramp up quickly on unfamiliar tech stacks while delivering a solution under a **1-month compliance deadline**.  
- Design and implement a **maker-checker process** for restaurant status changes with full audit history.  
- Act as the **sole backend engineer** in a Salesforce-heavy team, responsible for integrations.  
- Align with **product, Salesforce engineers, account managers, and legacy system owners** to agree on solution approach.  
- Balance **learning curve vs. delivery speed** to meet compliance requirement.  

**Action**  
- Learned **just enough Golang and Ruby** to code effectively, instead of trying to master them upfront.  
- Balanced half-day onboarding with **requirement gathering and design discussions** in the first two weeks.  
- Discovered Scala components unexpectedly → studied existing flows and reused them for speed.  
- Designed integration between Salesforce (account managers’ primary tool) and backend systems.  
- Leveraged Salesforce to implement maker-checker + audit reporting.  
- Coordinated approvals from legacy system owners who resisted extending the soon-to-be-decommissioned monolith.  
- Took ownership of all backend integration aspects and delivered smaller reliability fixes (flaky tests, Terraform builds) to build trust.  

**Result**  
- Delivered the compliance solution within the **1-month deadline**, despite new tech and team setup.  
- Implemented maker-checker flow that introduced **full accountability** for restaurant status changes.  
- Enabled **audit reporting** via Salesforce, tracking who enabled/disabled restaurants and why.  
- Reduced business risk by ensuring food safety/legal compliance issues were traceable.  
- Approach of leveraging Salesforce as workflow + audit layer became a **pattern for other compliance initiatives**.  
- Built credibility early in Deliveroo as someone who could **adapt quickly, deliver under ambiguity, and align multiple teams**.  

---

### Paragraph Version

When I joined Deliveroo as a Senior Engineer, I came from 12+ years of Java experience, but Deliveroo’s systems were almost entirely in Golang, Ruby, and Scala — languages I had no prior background in. To add to the challenge, Deliveroo had not yet established an India entity when I accepted the offer, so it was a risky and ambiguous environment. My very first assignment was a compliance-critical project: the restaurant enable/disable flow needed stronger auditability. The existing Ruby monolith allowed anyone with access to flip restaurant status, but it didn’t capture user IDs or reasons, creating risk for the business, especially if a restaurant was disabled due to food safety or legal violations.  

The task was to deliver a solution within just one month. As the sole backend engineer embedded in a Salesforce-heavy team, I was responsible for designing a maker-checker process with full audit history, handling all backend integrations, and aligning product, Salesforce engineers, account managers, and legacy system owners. This meant I had to adapt simultaneously to new technologies, a new company setup, and a different engineering culture — all under strict compliance deadlines.  

I approached this by focusing on outcomes rather than depth. I learned just enough Golang and Ruby to be effective, balanced onboarding sessions with requirement gathering from product and account managers, and discovered Scala components midstream that I adapted to by reusing existing flows. I designed an integration where Salesforce served as the maker-checker and audit layer, since it was already the account managers’ primary tool, and built reporting to capture exactly who enabled or disabled restaurants and why. Alongside the project, I also fixed flaky tests and Terraform builds to show reliability and build trust with my new team.  

The result was that we delivered the compliance solution on time, implementing a maker-checker process that introduced full accountability for restaurant status changes. Audit reporting was enabled through Salesforce, reducing business risk and satisfying compliance needs. Importantly, this integration approach became a reusable pattern for other compliance initiatives. For me, it was a Staff-level lesson: adaptability isn’t just about learning new languages — it’s about thriving in ambiguity, influencing across teams, and creating solutions that scale beyond a single project.  
