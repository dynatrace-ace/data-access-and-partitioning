## Slice & Dice

### Objectives

- Participants will be working with an existing customer.
- Participants will Learn how to extract:
    - 📋 Requirements
    - 📐 Dimensions
    - 🖥️ Technologies

### 📋 Requirements
- Make it interactive, we are the customer in 2nd-Gen. Make them use this guide: https://dt-rnd.atlassian.net/wiki/spaces/d1coe/pages/1247150978/1.+Slice+Dice
- We will give them the requirements
    - Data Access
        - teams should have access to their own aps
    - Partitioning
        - easytravel logs are high volume, need a separate bucket, keep the default for the rest
    - Segmentation
        - Customer wants a global apps filter so they can see entities, problems, synthetics & SLOs
    - Cost Control
        - costs allocation splitted by apps

### Discover 📐 Dimensions
1. Copy the notebook: https://guu84124.apps.dynatrace.com/ui/document/v0/#share=06f00290-72b6-4a03-930d-5a7bf17de35e
2. Find out dimensions (dimensions are what customers use as metadata for their entities) from:
    - Host Groups List ("k8s_multi_prod", dimensions will be platform: k8s, app:multi, environment:prod)
    - Tags rules, they will also find the "app" dimension

Output of the exercise
- platform
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

