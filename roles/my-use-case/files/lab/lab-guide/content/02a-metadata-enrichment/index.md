## Metadata Enrichment - Labels & Annotations

We understood now the need of setting
- dt.security_context
- dt.cost.costcenter
- dt.cost.product

1. In your Dynatrace environment, open the Notebooks app, and especifically the provided Enrichment Overview notebook. We will be using the notebook to track the enrichment status within our environment.

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

6. This step in a real-life scenario is not needed. The Dynatrace Operator queries the settings API once every 45 mins. After creating or modifying rules, if you want to ensure inmediate effects, you can restart the it with. Restart operator to grab config changes

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

kubectl describe pod -n easytrade -l app=accountservice
