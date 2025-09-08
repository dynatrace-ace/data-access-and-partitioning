## Metadata Enrichment

### 🎯 Objectives
All participants will enrich observability data (entities, metrics, events, logs, etc.) with metadata fields such as:
- `dt.security_context`
- `dt.cost.costcenter`
- `dt.cost.product`
> The idea is to explore different enrichment strategies using Kubernetes and understand trade offs between approaches.

#### 📋 Step 1: Understand Why Metadata Enrichment Matters
💡 Enrichment helps with access control, cost allocation, segmentation, and governance. We are trying to make sure that observability data is tagged with meaningful context.

Key Enrichment Targets:
- Entities (e.g., services, workloads)
- Metrics
- Events
- Logs
- Traces

  
🧠 Questions to consider:
- What metadata do you need to enrich your data with?
- What level of granularity is required—namespace or workload?
- Do you want enrichment to be automatic, declarative, or manual?
- How will this metadata be used for IAM, cost control, and segmentation?


#### 🛠️ Step 2: Explore Enrichment Strategies
🧪 Use the guide: [Enrichment Kubernetes](https://dt-rnd.atlassian.net/wiki/spaces/d1coe/pages/1229849653/Enrichment+Kubernetes)

✅ Option 1: Rely on Primary Grail Fields
Fields:
- `k8s.namespace.name`
- `k8s.cluster.name`
  
Pros:
- Out-of-the-box (OOTB)
- No configuration needed

Cons:
- Limited granularity
- Only namespace-level
  
Use When:
- Quick setup is needed
- Simple IAM and segmentation

🟡 Option 2: Use [Namespace Annotations & Labels](https://docs.dynatrace.com/docs/ingest-from/setup-on-k8s/guides/metadata-automation/k8s-metadata-telemetry-enrichment)

How it works? Dynatrace Operator converts namespace-level metadata into enrichment fields.

Pros:
- Declarative
- Moderate effort
- Supports custom Primary Grail Tags
  
Cons:
- Only applies at namespace level
- Requires Dynatrace configuration
  
Use When:
- Customer follows cloud-native tagging practices
- Needs more flexibility than OOTB fields


🔴 Option 3: Set Manual Pod Annotations

How it works? Manually add annotations to pod definitions (e.g., in deployment YAML)

Pros:
- Maximum granularity (workload-level)
- Full control over enrichment
  
Cons:
- Requires code changes
- Higher effort
  
Use When:
- Need to segregate access or cost at workload level
- Namespace-level granularity is not enough


🧾 Summary Table
| Approach	| Effort	|Granularity |	Flexibility |	Best For |
| ------ | ------ | ------ | ------ | ------|
| Primary Grail Fields|	🟢 Low | Namespace	| 🔴 Limited | 	Quick IAM & Segments setup |
| Namespace Annotations/Labels |	🟡 Medium |	Namespace	| 🟡 Moderate	| Declarative tagging, cloud-native orgs |
| Manual Pod Annotations	| 🔴 High	| Workload | 🟢 Maximum	| Fine-grained control, cost partitioning|


#### 🧩 Step 3: Try It Out

Complete enrichment using one or more strategies.

Tasks:
Choose one enrichment strategy. General approach should be **Option 2**. Apply it to a sample namespace or pod.
Enrich with:
- `dt.security_context`
- `dt.cost.costcenter`
- `dt.cost.product`
  
🧾 Example
- **Namespace**:easytrade
- **Pod**:accountservice

Enrichment via Pod Annotation:
```
metadata:
  annotations:
    dt.security_context: "easytrade"
    dt.cost.costcenter: "easytrade"
    dt.cost.product: "easytrade"

```

Apply with:
```
kubectl apply -f accountservice.yaml -n easytrade
```

> NEED TO ADD SCREENSHOTS AND UI STEPS THAT PARTICIPANTS WILL NEED TO COMPLETE TO HAVE THESE ATTRIBUTES PROPAGATED PROPERLY




OLD STRUCTURE - keeping it for now
### Objectives

1. Participants need to enrich with dt.security_context, cost center, cost product, following this guide: (Dedicated Infrastructure enrichment): https://dt-rnd.atlassian.net/wiki/spaces/d1coe/pages/1229849653/Enrichment+Kubernetes

2. Learn the importance of Primary Grail Fields, in this case the host group. https://dt-rnd.atlassian.net/wiki/spaces/d1coe/pages/1246757730/2.+Metadata+Enrichment
    - difference between host group with java.jar.file

3. Talk about bare-metal, OTEL_RESOURCE_ATTRIBUTE
