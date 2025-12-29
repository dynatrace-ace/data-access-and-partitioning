## Introduction & Primary Grail Fields (10min)

## Introduction

In this session, you will learn how to work with Dynatrace Platform native features. This considers (but is not limited to) the following topics: 
- Enrichment at Source, Primary Grail Fields & Tags
- Data Access, IAM, Policies & Boundaries, dt.security_context
- Partitioning, Bucket Strategy, OpenPipeline routing
- Segmentation using Segments

By learning the Platform concepts, you will be able to use the Dynatrace Platform from scratch!

For our example today, you're responsible for executing the Proof-of-Concept for a new application onboarded into Dynatrace called "Easytrade".

## Warm Up

1. Open your Dynatrace environment, open a new notebook, and click the _plus_ icon to write a DQL to fetch one span. This is how you can check all fields and metadata available for a signal, as shown here as a record.

```sql
fetch spans
| limit 1
```

Change the view to "Record list" to have a nice overview of all fields. You can do this by clicking on Options->Record List on the DQL tile.

![](../../assets/images/fetch_spans.png)


2. Copy the value of the `java.jar.path` property.

3. Open the Segments settings by searching for Segments using the search bar in the top left menu bar

![](../../assets/images/search_segment.png)

Dynatrace segments are a way to organize and manage groups of monitored entities within your environment, such as hosts, services, or applications, based on shared characteristics or business logic. They allow you to define logical partitions that reflect your organizational structure, operational responsibilities, or specific use cases, making it easier to apply consistent settings, permissions, and monitoring configurations across related components. By using segments, teams can streamline governance, simplify data filtering, and ensure that monitoring aligns with business priorities.

4. Create a new Segment, and filter Data (all types) with the java.jar.path. E.g.

```bash
java.jar.path = "/home/easytrade/app.jar" 
```

![](../../assets/images/segment_java.png)

See how `java.jar.path` is just available for spans? not quite a good fit for a tenant-wise configuration

5. Now let's use `k8s.namespace.name` to filter Data (all types). E.g.

```bash
k8s.namespace.name = "easytrade"
```

Click on the Metrics/Logs/Events tab. Notice how the metadata is available on all signals, hence it's a very good fit for a tenant-wise configuration.

![](../../assets/images/pgfallsignals.png)

## Close Up & Next Challenge

Well done, hopefully now you understand the importance of Primary Grail Fields

With out-of-the-box permission relevant Primary Grail Fields, you could directly configure IAM to give access to each team to their own namespace. The boundary and policy would look as following:

<div align="center">
<img width="400" src="../../assets/images/iam_with_namespace.png">
</div>

This is the most simple scenario, but what if `k8s.namespace.name` is not enough to meet our requirements? E.g.

- There are other underlying technologies apart from k8s
- We should use app IDs defined in a k8s label
- Needed higher granularity
- Cost allocation is a must

### "There are other underlying technologies apart from k8s"

Teams using K8s are relying on `k8s.namespace.name`, but there are teams building apps on premise, and serverless.

As of today, we recommend using a common metadata structure and defining three key attributes:
- `dt.security_context`
- `dt.cost.costcenter`
- `dt.cost.product`

Back to the presentation!
