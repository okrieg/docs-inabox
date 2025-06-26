Here is an example YAML file for creating a `clusterorder` using `fulfillment-cli`, based on the internal API structure and field names used in the repo:

```yaml
apiVersion: fulfillment.innabox.io/v1
kind: ClusterOrder
metadata:
  name: my-test-cluster
  labels:
    environment: dev
spec:
  tenantID: tenant-1234
  clusterTemplateID: template-abc
  regionID: region-us-east-1
  parameters:
    nodeCount: 3
    machineType: m5.large
    storageSizeGB: 100
    version: "4.14.1"
  expiration:
    duration: 48h
  addons:
    - id: logging
    - id: monitoring
```

### 🔍 Field Breakdown

| Field                      | Description                                                  |
| -------------------------- | ------------------------------------------------------------ |
| `apiVersion`               | API version identifier (usually `fulfillment.innabox.io/v1`) |
| `kind`                     | Resource type (must be `ClusterOrder`)                       |
| `metadata.name`            | Name of the order                                            |
| `metadata.labels`          | Optional key-value tags                                      |
| `spec.tenantID`            | Tenant the cluster will belong to                            |
| `spec.clusterTemplateID`   | ID of the cluster template to use                            |
| `spec.regionID`            | Cloud region or datacenter ID                                |
| `spec.parameters`          | Template-specific customization like nodes and storage       |
| `spec.expiration.duration` | Time until auto-expiration                                   |
| `spec.addons`              | Optional list of addon service IDs                           |

> 🔧 Template and region IDs can be retrieved using:

```bash
fulfillment-cli get templates
fulfillment-cli get regions
```

Let me know if you’d like me to include alternative examples (e.g., with GPU nodes, special networking, or no expiration), or generate this dynamically from a live template.
