## Metadata Enrichment - Manual Pod Annotations

### New Challenge

Easytrade doesn’t follow k8s standards, and have multiple teams working within the same namespace
We need to provide data access, not at app level (easytrade), but at component level (e.g. BrokerService)

We need a higher level of granularity

### Exercises

1. Modify pod definition for BrokerService, adding it owns dt.security context, cost cvwente & product

SCREENSHOT

2. Validate it has it owns, in pod and in Dynatrace

SCREENSHOT

3. Run command to redeploy all pods with the custom values

SCREENSHOT