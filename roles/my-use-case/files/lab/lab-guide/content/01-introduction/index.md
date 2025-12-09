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

```py
java.jar.path = "/home/easytrade/app.jar" 
```

![](../../assets/images/segment_java.png)

See how java.jar.path is just available for spans? not quite a good fit for a tenant-wise configuration

5. Now let's use k8s.namespace.name to filter Data (all types). E.g.

```py
k8s.namespace.name = "easytrade"
```

See how the metadata is available in all signals, a good fit for a tenant-wise configuration

## Close Up

Well done, hopefully now you understand the importance of Primary Grail Fields



