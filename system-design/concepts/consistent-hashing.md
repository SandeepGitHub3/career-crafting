# Consistent Hashing — Quick Revision

> **Core idea:** Distribute data across servers by placing both data and servers on a circular "hash ring" — minimising data movement when servers are added or removed.

---

## The Problem with Simple Modulo Hashing

```
database_id = hash(event_id) % number_of_databases
```

Works fine until you add or remove a node:
- Adding DB4 → changes `% 3` to `% 4` → **almost every key remaps** → massive data movement
- Removing a DB → same issue, entire cluster reshuffles

❌ Not scalable. Enter **Consistent Hashing**.

---

## How Consistent Hashing Works

1. Create a **hash ring** (space of 0 → 2³² - 1, wraps around)
2. Place **servers** on the ring by hashing their names → fixed positions
3. Place **data** on the ring by hashing the key → walk **clockwise** to find the server

```
          0
          │
    DB4(75)○ ─────── ○ DB1(0/100)
         /               \
        /                 \
  DB3(50)○               ○ DB2(25)
        \                 /
         \               /
          ─────────────
```

**Adding a node (e.g. DB5 at position 90):**
- Only keys between 75–90 move (from DB1 → DB5)
- Everything else stays put ✅

**Removing a node (e.g. DB2 at 25):**
- Only DB2's keys move to DB3
- Everything else stays put ✅

---

## Virtual Nodes

**Problem:** Without virtual nodes, removing DB2 dumps ALL its load onto a single neighbour (DB3) → uneven load.

**Solution:** Each server gets **multiple positions** on the ring by hashing variations of its name:

```
hash("DB1-vn1") → pos 10
hash("DB1-vn2") → pos 45
hash("DB1-vn3") → pos 82
hash("DB2-vn1") → pos 20
hash("DB2-vn2") → pos 60  ...and so on
```

When DB2 fails → its virtual nodes' traffic spreads across DB1, DB3, DB4 evenly ✅

> More virtual nodes = more even distribution

---

## Handling Hot Spots

Consistent hashing distributes **keys** evenly — not necessarily **traffic**. A popular key (e.g. Taylor Swift concert) can still overwhelm one node.

| Strategy | How it helps |
|---|---|
| **Read replicas** | Replicate hot keys to multiple nodes, load-balance reads |
| **Key salting** | Append suffix `key-{0..9}` → scatter across nodes, aggregate reads |
| **Adaptive rebalancing** | Monitor traffic, move hot key ranges (DynamoDB does this automatically) |

> **Virtual nodes** fix structural imbalance (uneven key count). **Replication + salting** fix workload imbalance (uneven traffic).

---

## Data Movement in Practice

Consistent hashing tells you *where* data should live — it doesn't move it automatically.

- Most DBs (Cassandra, DynamoDB) use **replication** alongside consistent hashing
- On node failure → a **replica is promoted** (via Raft), no data moves
- Data only physically moves during **planned changes** (adding capacity), and even then only a bounded fraction of keys

---

## Real World Usage

| System | How it uses consistent hashing |
|---|---|
| **Cassandra** | Distributes data across the ring natively |
| **DynamoDB** | Partition placement under the hood |
| **CDNs** | Which edge server caches which content |
| **Redis Cluster** | Uses a *variation* — 16,384 fixed hash slots (`CRC16(key) % 16384`) instead |

> Redis Cluster's fixed slot approach is simpler but requires more coordination on rebalance — a real design trade-off worth mentioning.

---

## When to Use in an Interview

**Most interviews** → just mention that Cassandra/DynamoDB use consistent hashing under the hood. No need to go deep.

**Go deep when designing from scratch:**
- Distributed database
- Distributed cache
- Distributed message broker

**Key points to cover:**
1. Why modulo hashing fails at scale
2. How the hash ring works (clockwise lookup)
3. Virtual nodes for even load distribution
4. Hot spot mitigation (replication, key salting)
5. Replication handles failures — not rehashing

---

## Cheatsheet

| Concept | One-liner |
|---|---|
| Hash ring | Circle of hash space 0–2³², servers placed at fixed points |
| Key lookup | Hash the key → walk clockwise to first server |
| Adding node | Only 1/N of data moves (from clockwise neighbour) |
| Removing node | Only that node's data moves to next clockwise neighbour |
| Virtual nodes | Each server has multiple ring positions → even load |
| Hot spots | Solved by replication / key salting, not consistent hashing itself |
| Redis alternative | Fixed 16,384 hash slots instead of ring |
