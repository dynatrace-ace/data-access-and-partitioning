## Data Segmentation

With data access already sorted out, let's create Segments to filter our data across different Dynatrace views based on each team component

1. Go to the Segments settings, and click on **"+ Segment"**

![](../../assets/images/segments_setting.png)

2. Call it **"App"**, and create a variable by clicking on **"+ Variable"**.

<div align="center">
<img width="400" src="../../assets/images/variablesegment.png">
</div>

3. Paste the following code, preview it and save it.

```sql
fetch spans
| dedup dt.entity.host, dt.entity.process_group_instance, dt.smartscape.service
| fields dt.host_group.id, dt.security_context, dt.cost.costcenter, dt.cost.product,
         dt.entity.host, dt.entity.process_group_instance, dt.smartscape.service, span.id
| summarize count = count(), by:{dt.security_context}
```

![](../../assets/images/variablesegmentconfig.png)


4. Now, let's make sure we provide a filter which this Segment will be based on. **"Data (all types)"** is already pre-selected for you. All you need to do is add the filter. let's do that:

Please add - `dt.security_context = $dt.security_context`

![](../../assets/images/segmentresults.png)

> Note: K8s events are not enriched yet, but you can use the host group defined in the dynakube.

5. Check if the Segment is working in the Distributed Traces & Logs App

![](../../assets/images/segmentspans.png)

![](../../assets/images/segmentlogs.png)

Good job! Back to the slides for some theory.