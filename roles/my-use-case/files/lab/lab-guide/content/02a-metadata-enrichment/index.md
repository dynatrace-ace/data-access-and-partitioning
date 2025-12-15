## Metadata Enrichment - Labels & Annotations

We understood now the need of setting
- dt.security_context
- dt.cost.costcenter
- dt.cost.product

1. In your Dynatrace environment, open the Notebooks app, and specifically the provided Enrichment Overview notebook. We will be using the notebook to track the enrichment status within our environment.

![](../../assets/images/enrichment_initial.png)

If you are not a new to Dynatrace, you may face this scenario. Having a host group, but not the rest. 

2. Open K8s app, go to Namespaces, and check the existing labels & annotations for the easytrade namespace.

![](../../assets/images/labels_of_easytrade.png)

3. In settings -> Cloud and virtualization -> Kubernetes telemetry enrichment configure dt.security_context based on the kubernetes.io/metadata.name label

![](../../assets/images/dt_sec_context.png)

4. Configure dt.cost.costcenter based on the app.kubernetes.io/part-of label

![](../../assets/images/costcenter.png)

5. Configure dt.cost.product based on the kubernetes.io/metadata.name label

![](../../assets/images/dtcostproduct.png)

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

8. Check the pod labels for accountservice

```bash
kubectl describe pod -n easytrade -l app=accountservice
```

![](../../assets/images/enriched.png)

9. Check once again your Enrichment Notebook

![](../../assets/images/enrichment_final.png)

## Close Up & Next Challenge

Well Done, now we have enriched our 3rd Gen environment, based on how we want ot slice and dice our data.

Now we will run into a New challenge.

Easytrade doesn’t follow k8s standards, and has multiple teams working within the same namespace.

We need to provide data access, not at the app level (easytrade), but at the component level (e.g. BrokerService)

We need a lower granularity

We will have to solve this by manual pod annotations.

![](../../assets/images/enrichapproaches.png)

Good job!, back to the slides
