## Management Zones to Segments

The team uses an `Easytrade` Management Zone to move across the environment and find their relevant entities. For example, the team is using the Management Zone to find their relevant services and to spot performance degradations.

![](../../assets/images/serviceclassicfilter.png)

The Distributing Tracing view is another interesting one for the team. This view is used to find relevant failed requests and exceptions which they later convert to metrics and alerts

![](../../assets/images/ppclassic.png)

**Segments** are the equivalent capability in the new 3rd Gen Platform. Along with Enrichment at Source, they bring some key benefits and value components that we will discover during the lab

1. Within your Dynatrace tenant, search for the `Segments` settings as shown below:

![](../../assets/images/searchsegment.png)

2. Click on the **"+ Segment"** button to create a new Segment. Name it `app` and create a variable by clicking on **"+ Variable"**.

![](../../assets/images/segmentvariable.png)

Management Zones used to be each a single configuration object. E.g. there was an `Easytrade` management zone with their respective rules, and many others for others apps, environments & business units. Segments is a `key:value` configuration: we define the key (that is the name), and the values that are going to be the variables.

3. Add the following as the variable definition, click on Preview to test, and Done to save the changes. 

```sql
fetch spans, from:now()-2m
| dedup dt.entity.host, dt.entity.process_group_instance, dt.smartscape.service

// extract primary grail fileds & tags defined
| fields dt.host_group.id, dt.security_context, dt.cost.costcenter, dt.cost.product,
         dt.entity.host, dt.entity.process_group_instance, dt.smartscape.service, span.id

// filter for classic entities
| fieldsAdd tags = concat("application:", dt.security_context)
| summarize count = count(), by:{dt.security_context, tags}
```

4. Save your Segment

![](../../assets/images/addvariablesave.png)

5. Filter `Data (all types)` with the Primary Grail Field. In our case, the `dt.security_context` value where we're extracting the app name. Then click on Preview.

![](../../assets/images/filteralldata.png)

See how all datapoints are getting enriched with the previously configured Primary Grail Field. And also notice how `dt.security_context` doesn't work for `Classic Entities`. This is meant to be like this, since it is a pure 3rd Gen configuration, and applies just to the "New" entities. And this is the reason why we created the below variable:

```sql
| fieldsAdd tags = concat("application:", dt.security_context)
```

![](../../assets/images/classicentities.png)

6. Save your segment in the top right

7. Click on More at the bottom of the page and click on Host

![](../../assets/images/morehost.png)

8. Filter by tags, use the "tag" variable value, and press Preview to see the results

![](../../assets/images/hostappear.png)

9. Click on related entity and click on Process Group

![](../../assets/images/relatedpg.png)

10. Do the same for Process & Service respectively

![](../../assets/images/sameforservice.png)

11. Click on Preview results for each of them to validate if it worked

![](../../assets/images/validate.png)

12. Save your Segment!

13. Go to the new Services app to validate the Segment is working. Apply the segment using the cube icon near the filter bar as shown below

![](../../assets/images/segmentnewserviceapp.png)

14. After applying the Segment, see how all our entities remain when filtering. We just accomplished one of the team's requirements about filtering across different screens!

15. Go to the Distributed Tracing app, and filter using the Segment to validate the same

![](../../assets/images/filtertracessegment.png)

### Close Up

Well done, you just replicated Management Zones functionality using Segments in the new platforn. Now users still achieve their exploration as they were doing it in classic, but unleash powerful new capabilities thanks to Grail and other 3rd Gen platform capabilities

As an example, you can now filter by any attribute of the spans (e.g. exception message) and pin it to a Dashboard or to a Notebook to have a ready-made DQL to use in workflow automation

![](../../assets/images/exceptionstodash.png)

![](../../assets/images/metricandalert2.png)

For those teams that are comfortable with using the 3rd Gen apps, you could "close" the access to the classic views, with boundaries at IAM level.

Let's suppose the Easytrade team is happy with the new platform, then you could configure their group at IAM level, using boundaries to exclude the classic distributed traces app as follows

![](../../assets/images/easytradegroup.png)

Check boundaries here

![](../../assets/images/boundariestoapps.png)

This is how you exclude an app

```sql
shared:app-id not in ("dynatrace.classic.distributed.traces");
```

![](../../assets/images/excludeapp.png)

Then the easytrade team will not be able to access the "classic" Distributed traces app, but the new & enhanced experience!

![](../../assets/images/notracesclassic.png)
