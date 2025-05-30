---

## **Starta miljön**

1. Starta Kafka-miljön med:

   ```bash
   docker compose up -d
   ```

2. Öppna Kafdrop UI i webbläsaren:

   ```
   http://localhost:9000
   ```

3. För att stänga ner miljön:

   ```bash
   docker compose down
   ```

---

## **Test via CLI:**

```bash
# Skapa en topic för testmeddelanden:
docker exec -it kafka1 /opt/kafka/bin/kafka-topics.sh \
  --create --topic test-topic \
  --partitions 3 --replication-factor 3 \
  --bootstrap-server kafka1:9092

# Skicka ett testmeddelande:
echo "Hello Kafka!" | docker exec -i kafka1 /opt/kafka/bin/kafka-console-producer.sh \
  --broker-list kafka1:9092 \
  --topic test-topic

# Läs testmeddelandet:
docker exec -it kafka2 /opt/kafka/bin/kafka-console-consumer.sh \
  --bootstrap-server kafka2:9094 \
  --topic test-topic \
  --from-beginning --max-messages 1
```

---
