Here is a **Markdown** documentation suitable for GitHub, detailing how to install and use the **`fulfillment-cli`** command-line tool from [innabox/fulfillment-cli](https://github.com/innabox/fulfillment-cli).

---

# `fulfillment-cli`

A command-line interface (CLI) for interacting with the Innabox Fulfillment platform, including cluster provisioning and management.

> **License:** Apache 2.0
> **Maintained by:** Red Hat / Innabox team

## 🛠️ Installation

### Prerequisites

* Go 1.22+ (for building from source)
* Git

### Build from Source

```bash
git clone https://github.com/innabox/fulfillment-cli.git
cd fulfillment-cli
go build -o fulfillment-cli main.go
```

The compiled binary will be available as `./fulfillment-cli`.

## 🔐 Authentication

To interact with the API, you must be authenticated. Use the `login` command:

```bash
./fulfillment-cli login
```

This will run a script-based token source to authenticate your session.

Logout when finished:

```bash
./fulfillment-cli logout
```

## 📦 Commands Overview

| Command                 | Description                                   |
| ----------------------- | --------------------------------------------- |
| `create clusterorder`   | Create a new cluster order                    |
| `describe clusterorder` | Show details of a specific cluster order      |
| `get kubeconfig`        | Retrieve kubeconfig for a provisioned cluster |
| `get password`          | Retrieve admin password for a cluster         |
| `get`                   | List objects (clusters, templates, etc.)      |
| `edit`                  | Edit existing resources                       |
| `delete`                | Delete resources                              |

---

## 📄 Usage Examples

### Create a Cluster Order

```bash
./fulfillment-cli create clusterorder --name test-order --template my-template.yaml
```

### Describe a Cluster Order

```bash
./fulfillment-cli describe clusterorder --id 1234
```

### Get Kubeconfig

```bash
./fulfillment-cli get kubeconfig --cluster-id 1234 > kubeconfig.yaml
```

### Get Cluster Password

```bash
./fulfillment-cli get password --cluster-id 1234
```

---

## 🧪 Development & Testing

This project uses `ginkgo` and `gomega` for testing.

Run tests with:

```bash
go test ./...
```

To lint and format YAML and Go code before committing, use:

```bash
pre-commit run --all-files
```

## 📁 Directory Structure

Key components are under:

* `internal/cmd/` – CLI command definitions
* `internal/api/` – Protobuf-generated API definitions
* `internal/auth/` – Authentication handling
* `internal/config/` – CLI configuration
* `internal/logging/` – Logging setup

## 📦 Releasing

Releases are managed via [`goreleaser`](https://goreleaser.com/). Run:

```bash
goreleaser release --clean
```

To prepare a cross-platform release archive (tar.gz/zip) for GitHub.

---

## 🧾 License

This project is licensed under the [Apache 2.0 License](./LICENSE).

---

Let me know if you'd like this turned into a `README.md` file or want specific sections expanded, like configuration formats or plugin development.
