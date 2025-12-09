## Metadata Enrichment - Labels & Annotations

We understood now the need of setting
- dt.security_context
- dt.cost.costcenter
- dt.cost.product

1. Open the Notebooks App, and especifically the provided Enrichment Overview notebook. We will be using the notebook to track the enrichment status within our environment.

![](../../assets/images/enrichment_initial.png)

If you are not a new to Dynatrace, you may face this scenario. Having host group, but not the rest. 

2. Open K8s app, go to Namespaces, and check the existing labels & annotations for easytrade

![](../../assets/images/labels_of_easytrade.png)

3. Configure dt.security_context based on the kubernetes.io/metadata.name label

![](../../assets/images/dt_sec_context.png)

4. Configure dt.cost.costcenter based on the app.kubernetes.io/part-of label

![](../../assets/images/costcenter.png)

5. Configure dt.cost.product based on the kubernetes.io/metadata.name label

![](../../assets/images/dtcostproduct.png)


The Dynatrace
This step in a real-life scenario is not needed. 

Restart operator to grab config changes

```bash
kubectl -n dynatrace rollout restart deployment dynatrace-operator
```

6. Check enriched signal in Dynatrace

SCREENSHOT