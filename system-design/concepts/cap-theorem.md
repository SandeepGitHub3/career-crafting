# CAP Theorem — Quick Revision

> **Core idea:** In a distributed system, you can only guarantee **2 of 3**: Consistency, Availability, Partition Tolerance.

---

## The 3 Properties

| Property | Meaning |
|---|---|
| **Consistency (C)** | All nodes see the same data at the same time. Every read returns the latest write. |
| **Availability (A)** | Every request gets a response — but data might be stale. |
| **Partition Tolerance (P)** | System keeps working despite network failures between nodes. |

> ⚠️ **CAP Consistency ≠ ACID Consistency.** CAP = same data across nodes. ACID = data integrity rules.

---

## The Real Tradeoff

**P is non-negotiable** — network failures always happen. So the real choice is:

```
CP  →  Consistency + Partition Tolerance  (may reject requests to stay consistent)
AP  →  Availability + Partition Tolerance  (responds with possibly stale data)
```

**The one question to ask:** *"Would it be catastrophic if users briefly saw inconsistent data?"*
- **YES** → Choose Consistency
- **NO** → Choose Availability (eventual consistency is fine)

---

## When to Choose What

| Consistency (CP) | Availability (AP) |
|---|---|
| Ticket booking (no double-booking) | Social media profiles |
| E-commerce inventory | Netflix content descriptions |
| Financial / stock trading | Review sites (Yelp hours) |
| Bank balances | DNS |

---

## Design Implications

**If Consistency →**
- Single-node DB, or distributed transactions (2PC)
- Higher latency, may error during partition
- Tech: PostgreSQL, MySQL, Google Spanner, DynamoDB (strong mode)

**If Availability →**
- Multiple read replicas + async replication, CDC
- Always responds, may serve stale data
- Tech: Cassandra, DynamoDB (multi-AZ), Redis clusters

---

## Consistency Spectrum (Senior Level)

| Model | What it means | Example |
|---|---|---|
| **Strong** | Every read = latest write | Bank balances |
| **Causal** | Related events in same order for all | Comments appear after their post |
| **Read-your-own-writes** | You see your updates immediately; others may not | Your own profile edits |
| **Eventual** | Will sync over time, temporarily stale | DNS, social feeds |

---

## Mixed Requirements (Real Systems)

Most real systems need **both** — feature by feature:

- **Ticketmaster:** Booking → Consistency | Browsing events → Availability
- **Tinder:** Matching → Consistency | Viewing profiles → Availability

💬 *Say in interview: "I'll prioritize consistency for X, but optimize for availability for Y."*

---

## Interview Cheatsheet

- Bring up CAP during **non-functional requirements** phase
- Real choice = **CP vs AP** (P is always required)
- Most systems → **AP** (eventual consistency is fine)
- Finance, inventory, bookings → **CP** (stale = catastrophic)
