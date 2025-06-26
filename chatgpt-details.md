Here is detailed Markdown documentation for the `fulfillment-cli`, including **all known commands** and **options** extracted from the source code and documentation.

---

# `fulfillment-cli` – Full Command Reference

> A command-line tool for interacting with the Innabox Fulfillment system.

---

## 🔑 Authentication

### `login`

Authenticate the CLI session using your credentials.

```bash
fulfillment-cli login
```

This will launch an OAuth flow and store credentials in the config file.

#### Options:

* `--auth-server`: URL of the authentication server.
* `--client-id`: OAuth client ID.
* `--issuer`: Token issuer.
* `--redirect-uri`: Callback URL for the login flow.

---

### `logout`

Clear session credentials.

```bash
fulfillment-cli logout
```

---

## 📦 Cluster Order Commands

### `create clusterorder`

Create a new cluster order from a YAML/JSON file.

```bash
fulfillment-cli create clusterorder --file order.yaml
```

#### Options:

* `--file`, `-f`: Path to the order specification YAML or JSON.
* `--name`, `-n`: Optional human-readable name for the order.

---

### `describe clusterorder`

Describe a specific cluster order.

```bash
fulfillment-cli describe clusterorder --id <order-id>
```

#### Options:

* `--id`: ID of the cluster order (required).

---

## 🔐 Credentials

### `get kubeconfig`

Retrieve a kubeconfig file for a given cluster.

```bash
fulfillment-cli get kubeconfig --cluster-id <id> > kubeconfig.yaml
```

#### Options:

* `--cluster-id`: ID of the target cluster (required).

---

### `get password`

Retrieve the admin password for a cluster.

```bash
fulfillment-cli get password --cluster-id <id>
```

#### Options:

* `--cluster-id`: ID of the target cluster (required).

---

## 📋 General Resource Management

### `get`

List resources of a given type.

```bash
fulfillment-cli get <resource> [--flags]
```

Supported resources:

* `clusterorders`
* `clusters`
* `templates`
* `regions`
* `orders`
* `tenants`

#### Common Options:

* `--output`, `-o`: Output format (`json`, `yaml`, `table`)
* `--filter`: Key=value filters (e.g. `status=ready`)

---

### `edit`

Edit a resource using your local editor.

```bash
fulfillment-cli edit <resource> --id <resource-id>
```

#### Options:

* `--id`: ID of the resource to edit.
* `--editor`: (optional) Override the default editor (e.g., `vim`, `nano`).

---

### `delete`

Delete a resource.

```bash
fulfillment-cli delete <resource> --id <resource-id>
```

#### Options:

* `--id`: ID of the resource to delete.
* `--force`: Skip confirmation prompt.

---

## ⚙️ Global Flags

The following options apply to all commands:

| Flag         | Description                                          |
| ------------ | ---------------------------------------------------- |
| `--verbose`  | Enable verbose logging                               |
| `--config`   | Path to config file (default: `~/.fulfillment.yaml`) |
| `--token`    | Override the stored auth token                       |
| `--insecure` | Allow insecure server connections (skip TLS)         |

---

## 🧪 Example Workflows

### Full Cluster Lifecycle

1. **Login**

   ```bash
   fulfillment-cli login
   ```

2. **Create Cluster Order**

   ```bash
   fulfillment-cli create clusterorder --file order.yaml
   ```

3. **Check Status**

   ```bash
   fulfillment-cli get clusterorders
   ```

4. **Get Credentials**

   ```bash
   fulfillment-cli get kubeconfig --cluster-id 123 > kubeconfig.yaml
   fulfillment-cli get password --cluster-id 123
   ```

5. **Logout**

   ```bash
   fulfillment-cli logout
   ```

---

## 📁 Configuration File

Default location: `~/.fulfillment.yaml`

Fields:

* `api_url`: API base URL
* `token`: Auth token
* `tenant_id`: Default tenant
* `cluster_id`: Default cluster (optional)

---

Let me know if you'd like this exported as a GitHub-ready `README.md`, or if you want autocomplete setup instructions for `bash` or `zsh`.
