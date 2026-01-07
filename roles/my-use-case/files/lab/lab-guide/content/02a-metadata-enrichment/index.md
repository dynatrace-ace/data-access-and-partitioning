## Metadata Enrichment - Labels & Annotations

We now understand the need for setting the following:
- `dt.security_context`
- `dt.cost.costcenter`
- `dt.cost.product`

1. In your Dynatrace environment, open the **Notebooks app** and click on the provided Notebook `Enrichment Overview`. We will be using this notebook to track the enrichment status within our environment.

![](../../assets/images/enrichment_initial.png)

Existing customers may face the following scenario: having a host group id, but not `dt.security_context`, `dt.cost.costcenter`, or `dt.cost.product`. 

2. Open the Kubernetes app, go to Namespaces, click on the Metadata tab, and review the existing labels for the **easytrade** namespace by clicking on the number.

<div align="center">
<img width="600" src="../../assets/images/labels_of_easytrade.png">
</div>

3. In **Settings -> Cloud and virtualization -> Kubernetes metadata/telemetry enrichment** configure `dt.security_context` based on the `kubernetes.io/metadata.name` label by clicking Add rule

<div align="center">
<img width="600" src="../../assets/images/dt_sec_context.png">
</div>

4. Click Add rule and configure `dt.cost.costcenter` based on the `app.kubernetes.io/part-of` label

<div align="center">
<img width="600" src="../../assets/images/costcenter.png">
</div>

5. Click Add rule and configure `dt.cost.product` based on the `kubernetes.io/metadata.name` label

<div align="center">
<img width="600" src="../../assets/images/dtcostproduct.png">
</div>

6. Click **Save changes**

7. The following step is not necessary in a real-life scenario. The Dynatrace Operator queries the settings API once every 45 minutes, so instead of waiting, we're going to uninstall and install the operator with this script:

```bash
export ACE_ACTION=redeploy && ace enable https://github.com/dynatrace-ace/data-access-and-partitioning.git@perform_3rdgen_part_1 --local
```

![](../../assets/images/enrichement45min.png)

8. You can check the Enrichment rules in the dynakube with the following command

```bash
kubectl get dynakube dynakube -n dynatrace   -o jsonpath='{.status.metadataEnrichment}'
```

9. Restart all deployments in the easytrade namespace:

```bash
for d in $(kubectl -n easytrade get deploy -o name); do
  kubectl -n easytrade rollout restart "$d"
done
```

10. Validate that the command worked after a few minutes and make sure the enrichment is there under the labels section we checked in the Kubernetes App (if it's not, please run the command above again).

```bash
kubectl describe pod -n easytrade -l app=accountservice
```

![](../../assets/images/enriched.png)

11. Review your **Enrichment** Notebook with the updated values by pressing "Run" on the percentage table under the Spans section.

![](../../assets/images/enrichment_final.png)

## Close Up & Next Challenge

Well Done! We have now enriched our Dynatrace Platform environment based on how we want to slice and dice our data.

Now, we will run into a new challenge:,
Easytrade doesn’t follow kubernetes standards and has multiple teams working within the same namespace. We need to provide data access; not at the application level (easytrade), but at the component level (e.g. BrokerService). We need lower granularity!

We will solve this by performing pod annotations in our next lab.

![](../../assets/images/enrichapproaches.png)

Good job! Now, back to the slides.
