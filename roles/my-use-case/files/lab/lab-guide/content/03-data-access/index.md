## Data Access

#### The Easytrade scenario

Easytrade, a fast-growing fintech platform, has just expanded its operations across multiple regions and teams. With 13 microservices powering everything from login to trading, the platform is now managed by several specialized teams: infrastructure, observability, and application owners.

As the company scales, so does the complexity of managing access to observability data. The infrastructure team needs full control over configurations, while application teams only need read access to their own services. Meanwhile, everyone should be able to view SLOs and dashboards.

To avoid chaos and manual permission management, Easytrade decides to implement a scalable IAM strategy in Dynatrace — one that uses custom roles, policy boundaries, and group-based access control.

Your mission in this lab is to help Easytrade build this strategy from the ground up.


### 🎯 Objectives

- Understand how Dynatrace IAM works.
- Learn how to create and manage roles, policies, boundaries, and groups.
- Apply scoped access using dt.security_context and management-zone.
- Minimize maintenance effort by decoupling permissions from scopes.


#### Exercise 1: Create Default User Policies

Default users get access to Dynatrace apps and basic usage features, but no data access.


**Tasks**

1. Create Policy: Default users

<details>
  <summary>App access permissions – Apps Access</summary>

```sql
ALLOW app-engine:apps:run WHERE shared:app-id IN (
  "dynatrace.appshell",
  "dynatrace.launcher",
  "dynatrace.dashboards",
  "dynatrace.notebooks",
  "dynatrace.logs",
  "dynatrace.davis.problems",
  "dynatrace.classic.logs.events",
  "dynatrace.classic.dashboards",
  "dynatrace.classic.problems",
  "dynatrace.classic.data.explorer",
  "dynatrace.classic.metrics",
  "dynatrace.classic.smartscape",
  "dynatrace.infraops",
  "dynatrace.database.overview",
  "dynatrace.extensions.manager",
  "dynatrace.clouds",
  "dynatrace.kubernetes",
  "dynatrace.classic.hosts",
  "dynatrace.classic.network",
  "dynatrace.classic.technologies",
  "dynatrace.classic.aws",
  "dynatrace.classic.kubernetes",
  "dynatrace.classic.containers",
  "dynatrace.classic.extensions",
  "dynatrace.classic.vmware",
  "dynatrace.service.level.objectives",
  "dynatrace.classic.slo",
  "dynatrace.classic.releases",
  "dynatrace.distributedtracing",
  "dynatrace.services",
  "dynatrace.classic.distributed.traces",
  "dynatrace.classic.services",
  "dynatrace.classic.profiling",
  "dynatrace.classic.queues",
  "dynatrace.classic.mda",
  "dynatrace.classic.databases",
  "dynatrace.classic.kubernetes.workloads",
  "dynatrace.synthetic",
  "dynatrace.error.inspertor",
  "dynatrace.experience.vitals",
  "dynatrace.classic.query.user.sessions",
  "dynatrace.classic.synthetic",
  "dynatrace.classic.web",
  "dynatrace.classic.frontend",
  "dynatrace.classic.session.replay",
  "dynatrace.classic.session.segmentation",
  "dynatrace.classic.mobile",
  "dynatrace.classic.custom.applications",
  "dynatrace.hub",
  "dynatrace.segments.management",
  "dynatrace.settings",
  "dynatrace.classic.settings",
  "dynatrace.classic.user.settings",
  "dynatrace.classic.personal.access.tokens",
  "dynatrace.learndql"
);
```
</details>

2. Add to Policy: Default users

<details>
  <summary>Standard permissions – Basic Usage</summary>

```sql
ALLOW
  state:app-states:delete,
  state:app-states:read,
  state:app-states:write,
  state:user-app-states:read,
  state:user-app-states:write,
  state:user-app-states:delete,
  state-management:user-app-states:delete,
  state-management:user-app-states:delete-all,
  document:documents:read,
  document:documents:write,
  document:documents:delete,
  document:environment-shares:read,
  document:environment-shares:write,
  document:environment-shares:claim,
  document:environment-shares:delete,
  document:direct-shares:read,
  document:direct-shares:write,
  document:direct-shares:delete,
  document:trash.documents:read,
  document:trash.documents:restore,
  document:trash.documents:delete,
  unified-analysis:screen-definition:read,
  storage:bucket-definitions:read,
  storage:fieldset-definitions:read,
  storage:filter-segments:read,
  storage:filter-segments:write,
  storage:filter-segments:delete,
  hub:catalog:read,
  app-engine:functions:run,
  app-engine:edge-connects:read,
  davis:analyzers:read,
  davis:analyzers:execute,
  notification:self-notifications:read,
  geolocation:locations:lookup,
  slo:slos:read,
  slo:objective-templates:read;
```
</details>

3. Add to Policy: Default users 

<details>
  <summary>Workaround Infra&Ops apps issues – Default Metrics Access</summary>

```sql
ALLOW storage:metrics:read WHERE storage:metric.key IN (
  "dt.host.availability",
  "dt.host.uptime"
);
```
</details>

4. Add to Policy: Default users

<details>
  <summary>Network Devices in Infra&Ops App – Extensions Access</summary>

```sql
ALLOW extensions:definitions:read, extensions:configurations:read
WHERE extensions:extension-name IN (
  "com.dynatrace.extension.snmp-auto-discovery"
);
```
</details>

#### Exercise 2: Create Reader Role & Policy

Policy: Readers

<details>
  <summary>Read permissions – Basic Data</summary>

```sql
ALLOW
  storage:buckets:read,
  storage:entities:read,
  storage:smartscape:read,
  storage:metrics:read,
  storage:spans:read,
  storage:logs:read,
  environment:roles:logviewer,
  storage:events:read,
  storage:bizevents:read,
  storage:user.events:read,
  storage:user.sessions:read,
  environment:roles:viewer,
  app-settings:objects:read,
  settings:objects:read,
  settings:schemas:read,
  extensions:definitions:read,
  extensions:configurations:read;
```
</details>

#### Exercise 3: Create Writer Role & Policies

Policy 1: Writers

<details>
  <summary>Write permissions on settings – Settings</summary>

```sql
ALLOW settings:objects:write, environment:roles:manage-settings;
```
</details>

Policy 2: Writers

<details>
  <summary>Write permissions on extensions – Extensions</summary>

```sql
ALLOW settings:objects:write, environment:roles:manage-settings;
```
</details>

#### Exercise 4: Create Boundaries

Boundary 1

<details>
  <summary>dt.security_context = easytrade</summary>

```sql
storage:dt.security_context IN ("easytrade")
```
</details>

Boundary 2

<details>
  <summary>management-zone = easytrade</summary>

```sql
environment:management-zone IN ("easytrade")
```
</details>

#### Exercise 5: Create Groups & Assign Policies

Groups to create:

- Default Users → assign all default policies (no boundary)
- Easytrade Readers → assign Readers – Basic Data + easytrade boundary
- Easytrade Writers → assign both Writers policies + easytrade boundary


#### Exercise 6: Assign Users to Groups

Group Membership Strategy

- Writers → must be in:
    - Default Users
    - Easytrade Readers
    - Easytrade Writers
- Readers → must be in:
    - Default Users
    - Easytrade Readers


 OLD INSTRUCTIONS
### Learning Objectives

- Configure IAM by following this guide: https://dt-rnd.atlassian.net/wiki/spaces/d1coe/pages/1356339039/4.+Data+Access
- Create 4 different personas: Default, Readers, Writers
- Use what we configured previously (dt.security_context=easytrade)