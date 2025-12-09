## Intro & Warm Up (10min)

## Intro

Your orgnization has been running Dynatrace for years, and now a new application team "Easytrade" is getting onboarded, directly into the Dynatrace 3rd Generation Platform. You're responsible to execute the Proof-of-Concept. Their apps are running in K8s.

Your goal is to help implement the Dynatrace 3rd-Generation Platform end-to-end for the Easytrade team

You will complete a series of critical tasks:
- Metadata Enrichment
- Data Access
- Data Segmentation
- Data Partitioning
- Cost Allocation

## Warm Up

1. Open your dt environment, go to Segments

SCREENSHOT

Pro Tip: we will not create a Segment, but we will use Segments to understand where the metadata gets propagated.

2. Filter using span name SELECT TradeManagement

SCREENSHOT

See how the metadata is available just for spans, not quite a good fit for a tenant-wise configuration

3. Filter using k8s.namespace.name

SCREENSHOT

See how the metadata is available in all signals, a good fit for a tenant-wise configuration



