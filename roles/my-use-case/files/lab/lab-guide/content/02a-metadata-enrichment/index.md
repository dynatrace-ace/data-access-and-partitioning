## Metadata Enrichment - Labels & Annotations

We understood now the need of setting
- `dt.security_context`
- `dt.cost.costcenter`
- `dt.cost.product`

1. In your Dynatrace environment, open the **Notebooks app**, and specifically the provided `Enrichment Overview` notebook. We will be using the notebook to track the enrichment status within our environment.

![](../../assets/images/enrichment_initial.png)

If you are not new to Dynatrace, you may face this scenario - having a host group, but not the rest. 

2. Open K8s app, go to Namespaces, and check the existing labels & annotations for the **Easytrade** namespace.

<div align="center">
<img width="600" src="../../assets/images/labels_of_easytrade.png">
</div>

3. In **settings -> Cloud and virtualization -> Kubernetes telemetry enrichment** configure `dt.security_context` based on the `kubernetes.io/metadata.name` label

<div align="center">
<img width="600" src="../../assets/images/dt_sec_context.png">
</div>

4. Configure `dt.cost.costcenter` based on the `app.kubernetes.io/part-of` label

<div align="center">
<img width="600" src="../../assets/images/costcenter.png">
</div>

5. Configure `dt.cost.product` based on the `kubernetes.io/metadata.name` label

<div align="center">
<img width="600" src="../../assets/images/dtcostproduct.png">
</div>

6. This step is not necessary in a real-life scenario. The Dynatrace Operator queries the settings API once every 45 minutes. After creating or modifying rules, if you want to ensure immediate effects, you can restart it. Restart operator to grab config changes:

```bash
kubectl -n dynatrace rollout restart deployment dynatrace-operator
```

![](../../assets/images/enrichement45min.png)


7. Restart all deployments in the easytrade namespace:

```bash
for d in $(kubectl -n easytrade get deploy -o name); do
  kubectl -n easytrade rollout restart "$d"
done
```

8. Validate that the command worked after a few minutes and make sure the enrichment is there under the labels section (if it's not, please run the command above again).

```bash
kubectl describe pod -n easytrade -l app=accountservice
```

![](../../assets/images/enriched.png)

9. Check once again your **Enrichment** Notebook

![](../../assets/images/enrichment_final.png)

## Close Up & Next Challenge

Well Done, now we have enriched our Dynatrace Platform environment, based on how we want to slice and dice our data.

Now we will run into a new challenge.

Easytrade doesn’t follow k8s standards, and has multiple teams working within the same namespace. We need to provide data access, not at the app level (easytrade), but at the component level (e.g. BrokerService). We need lower granularity!

We will have to solve this by manual pod annotations in our next lab.

![](../../assets/images/enrichapproaches.png)

Good job! Now, back to the slides.
