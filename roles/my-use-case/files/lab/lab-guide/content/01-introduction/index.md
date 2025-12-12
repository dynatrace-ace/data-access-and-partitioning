## Introduction & Primary Grail Fields (10min)

## Introduction

You're responsible to execute the Proof-of-Concept for a new application onboarded into Dybatrace called "Easytrade".

## Warm Up

1. Open your Dynatrace environment, open a new notebook and fetch 1 spans. This is how you can check all metadata available for a single datapoint

```sql
fetch spans
| limit 1
```

![](../../assets/images/fetch_spans.png)


2. Copy the value of the java.jar.file property.

3. Open the Segments settings

![](../../assets/images/search_segment.png)

4. Create a new Segment, and filter Data (all types) with the java.jar.path. E.g.

```bash
java.jar.path = "/home/easytrade/app.jar" 
```

![](../../assets/images/segment_java.png)

See how java.jar.path is just available for spans? not quite a good fit for a tenant-wise configuration

5. Now let's use k8s.namespace.name to filter Data (all types). E.g.

```bash
k8s.namespace.name = "easytrade"
```

See how the metadata is available in all signals, a good fit for a tenant-wise configuration

![](../../assets/images/pgfallsignals.png)

## Close Up & Next Challenge

Well done, hopefully now you understand the importance of Primary Grail Fields

With OOTB Primary Grail Fields, you could directly configure IAM to give access to each team to their own namespace. The boundary and policy would look as follows

![](../../assets/images/iam_with_namespace.png)

This is the most simple scenario, but what if namespace is not enough to meet our requirements? E.g.

- there are other underlying technologies apart from k8s
- we should use app IDs defined in a k8s label
- needed higher granularity
- cost allocation is a must

### "there are other underlying technologies apart from k8s"

Teams under K8s are relying on k8s.namespace, but there are teams building apps on premise, and serverless.

Then we recommend a common metadata, we will define 3:
- dt.security_context
- dt.cost.costcenter
- dt.cost.product

Back to the presentation!