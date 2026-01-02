## Management Zones to Segments

The team uses an `Easytrade` Management Zone to move across the environment and find their relevant entities. For example the team is using the Management Zone to find their relevant services, to spot performance degradations

![](../../assets/images/serviceclassicfilter.png)

The distributed traces view is another interesting one for the team, to find relevant failed requests & exceptions, and later convert them into metrics & alerts in case necessarely

![](../../assets/images/ppclassic.png)

Segments are the equivalent capability in 3rd Gen, and along with Enrichment at Source, they bring some key benefits that we will discover during the lab

1. Within your Dynatrace tenant, search for the `Segments` settings 

![](../../assets/images/searchsegment.png)

2. Create a new Segment, name it `app`, and enter a variable

![](../../assets/images/segmentvariable.png)

Management Zones used to be each a single configuration object. E.g. there was an `Easytrade` management zone with their respective rules, and many others for others apps, environments & bu. Segments is a `key:value` configuration types, then we have the define the key (that is the name), and the values that are going to be the variables.

3. Add the following as the variable definition, click on run to test, and save the changes

```sql
fetch spans
| dedup dt.entity.host, dt.entity.process_group_instance, dt.smartscape.service

// extract primary grail fileds & tags defined
| fields dt.host_group.id, dt.security_context, dt.cost.costcenter, dt.cost.product,
         dt.entity.host, dt.entity.process_group_instance, dt.smartscape.service, span.id

// filter for classic entities
| fieldsAdd tags = concat("application:", dt.security_context)
| summarize count = count(), by:{dt.security_context, tags}
```

![](../../assets/images/addvariablesave.png)

4. Filter `All Data` with the Primary Grail Field, in our case, the dt.security_context, value where we're extracting the app name. Then click in Preview.

![](../../assets/images/filteralldata.png)

See how all datapoints are getting enriched with the previously configured Primary Grail Field. And also notice how dt.security_context doesn't work for `Classic Entities`. This is meant to be like this, since it is a pure 3rd Gen configuration, and applies just to the "New" entities. And this is the reason why we've created the 2nd variable

```sql
| fieldsAdd tags = concat("application:", dt.security_context)
```

![](../../assets/images/classicentities.png)

5. Click in More, and add Host

![](../../assets/images/morehost.png)

6. Filter by tags, use the "tag" variable value, and preview the results

![](../../assets/images/hostappear.png)

7. Click in related entity, add process group

![](../../assets/images/relatedpg.png)

8. Do the same for process & service

![](../../assets/images/sameforservice.png)

9. Click on preview to check if it works

![](../../assets/images/validate.png)



### Close Up

Now our users can navigate across 3rd Gen apps as they did in classic, and removed some of the classic apps to ensure consistency.

If the 3rd Gen app doesn't satisfy yet the requirements of the team as the classic was, please reach out to us for feedback!