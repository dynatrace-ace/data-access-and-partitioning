## Metadata Enrichment

### Objectives

1. Participants need to enrich with dt.security_context, cost center, cost product, following this guide: (Dedicated Infrastructure enrichment): https://dt-rnd.atlassian.net/wiki/spaces/d1coe/pages/1255932217/Enrichment+OneAgent. 

sudo /opt/dynatrace/oneagent/agent/tools/oneagentctl --set-monitoring-mode=fullstack --set-app-log-content-access=true --set-host-group=onPrem_easytrade_staging --set-host-property=dt.security_context=easytrade --set-host-property=dt.cost.costcenter=easytrade --set-host-property=dt.cost.product=easytrade --set-host-property=team=alpha --set-host-property=app=easytrade --set-host-property=stage=staging

2. Learn the importance of Primary Grail Fields, in this case the host group. https://dt-rnd.atlassian.net/wiki/spaces/d1coe/pages/1246757730/2.+Metadata+Enrichment