This document provides an overview of the `innabox-fulfillment-cli` command-line tool, a Go-based interface for the fulfillment API.

### **Installation and Setup**

To use the `innabox-fulfillment-cli`, you'll first need to log in to the service.

**Login:**
The `login` command saves the connection and authentication details necessary to interact with the fulfillment API.

```bash
fulfillment-cli login [flags]
```

**Login Flags:**

  * `--address`: The server address. This can also be set using the `FULFILLMENT_SERVICE_ADDRESS` environment variable.
  * `--insecure`: Disables verification of TLS certificates and hostnames.
  * `--plaintext`: Disables the use of TLS for communications.
  * `--token`: Specifies the authentication token. This can also be set using the `FULFILLMENT_SERVICE_TOKEN` environment variable.
  * `--token-script`: Provides a shell command that will be executed to obtain the token. For example, to get a token for a Kubernetes service account, you could use:
    `--token-script 'kubectl create token -n example client --duration 1h'`

### **Core Commands**

The `innabox-fulfillment-cli` provides several commands for managing resources.

#### **`create`**

The `create` command is used to create new objects.

**Usage:**

```bash
fulfillment-cli create [OPTION]...
```

**Subcommands:**

  * `clusterorder`: Creates a new cluster order.

    **Usage:**

    ```bash
    fulfillment-cli create clusterorder [flags]
    ```

    **Flags:**

      * `--template-id`: Specifies the template identifier for the cluster order (required).

**Flags:**

  * `-f`, `--filename`: The name of the file containing the object to create. Use `-` to read from standard input (required).

#### **`delete`**

The `delete` command removes objects.

**Usage:**

```bash
fulfillment-cli delete OBJECT [OPTION]... [ID]...
```

#### **`describe`**

The `describe` command provides a detailed description of a resource.

**Usage:**

```bash
fulfillment-cli describe
```

**Subcommands:**

  * `clusterorder`: Describes a cluster order.

    **Usage:**

    ```bash
    fulfillment-cli describe clusterorder [flags] ID
    ```

#### **`edit`**

The `edit` command allows for editing objects.

**Usage:**

```bash
fulfillment-cli edit OBJECT ID
```

**Flags:**

  * `-o`, `--output`: Specifies the output format, either `json` or `yaml`. [cite\_start]The default is `yaml`[cite: 3779].

#### **`get`**

The `get` command retrieves information about objects.

**Usage:**

```bash
fulfillment-cli get OBJECT [OPTION]... [ID]...
```

**Subcommands:**

  * `kubeconfig`: Retrieves the kubeconfig for a cluster.
    **Usage:**
    ```bash
    fulfillment-cli get kubeconfig [OPTION]...
    ```
    **Flags:**
      * `--cluster`: The identifier of the cluster (required).
  * `password`: Retrieves the password for a cluster.
    **Usage:**
    ```bash
    fulfillment-cli get password [OPTION]...
    ```
    **Flags:**
      * `--cluster`: The identifier of the cluster (required).

**Flags:**

  * `--filter`: A CEL expression to filter results.
  * `--include-deleted`: Includes deleted objects in the results.
  * `-o`, `--output`: Specifies the output format, one of `table`, `json`, or `yaml`. [cite\_start]The default is `table`[cite: 3795].

#### **`logout`**

The `logout` command discards the saved connection and authentication details.

**Usage:**

```bash
fulfillment-cli logout [flags]
```
