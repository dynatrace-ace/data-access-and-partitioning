## Slice & Dice

### Objectives

- Work with an existing customer scenario (we play the role of the customer).
- Learn how to extract and map:
    - 📋 Requirements
    - 📐 Dimensions
    - 🖥️ Technologies

### Step 1: Understand the 📋 Requirements (Interactive Discovery) 
You are interviewing the customer currently working on 2nd gen (played by us). Use the questions below to uncover their needs. Write down your findings, you will need it later. Feel free to spend a few minutes and read through the best practice guide available [here](https://dt-rnd.atlassian.net/wiki/spaces/d1coe/pages/1247150978/1.+Slice+Dice).

#### 🔐 Access Control
Goal: Understand who should access what data. Think about all questions that you need to ask your customer to uncover this. For example:
- Who should be able to access which data sets?
- Are there any restrictions based on data sensitivity or compliance?
- Do different teams need isolated views of their own applications?
- Do you need to go more granular than just the application view?

#### 🧱 Partitioning (Bucket Strategy)
Goal: Identify how logs and spans should be stored and separated.
- Can you think of reasons why logs might need to be stored in separate buckets?
- What about log retention: should all logs be kept for the same duration? Usually that's not the case.
- Based on log volume, would query performance be affected?
- Could separating logs into their respective application buckets help with cost control? Do you think this is best practice?

#### 🎯 Segmentation
Goal: Determine how data should be filtered and grouped for visibility.
- What would be the best way to split your customer's data for visibility?
- Would you like to filter by app, environment, region, or business unit? What do you think is the best approach?
- How would this affect your data access?
> Think about the move from Management Zones to IAM + Segments. What can people have access to vs what can they only filter on?
#### 💰 Cost Allocation
Goal: Understand how observability costs should be tracked and distributed.
- How would your customer like to allocate costs?
- Should costs be split by application, team, or department?
- Do you need a chargeback or showback model for budgeting?

#### ✅ Provided Requirements (Simulated customer answers in this use case)
Use these to validate your findings:

- Data Access → Teams should access only their own apps, those apps being easytrade and hipstershop. This includes ALL DATA.
- Partitioning → Both easytrade and hipstershop logs need a separate bucket. Think about routing rules for logs and their respective buckets considering that everything is deployed in a kubernetes environment.
- Segmentation → Global app filter needed for unified visibility for both easytrade and hipstershop.
- Cost Control → Costs split by apps.

### Discover 📐 Dimensions
> 💡 Dimensions = metadata used to tag and organize observability data.

Instructions:
1. Copy the notebook: https://guu84124.apps.dynatrace.com/ui/document/v0/#share=06f00290-72b6-4a03-930d-5a7bf17de35e
2. Explore metadata sources:
    - Host Groups
    - MZ rules
    - Tag Rules
      Look for tags that reveal dimensions like platform, app, stage, team, etc.

Write down the dimensions you discover:

- ______________________
- ______________________
- ______________________


### 🖥️ Technologies

Find out underlying technologies -> not K8s, but standard VM running in GCP with app deployed as processes
> 💡 Understand the infrastructure to enrich observability data.

🔍 Questions to Ask
- What cloud providers are used? (e.g., AWS, GCP, on-prem)
- Is Kubernetes or serverless in use?
- What tagging strategies exist across environments?
- What Dynatrace metadata can be leveraged? (e.g., HOST_GROUPS)

    
### Map requirements with dimensions

| Requirement    | Dimension |
| -------- | ------- |
| Data Access  | dt.security_context = easytrade  (same for hipstershop)  |
| Partitioning  | k8s.namespace.name    |
| Segmentation  | segment for easytrade and hipstershop  |
| Cost Allocation  | dt.cost.costcenter = easytrade and dt.cost.product = easytrade (same for hipstershop)   |

