## Data Partitioning and Cost Allocation

Since easytrade is frowing fast and multiple teams are accessing logs and metrics across environments, performance and cost are becoming critical concerns.
To stay ahead, Easytrade engineers need to implement a bucket strategy to optimize log storage and query performance. At the same time, they’re introducing cost allocation tagging to track usage across teams and applications.
This lab will guide you through designing a log bucket strategy and applying cost allocation metadata to a VM — helping Easytrade scale smart, not just fast.

### 🎯 Learning Objectives

- Understand how buckets impact data retention, query performance, and cost.
- Design a log bucket strategy based on ingestion volume and dimensions.
- Learn how to apply cost allocation metadata using `dt.security_context`, `dt.cost.product`, and `dt.cost.costcenter`.


### Data Partitioning – Bucket Strategy for Logs

Why do buckets matter?

- Data Retention: Controls how long logs are stored - main use!
- Query Performance: Targeted buckets reduce scan time.
- Cost Efficiency: Less scan = lower DQL costs.

#### Exercise 1: Analyze Ingestion Volume

Use dimensions like app, stage, or team to estimate log volume.

Review the customer’s log ingestion volume per app. You can do that by fetching all logs for your k8s cluster and then applying any of the created segments that will lower the result size as well as improve the performance.

#### Exercise 2: Design Bucket Strategy

Choose the right dimension to partition logs - in this case, we can go with the namespace name.

1. Go to Settings > Storage Management 
2. Click on "+Bucket"
3. Create a new custom bucket for easytrade logs and choose your retention
4. Go to Settings > Process and Contextualize > Logs 
5. Add a new dynamic routing rule with a route = `k8s.namespace.name == "easytrade"`
6. Add a new pipeline and in the last stage of the pipeline, add the bucket asignment rule.
7. Fetch the logs again and check that your rule works.


# -TO-DO


#### Exercise 3: Connect Buckets to Access Control

Use IAM to restrict log access by bucket.


#### Exercise 4: Cost Allocation – Tagging a VM


