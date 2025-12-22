# Data Access & Partitioning

## Provisioning scopes

Api Token
- read api token
- write api token

## OAuth Client

storage:buckets:read, storage:bucket-definitions:read, storage:bucket-definitions:write, openpipeline:configurations:read, openpipeline:configurations:write, app-settings:objects:read, settings:objects:read, settings:objects:write, settings:schemas:read, settings:objects:admin, app-engine:apps:run, document:documents:write, document:documents:read

## To see DPS/Cost Allocation

ALLOW storage:buckets:read WHERE storage:table-name = "dt.system.events";
ALLOW storage:system:read;
