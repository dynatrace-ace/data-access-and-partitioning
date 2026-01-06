## Data Partitioning

We have completed enrichment, data access, and segmentation. Now, let's focus on the query performance and costs. For that, we will implement a **Bucket Strategy**.


1. Go to the `Notebooks` application and open `Data Partitioning Helper`. Click **Run** on the `Spans Tb/day` & `Logs Tb/day` tiles and check the avg volume per day for both.

![](../../assets/images/logsspansvolume.png)

✅ Both ingest size are lower than 5Tb/day, meaning that 80 buckets will meet our requirements. Please have a look at the diagram below.

![](../../assets/images/lessthan5tbday.png)

2. We need to now calculate the `spans` traffic per application. Run the query in the tile labeled **1. Spans have a dt.ingest.size attribute** and notice how every single span has a `dt.ingest.size` attribute.

![](../../assets/images/dtingestsize.png)

3. We will use this attribute to create a metric in OpenPipeline with the `dt.security_context` as our dimension. Go to the **Settings -> Process and contextualize -> OpenPipeline -> Spans** as shown below:

![](../../assets/images/spansop.png)

4. Click on the `Pipelines` tab and then create a new one by clicking on **"+ Pipeline"**:

![](../../assets/images/newop.png)

5. Call it `General Pipeline` and click on `Metric Extraction` tab to create a metric extraction rule that grabs the `dt.ingest.size` field and has `dt.security_context` as a dimension. Click `Save`. Please see the screenshot below:

![](../../assets/images/opmetric.png)

6. Go to the Dynamic Routing and create a new one by clicking on **"+ Dynamic Route"**:

![](../../assets/images/dynamicroute.png)

7. Route all the traffic to the respective pipeline by following below screenshot and pressing `Add`

<div align="center">
<img width="400" src="../../assets/images/routetopipeline.png">
</div>

8. Go back to your Notebook and run the DQL of the `Spans Ingest a day per App` tile:

![](../../assets/images/overtimeperapp.png)

9. Run the `Avg/day Spans Ingest per App` tile

<div align="center">
<img width="600" src="../../assets/images/avgperapp.png">
</div>

### Data Retention & Performance Requirements

Let's suppose one of your company requirement is that all **spans** of **credit-card-order-service** must be retained for 12 months for auditing and compliance (PCI DSS). Let's add it to the table, please run this DQL:

11. Click on Show Input, uncomment the first 2 commented blocks as it is shown in the picture
query and run it again

![](../../assets/images/first2.png)

12. Uncomment the highlighted fields at the bottom of the DQL and run again

![](../../assets/images/uncommendandrun.png)

Now we should have a clear understanding on which apps need a separate bucket for data retention or performance reasons. For larger environments we could aggregate the numbers by a higher hierarchy, e.g. business unit. We will keep it simple for this exercise.

### Bucket Tracking & Naming

This DQL helps track and understand the reason of custom buckets, we will use columns to define the naming convention.

13. Uncomment the remaining blocks of the DQL, and run again

![](../../assets/images/remainingblocks.png)

14. Copy the bucket name, go to **Settings > Storage Management** and create a new bucket:

![](../../assets/images/newbucket.png)

15. Go to the Spans Openpipeline, and open the **"General Pipeline"** we've created before:

![](../../assets/images/backtoop.png)

16. Create a storage processor to ruote all spans with `dt.security_context == "credit-card-order-service"` to the recently created bucket"

![](../../assets/images/spanstobucket.png)

17. Let's validate traffic with our master **Notebook**:

![](../../assets/images/validatetraffic.png)

## Close Up

Well done! Now you have a separate bucket to meet Easytrade's requirements. 

You can apply the same steps for Logs. The Notebook provided will also guide you on how to do this same exercise for Logs. This is for you to take back and implement within your organization.
