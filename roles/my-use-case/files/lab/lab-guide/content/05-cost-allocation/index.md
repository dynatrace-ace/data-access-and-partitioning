## Cost Allocation

Now that we've implemented the right enrichment and data segmentation, let's make sure that all of that also reflects on our cost allocation to different departments.

Make sure that you:
- Verify that cost allocation attributes (dt.cost.costcenter and dt.cost.product) are correctly applied.
- Understand how Dynatrace uses these attributes for DPS tracking.
- Explore an out-of-the-box dashboard that visualizes cost allocation.

Remember that we've already completed the enrichment by setting cost attributes at the source in lab 02a. In that example we've used the following:
```bash
dt.cost.costcenter = ecommerce-apps
dt.cost.product = easytrade
```

**Step 1: Check Current Cost Allocation Attributes**
Goal: Confirm that the cost allocation attributes are recognized by Dynatrace by fetching different data types in a notebook.

Example query:
```bash
fetch logs
| filter dt.cost.costcenter == "ecommerce-apps"
```

[Screenshot Placeholder for a notebook querying logs]

> Cost Allocation Allowlist page showing dt.cost.costcenter and dt.cost.product.

***

**Step 2: Open the Out-of-the-Box Cost Allocation Dashboard**
Goal: Visualize how cost allocation attributes are applied to DPS usage.

Navigate to Dashboards → Cost Allocation Overview

[Screenshot Placeholder for the dashboard with a breakdown - WE NEED TO MAKE SURE TO UPLOAD THE DASHBOARD WITHIN PROVISIONING]

> Dashboard overview showing cost allocation breakdown by cost center and product.

***

Summary
In this lab, you:
- Confirmed metadata enrichment for cost attributes.
- Explored an OOTB dashboard for DPS cost tracking.


You’ve now completed the final step in building a scalable, governed observability strategy. By verifying cost allocation, you’ve ensured that every signal not only delivers insights but also drives financial transparency and accountability across teams.