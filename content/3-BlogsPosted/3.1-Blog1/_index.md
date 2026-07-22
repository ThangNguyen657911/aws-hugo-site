---
title: "Blog1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# OPTIMIZING BIG DATA COST AND RELIABILITY: DEPLOYING REMOTE SHUFFLE SERVICE ON AMAZON EMR WITH APACHE CELEBORN

Link post blog: [Blog1](https://www.facebook.com/share/p/1TAk7UBeU9/).

During the process of optimizing Big Data processing systems running Apache Spark on AWS, I have synthesized a solution that completely resolves the trade-off between infrastructure cost and system reliability: **Using Apache Celeborn as a Remote Shuffle Service (RSS) on Amazon EMR**.

## The Classic "Pain Points" of Large-Scale Spark Shuffles

Organizations running large-scale Apache Spark workloads frequently face severe challenges related to the Shuffle phase (the exchange of intermediate data between stages), particularly when attempting to optimize costs using EC2 Spot Instances or when dealing with data skew:

* **Disruptions from Spot Instances causing costly recomputation:** Spot Instances help reduce compute costs by up to 90% compared to On-Demand, but they can be reclaimed with only a 2-minute warning. When a Spark executor running on a Spot Instance is terminated, its local shuffle data is lost entirely. Spark is forced to recompute all upstream stages to recreate that data. For jobs processing terabytes of data, this triggers a domino effect that delays runtime and completely erases the cost savings achieved from Spot Instances.
* **Local shuffle storage causing resource over-provisioning:** In traditional Hadoop architectures (including Amazon EMR on EC2), the External Shuffle Service (ESS) stores shuffle data directly on the local disks of individual Node Managers. This forces every node to provision large storage and memory capacities just to safeguard shuffle output, even though only a few nodes carry out the majority of the heavy lifting. This represents a critical bottleneck caused by the tight coupling of Storage and Compute.
* **Trapping idle compute resources, blocking Scale-in:** To prevent the loss of shuffle data, Spark's dynamic scaling logic prevents nodes holding active shuffle files from shrinking (scaling down). Consequently, EC2 nodes must sit idle for extended periods after tasks have finished, driving up wasted infrastructure costs.

---

## The Saving Grace: What is Apache Celeborn?

![Blog1](/images/blog1.jpg)

**Apache Celeborn** is an open-source Remote Shuffle Service (RSS) designed to completely decouple the lifecycle of shuffle data from the executor. Celeborn utilizes a Leader-Worker-Client architecture:

* **Leader nodes:** Manage cluster metadata.
* **Worker nodes:** Read and write shuffle blocks independently.
* **Clients:** Integrate directly into computing engines (such as Spark).

Instead of persisting shuffle data to the Spark executor's local disk, executors push data directly to a shared, storage-optimized Celeborn cluster.

> **Core Highlight:** Thanks to this push-based mechanism, Amazon EMR executor nodes can confidently run 100% on EC2 Spot Instances. If a Spot Instance is reclaimed, the shuffle data remains safely stored on the Celeborn cluster, allowing executors to freely scale in and out without triggering expensive stage recomputations.

---

## Production-Grade Solution Architecture Overview

In a real-world production deployment, it is highly recommended to run Celeborn on a dedicated Amazon EKS cluster that is completely isolated from the EMR compute environment (applicable to both EMR on EKS and EMR on EC2).

This separation offers massive benefits because these two workloads have entirely different resource profiles: Celeborn is heavily specialized in network and storage I/O, whereas Spark is deeply specialized in CPU and Memory. This allows teams to provision distinct, optimized EC2 instance types for each specific cluster.

* **Cross-cluster Connectivity:** Both the EMR cluster and the EKS cluster housing Celeborn reside within the same Amazon VPC and share private subnets. The AWS Load Balancer Controller on EKS provisions an internal Network Load Balancer (NLB) targeting the Celeborn pods. The EMR clusters simply configure their endpoint via `spark.celeborn.master.endpoints` pointing to this NLB address to consume the service over RPC port 9097.
* **State Persistence & Data Safety:** Celeborn's Primary/Leader nodes utilize the Raft consensus mechanism to manage cluster states, deployed as Kubernetes StatefulSets backed by Amazon EBS (gp3) volumes to ensure Raft logs survive pod restarts. Meanwhile, Celeborn Workers leverage local NVMe instance storage to achieve ultra-high shuffle read/write throughput. To compensate for the ephemeral nature of NVMe, the system enables partition replication across 2 different workers (`spark.celeborn.client.push.replicate.enabled=true`) to protect against data loss if a single worker fails.
* **Observability & Monitoring:** An AWS Distro for OpenTelemetry (ADOT) collector is deployed within the EKS cluster to scrape Prometheus metrics from Celeborn pods. These metrics are then forwarded to monitoring options like Amazon Managed Service for Prometheus and elegantly visualized via Amazon Managed Grafana to monitor JVM health, buffer allocation, and real-time shuffle performance metrics.

---

## Critical Configurations

To ensure seamless integration, you must override several default parameters for both the Spark Client and the Celeborn Server:

### 1. Spark Client Configurations (RSS Client)

These parameters are applied when submitting Spark jobs via the EMR Steps API or the Spark Operator:

```properties
spark.shuffle.service.enabled = false
spark.shuffle.manager = org.apache.spark.shuffle.celeborn.SparkShuffleManager
spark.celeborn.client.spark.push.unsafeRow.fastWrite.enabled = false
spark.dynamicAllocation.shuffleTracking.enabled = false
```

* `spark.shuffle.service.enabled = false`: Disables the default Spark External Shuffle Service.
* `spark.shuffle.manager = org.apache.spark.shuffle.celeborn.SparkShuffleManager`: Activates Celeborn's custom Shuffle Manager replacement.
* `spark.celeborn.client.spark.push.unsafeRow.fastWrite.enabled = false`: Disables Celeborn's UnsafeRow optimization to ensure seamless compatibility with Amazon EMR's highly optimized internal Spark runtime.
* `spark.dynamicAllocation.shuffleTracking.enabled = false`: Deactivates Spark's native shuffle tracking feature, handing full lifecycle management over to Celeborn.

### 2. Celeborn Server Configurations (RSS Server)

These values are configured via the Helm `values.yaml` file during EKS deployment:

```yaml
master.replicas = 3
worker.volumes = 4 × hostPath (/mnt/nvme/disk1-4)
```

* `master.replicas = 3`: Configures the minimum number of leader nodes required to maintain the Raft quorum for high availability.
* `worker.volumes = 4 × hostPath (/mnt/nvme/disk1-4)`: Maps and mounts the local NVMe storage directly to achieve maximum I/O bandwidth.

---

## Conclusion

Implementing a Remote Shuffle Service with Apache Celeborn on Amazon EMR proves that a Decoupled Storage-Compute architecture applies beautifully not just to the Data Lake tier (Amazon S3) but also to transient intermediate stages (Shuffle Data).

This solution completely eliminates the fear of Spot Instance interruptions, optimizes cluster utilization, and unlocks the true potential of Spark's Auto-scaling capabilities. You no longer have to choose between a cost-effective infrastructure or a stable production pipeline — Celeborn gives you both on Amazon EMR.

Refer to the official source material at: [aws.amazon.com/vi/blogs/big-data/high-performance-remote-shuffle-service-on-amazon-emr-with-apache-celeborn](https://aws.amazon.com/vi/blogs/big-data/high-performance-remote-shuffle-service-on-amazon-emr-with-apache-celeborn/).

Is anyone else experiencing a nightmare with shuffle data costs or Spot instance terminations? Let's discuss it in the comments below!