## Metadata Enrichment - Manual Pod Annotations

### New Challenge

Easytrade doesn’t follow k8s standards, and has multiple teams working within the same namespace. We need to provide data access, not at the app level (easytrade), but at the component level (e.g. BrokerService). We need a finer level of granularity!

### Exercises

1. Modify pod definition for BrokerService, adding its own `dt.security context`, `dt.cost.costcenter` & `dt.cost.product`.

![](../../assets/images/addanotationsbroker.png)

2. The screenshot shows you how this would look like in an IDE. However, since you don't have access to one, we have prepared a one stop shop for you. Just run the command below and you'll see the results shown in the screenshot.

```bash
kubectl apply -k "/home/$USER/repos/data-access-and-partitioning/roles/app-easytrade/files/kustomize/base" -n easytrade
```

2. Validate that the command worked after a few minutes and make sure the enrichment is there under the labels section (if it's not, please run the command above again).

```bash
kubectl describe pod -n easytrade -l app=broker-service
```

3. Run command to re-deploy all pods with the custom values (not just the BrokerService).

```bash
kubectl apply -k "/home/$USER/repos/data-access-and-partitioning/roles/app-easytrade/files/kustomize/overlays/with-annotations" -n easytrade
```

4. Validate that the command worked after a few minutes and make sure the enrichment is there under the labels section of another workload (if it's not, please run the command above again).

```bash
kubectl describe pod -n easytrade -l app=frontend
```

![](../../assets/images/frontend.png)

5. Check the **Enrichment** Notebook one more time

![](../../assets/images/workloadgranularity.png)

Well done, you were successful at achieving a finer level of granularity.

Discuss with your class how to enrich a regular OA deployment as well as a Cloud one!

That was easy. What's next? Back to slides.

