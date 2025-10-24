# ServiceNow Interview - 24-Oct-2025

## Round 1 Summary

**Role:** Staff Software Engineer  
**Interviewer:** Senior Engineering Manager  
**Focus:** Kafka Internals, Cluster Management  

---

### 1. Interview Flow

- **Intro:** Discussed team focus (Kafka infra) and my projects:
  - **AWS Lambda:** Compliance report  
  - **Kafka:** Event-driven leaderboard (UpGrad)  
- **Technical focus:** Kafka internals, replication, cluster management  

---

### 2. Key Technical Questions

**Q1. Kafka Broker Failure**  
- Topic: 3 partitions, replication factor 2, 3 brokers  
- Asked about leader election and replication if a broker crashes  
- **Response:** Explained application-level usage; lacked depth on ISR, leader election  

**Q2. Zero Downtime Kafka Upgrade**  
- Asked about upgrading a cluster without downtime  
- **Expected:** Rolling upgrades, in-sync replicas, offset management, possibly MirrorMaker  

**Q3. Code Review: `LegacyKafkaConsumer`**  

```java
// Reconstructed snippet
private KafkaConsumer<String, String> consumer;
private Map<String, String> sharedData = new HashMap<>();

public void consume() {
    while (true) {
        consumer.poll(Duration.ofMillis(100))
                .forEach(record -> processRecord(record));
    }
}

private void processRecord(ConsumerRecord<String, String> record) {
    String[] parts = record.value().split(",");
    if (parts.length > 2) throw new RuntimeException("Bad data");
    sharedData.put(parts[0], parts[1]); // unsafe access
}
```

### 3. Behavioral Questions

- Manager’s view on **strengths/weaknesses**  
- Preferred **team environment**  
- **5-year career goals**

---

### 4. Reflection

- Strong **project discussion**  
- Weak on **Kafka internals** (broker failover, ISR, replication)  
- Code review tested **fault tolerance & thread safety**  
- Behavioral answers were clear and structured  

---

### 5. Next Steps

1. Strengthen **Kafka internals** knowledge  
2. Learn **zero-downtime upgrade** process  
3. Improve **code review reasoning**  
4. Prepare concise **behavioral answers**
