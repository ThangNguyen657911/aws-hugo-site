---
title: "Blog 3"
date: 2024-01-03
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only, please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# BUILDING A LARGE-SCALE REAL-TIME ANOMALY DETECTION SYSTEM WITH RAZORPAY AND AMAZON MSK

When operating large-scale financial and payment systems, every second of delay in detecting anomalies means failed transactions, lost revenue, and eroded customer trust.

Today, I would like to share the architecture of the **ADA (Anomaly Detection and Alerting)** system – the real-time anomaly detection and fraud prevention platform of Razorpay (one of India's largest Fintechs) built on **Amazon Managed Streaming for Apache Kafka (Amazon MSK)** and **Apache Flink**. This system helps Razorpay process over 5 billion events per day, detect incidents in under 30 seconds, and cut monitoring costs by up to 80%.

---

## The Challenge: When Static Thresholds Collapse at Scale

Prior to building ADA, Razorpay’s legacy monitoring system (based on Pinot + ThirdEye) hit its limits as the company grew rapidly, reaching over 500 million transactions per month:

* **Monitoring Blind Spots:** System degradation or drops in Success Rate (SR) were only detected after customers complained. Under manual operation, thousands of transactions had already failed before human operators could react.
* **Fraud at Velocity:** Attacks like card-testing and limit abuse demand detection in under 1 minute—a requirement where traditional batch-processing systems are completely helpless.
* **Alert Fatigue:** Configuring static thresholds created a dilemma: setting them too tight flooded operators with false alarms, while setting them too loose allowed actual attacks to slip through.
* **Cost Scale with Complexity (High Cardinality):** Monitoring individual merchants separately cost up to $500K/year with a minimum query latency (SLA) of 1–2 minutes, making it completely unscalable.

---

## ADA Architecture: Amazon MSK as the Streaming Backbone

To fundamentally resolve these limitations, Razorpay completely re-architected its system with a **Decoupled Data Pipeline**, placing **Amazon MSK** at the center of data orchestration.

![Blog3](/images/blog3.jpg)

This architecture operates based on the following core components:

### 1. High-Performance Ingestion Layer with Amazon MSK
* **All Change Data Capture (CDC) events** from core databases (Amazon Aurora MySQL) via Debezium, along with application events, are pushed directly into Kafka topics managed by Amazon MSK.
* **Tenant-Partitioned Topics:** Data from different business lines (Payments, Payroll, Banking) is logically isolated into dedicated topics while sharing the same physical MSK cluster infrastructure, ensuring independent throughput SLAs and optimizing costs.
* **Absolute Reliability Guarantees:** The MSK cluster is deployed across 3 Availability Zones (AZs) with high data durability configurations: `replication.factor=3`, `min.insync.replicas=2`, and `acks=all` on the producer side. This configuration completely eliminates the risk of data loss or ingestion pipeline disruption when a broker fails.

### 2. Stateful Stream Processing with Apache Flink
Apache Flink acts as the stateful computation engine, continuously consuming data from MSK with exactly-once semantics. The processing pipeline consists of 5 core stages:
* **Kafka Source:** Ingests raw data streams from MSK.
* **Watermarking:** Handles late-arriving events with a fault tolerance threshold of up to 2x the window size.
* **Windowed Aggregation:** Aggregates data by Merchant and dynamically calculates key metrics (success rate, latency, volume).
* **Async I/O Lookup:** Performs non-blocking asynchronous queries (supporting up to 1,024 concurrent connections) to ClickHouse to retrieve pre-computed baseline data.
* **Rule Evaluation:** Evaluates real-time streams against baselines using machine learning algorithms or Complex Event Processing (Flink CEP) to immediately detect fraud patterns (e.g., 5 consecutive declines followed by a success).

### 3. Decoupling Rules via AdaDSL
The most valuable aspect of ADA is the complete decoupling of **Rule Definition** from **Infrastructure Execution**. Razorpay developed a human-readable, declarative domain-specific language called AdaDSL.
* When operations team members update a rule, the definition is serialized and pushed to a dedicated Kafka snapshot topic on MSK.
* Flink consumes this topic as a **Broadcast Stream**, dynamically applying the new logic to all running pipeline threads in real-time (**Hot-reload**) without requiring system restarts or code redeployments.

---

## Breakthrough Results and Key Lessons

The ADA platform running on Amazon MSK delivered outstanding operational improvements for Razorpay:

* **80% reduction** in infrastructure costs compared to the legacy architecture.
* Anomaly detection latency dropped from several minutes to **under 30 seconds**.
* **90% reduction** in false alerts thanks to dynamic, calendar-aware baselines that adapt to schedules, holidays, and specific hours of the day.
* Sustained **99.99% Uptime** commitment for the entire monitoring ecosystem.

---

## Conclusion

**Key Takeaway for System Engineers:** For high-throughput transaction processing systems, investing in a robust streaming backbone like Amazon MSK from the start is not just an optimization—it is a prerequisite for stable operations. Decoupling the event producers from the consumer-processors allows you to scale and customize features freely (such as integrating predictive ML models or LLMs for Root Cause Analysis) without impacting the customers' primary payment flows.

Reference source: [aws.amazon.com/blogs/big-data/how-razorpay-built-real-time-anomaly-detection-with-amazon-msk](https://aws.amazon.com/blogs/big-data/how-razorpay-built-real-time-anomaly-detection-with-amazon-msk/).

What are your thoughts on Razorpay's real-time anomaly detection model? Feel free to leave a comment and discuss below!