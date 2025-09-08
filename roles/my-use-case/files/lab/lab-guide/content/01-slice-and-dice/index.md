## Slice & Dice

### Objectives

- Participants will be working with an existing customer (easytrade).
- Participants will Learn how to extract:
    - 📋 Requirements
    - 📐 Dimensions
    - 🖥️ Technologies

### 📋 Requirements
- Make it interactive, we are the customer in 2nd-Gen. Make them use this guide: https://dt-rnd.atlassian.net/wiki/spaces/d1coe/pages/1247150978/1.+Slice+Dice
- We will give them the requirements
    - Data Access
        - easytrade people have to access easytrade stuff
    - Partitioning
        - easytrade has very low volume of logs & spans, no need for a bucket strategy
    - Segmentation
        - Customer wants a global easytrade filter so they can see easytrade entities, problems, synthetics & SLOs
    - Cost Control
        - easytrade people want to see easytrade dynatrace costs

### Discover 📐 Dimensions
1. Copy the notebook: https://guu84124.apps.dynatrace.com/ui/document/v0/#share=06f00290-72b6-4a03-930d-5a7bf17de35e
2. Find out dimensions (dimensions are what customers use as metadata for their entities) from:
    - Host Groups List ("onPrem_easytrade_staging", dimensions will be platform: onPrem, bu:easytrade, environment:staging)
    - Tags rules, they will also find the "app" dimension

Output of the exercise
- platform
- bu
- enviroment
- app

### 🖥️ Technologies

Find out underlying technologies -> not K8s, but standard VM running in GCP with app deployed as processes

    
### Map requirements with dimensions

| Requirement    | Dimension |
| -------- | ------- |
| Data Access  | dt.security_context = easytrade    |
| Partitioning  | -    |
| Segmentation  | segment for easytrade    |
| Cost Allocation  | dt.cost.costcenter = easytrade and dt.cost.product = easytrade    |

