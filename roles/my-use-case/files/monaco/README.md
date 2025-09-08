# Monaco (Dynatrace Monitoring as Code) — monaco/ folder

This folder contains Monaco templates and configuration used to provision Dynatrace resources (buckets, pipelines, etc.) for the lab. It is scoped to the `roles/my-use-case/files/monaco` directory and intended to be applied to a Dynatrace tenant with the Monaco tooling.

## Layout
- main/
  - <resource-type>/
    - <resource-name>.json        → Monaco template (resource definition)
    - config.yaml                 → List of configs referencing templates (ids + parameters)
  - ...other resource folders...

Example: `main/bucket/` contains `bucket.json` and the `config.yaml` referenced in this repo.

## config.yaml (what to edit)
Each entry in `config.yaml` describes one resource instance to create. Key fields:
- id: unique identifier for the config
- type: resource type (e.g., `bucket`)
- template: filename of the JSON template to use
- config.parameters: template parameters to substitute (e.g., displayName, retentionDays, table)
- skip: set to `true` to ignore this config during deployment

Example (existing file):
```yaml
configs:
- id: test_bucket_monaco
  config:
    parameters:
      displayName: test_bucket_monaco
      retentionDays: 365
      table: spans
    template: bucket.json
    skip: false
  type: bucket
```

To add another bucket, copy the block, give a new id, adjust `parameters` and `template` as needed.

## Deploying with Monaco CLI
Prerequisites:
- Monaco CLI installed (see Dynatrace Monaco [documentation](https://docs.dynatrace.com/docs/deliver/configuration-as-code/monaco) for installation)
- A Dynatrace API token with configuration write permissions
- Tenant URL

Typical deploy command (replace placeholders):
monaco deploy --path ./roles/my-use-case/files/monaco --tenant https://{your-tenant} --token {YOUR_API_TOKEN}

Notes:
- You can deploy only a subfolder with `--path` or run from inside the monaco folder.
- Use `skip: true` in a config to temporarily disable a resource.
- Validate templates locally before deploying by running Monaco in dry-run/preview mode if supported by your installed version.

## Tips
- Keep parameter values in `config.yaml` small and obvious for labs (names, retentionDays).
- Use consistent `id` naming to avoid accidental duplicate deployments.
- When testing, set retention and resource names to avoid colliding with production tenants.

For full reference and CLI flags, consult the official Dynatrace Monaco documentation for your installed