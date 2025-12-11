## Data Segmentation

With data access already sorted out, let's create Segments to filter our data across different Dynatrace views based on each team component

1. Go to the Segments settings, and click on + Segment

![](../../assets/images/segments_setting.png)

2. Call it app, and create a variable

![](../../assets/images/variablesegment.png)

3. Paste the following code, preview and done

```sql
fetch spans
| dedup dt.entity.host, dt.entity.process_group_instance, dt.smartscape.service
| fields dt.host_group.id, dt.security_context, dt.cost.costcenter, dt.cost.product,
         dt.entity.host, dt.entity.process_group_instance, dt.smartscape.service, span.id
| summarize count = count(), by:{dt.security_context}
```

![](../../assets/images/variablesegmentconfig.png)


4. Add the data to the segment, use the recently created filter. Click on Preview and see how all data types are part of the segment

dt.security_context = $dt.security_context 

![](../../assets/images/segmentresults.png)

> Tip: for k8s events are not yet enriched, but you can use the host group defined in the dynakube

5. Check if the Segment is working in the Distributed Traces & Logs App

![](../../assets/images/segmentspans.png)

![](../../assets/images/segmentlogs.png)