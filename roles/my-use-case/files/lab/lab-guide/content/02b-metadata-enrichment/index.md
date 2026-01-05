## Metadata Enrichment - Manual Pod Annotations

### New Challenge

Easytrade application doesn’t follow Kubernetes standards and has multiple teams working within the same namespace. We need to provide data access, not at the application level (easytrade), but at the component level (e.g. BrokerService). We need a finer level of granularity!

### Exercises

1. Modify pod definition for BrokerService, adding its own `dt.security context`, `dt.cost.costcenter` & `dt.cost.product`.

![](../../assets/images/addanotationsbroker.png)

2. The screenshot shows you how this would look like in an IDE. However, since you don't have access to one, we have prepared a one stop shop for you. Run the next two commands below and after the validation command you'll see similar results to what is shown in the above screenshot.

```bash
kubectl apply -k "/home/$USER/repos/data-access-and-partitioning/roles/app-easytrade/files/kustomize/base" -n easytrade
```

2. Validate that the command worked after a few minutes and make sure the enrichment is there under the `Annotations` section (if it's not, please run the command above again).

```bash
kubectl describe pod -n easytrade -l app=broker-service
```

3. Now run the command to re-deploy all pods with the new custom values (not just the BrokerService).

```bash
kubectl apply -k "/home/$USER/repos/data-access-and-partitioning/roles/app-easytrade/files/kustomize/overlays/with-annotations" -n easytrade
```

4. Validate that the command worked after a few minutes and make sure the enrichment is there under the labels section of another workload such as `frontend` (if it's not, please run the command above again).

```bash
kubectl describe pod -n easytrade -l app=frontend
```

![](../../assets/images/frontend.png)

5. Review the **Enrichment** Notebook and click "Run" under the section labeled `All values for dt.security_context`

![](../../assets/images/workloadgranularity.png)

Well done! You were successful in achieving a finer level of granularity.

Discuss with your class how to enrich a regular OneAgent deployment as well as a Cloud one!

That was easy. What's next? Back to the slides.

