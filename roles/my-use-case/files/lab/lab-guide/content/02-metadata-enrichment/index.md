## Metadata Enrichment

### Learning Objectives

- Learn the importance of Primary Grail Fields, in this case the host group. https://dt-rnd.atlassian.net/wiki/spaces/d1coe/pages/1246757730/2.+Metadata+Enrichment
- Host group may not be enough for the granularity that customer needs, so they will have to set OTEL_RESOURCE_ATTRIBUTE: https://dt-rnd.atlassian.net/wiki/spaces/d1coe/pages/1255932217/Enrichment+OneAgent
- Learn how to set all attributes 
    - `dt.security_context` → for Access Control (IAM)
    - `dt.cost.costcenter` & `dt.cost.product` → for Cost Allocation (DPS)
- `dt.security_context` == app (not to team) (i.e. `dt.security_context` = easytrade), then we map teams with apps within IAM
- `dt.cost.product` == app
- `dt.cost.costcenter` == ecommerce