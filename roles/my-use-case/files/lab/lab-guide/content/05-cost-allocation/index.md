## Cost Allocation

Now that we've implemented the right enrichment and data segmentation, let's make sure that all of that also reflects on our cost allocation to different departments.

Make sure that you:
- Verify that cost allocation attributes (`dt.cost.costcenter` and `dt.cost.product`) are correctly applied.
- Understand how Dynatrace uses these attributes for DPS tracking.
- Explore an out-of-the-box dashboard that visualizes cost allocation.

Remember that we've already completed the enrichment by setting cost attributes at the source in lab 02a. In that example we've used the following:
```bash
dt.cost.costcenter = ecommerce-apps
dt.cost.product = easytrade
```

**However, this is on namespace level and only for signals (logs/metrics/events etc) due to our monitoring mode which is CloudNativeFullStack.**

Dynatrace CloudNativeFullStack licensing is based on Host-level RAM, so we need to ensure that host properties are correctly set at the Host level in order for them to show up correctly on your chargeback report. These properties also align with the enrichment you completed earlier for cost allocation.

> Important: If you want a split on the namespace level, what you are looking for is Full-Stack Monitoring which combines [Kubernetes Platform Monitoring and Application-only monitoring](https://docs.dynatrace.com/docs/ingest-from/setup-on-k8s/deployment/application-observability). Licensing here is calculated based on pod-hours, plus the enrichment you’ve already applied in previous exercises.

What to do:
1. Run the following command that automatically applies these 3 fields to your Dynakube manifest.
```bash
CODE
```
2. Apply the updated manifest
```bash
kubectl apply -f dynakube.yaml
```
3. Go to Infrastructure and Operations App and check your Node

[SCREENSHOT OF THIS WORKING]

> Why this matters: These properties ensure accurate licensing calculation and cost attribution for CloudNativeFullStack monitoring, aligning technical usage with organizational governance.

**Task 1: Check Current Cost Allocation Attributes**

Goal: Confirm that the cost allocation attributes are recognized by Dynatrace by fetching different data types in a notebook.

Example query:
```bash
fetch logs
| filter dt.cost.costcenter == "ecommerce-apps"
```

[Screenshot Placeholder for a notebook querying logs]

> Fetch logs showing `dt.cost.costcenter` and `dt.cost.product` correctly applied.

***

**Task 2: Open the Out-of-the-Box Cost Allocation Dashboard**

Goal: Visualize how cost allocation attributes are applied to DPS usage.

Navigate to Dashboards → Cost Allocation Overview

[Screenshot Placeholder for the dashboard with a breakdown - WE NEED TO MAKE SURE TO UPLOAD THE DASHBOARD WITHIN PROVISIONING]

> Dashboard overview showing cost allocation breakdown by `dt.cost.costcenter` and `dt.cost.product`.

***

**Summary**

In this lab, you:
- Confirmed enrichment for cost attributes.
- Explored an OOTB dashboard for DPS cost tracking.


You’ve now completed the final step in building a scalable, governed observability strategy. By verifying cost allocation, you’ve ensured that every signal not only delivers insights but also drives financial transparency and accountability across teams.