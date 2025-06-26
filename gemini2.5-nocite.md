### Using the Innabox Fulfillment CLI

This document provides instructions on how to use the `innabox-fulfillment-cli`, a command-line tool for interacting with the Innabox Fulfillment API.

### Installation

To use the `innabox-fulfillment-cli`, you need to have Go installed on your system. You can build the tool from the source by running the following command in the root directory of the repository:

```sh
go build
```

### Configuration

Before using the CLI, you need to configure it with the necessary connection and authentication details.

#### Login

The `login` command saves the connection and authentication details.

```sh
fulfillment-cli login --address <server_address> --token <authentication_token>
```

**Arguments:**

  * `--address`: **(Required)** The address of the fulfillment API server. This can also be set using the `FULFILLMENT_SERVICE_ADDRESS` environment variable.
  * `--token`: The authentication token. This can also be set using the `FULFILLMENT_SERVICE_TOKEN` environment variable.
  * `--token-script`: A shell command that will be executed to obtain the token. For example: `--token-script 'kubectl create token -n example client --duration 1h'`. This can also be set using the `FULFILLMENT_SERVICE_TOKEN_SCRIPT` environment variable.
  * `--plaintext`: Disables the use of TLS for communication.
  * `--insecure`: Disables verification of TLS certificates and hostnames.

The configuration is saved in a file named `config.json` inside the `fulfillment-cli` directory within your user-specific configuration directory.

#### Logout

The `logout` command discards the saved connection and authentication details.

```sh
fulfillment-cli logout
```

### General Usage

The CLI follows a standard `verb-noun` syntax.

### Commands

#### `create`

The `create` command is used to create new objects.

**Usage:**

```sh
fulfillment-cli create -f <filename>
```

  * The `-f` or `--filename` flag is mandatory and specifies the file containing the object definition. Use `-` to read from standard input.

You can create a `ClusterOrder` using a YAML file like the following:

```yaml
# cluster-order.yaml
---
apiVersion: fulfillment.innabox.com/v1
kind: ClusterOrder
spec:
  template_id: "your-template-id"
```

Then create it with:

```sh
fulfillment-cli create -f cluster-order.yaml
```

#### `get`

The `get` command retrieves information about objects.

**Usage:**

```sh
fulfillment-cli get <object_type> [object_id] [flags]
```

**Available Object Types:**

  * `clusters`
  * `clusterorders`
  * `clustertemplates`
  * `hostclasses`

**Flags:**

  * `-o`, `--output <format>`: Specifies the output format. Supported formats are `table` (default), `json`, and `yaml`.
  * `--filter <expression>`: Filters results using a CEL expression.
  * `--include-deleted`: Includes deleted objects in the output.

**Examples:**

  * To get a list of all cluster templates:
    ```sh
    fulfillment-cli get clustertemplates
    ```
  * To get the details of a specific cluster order in JSON format:
    ```sh
    fulfillment-cli get clusterorder <order_id> -o json
    ```
  * To get the `kubeconfig` for a cluster:
    ```sh
    fulfillment-cli get kubeconfig --cluster <cluster_id>
    ```
  * To get the password for a cluster:
    ```sh
    fulfillment-cli get password --cluster <cluster_id>
    ```

#### `describe`

The `describe` command provides a detailed description of a specific object.

**Usage:**

```sh
fulfillment-cli describe <object_type> <object_id>
```

**Available Object Types:**

  * `clusterorder`

**Example:**

  * To describe a cluster order:
    ```sh
    fulfillment-cli describe clusterorder <order_id>
    ```

#### `edit`

The `edit` command allows you to edit an object in your default text editor.

**Usage:**

```sh
fulfillment-cli edit <object_type> <object_id>
```

Your `EDITOR` or `VISUAL` environment variables will be used to determine which editor to open.

**Example:**

  * To edit a cluster:
    ```sh
    fulfillment-cli edit cluster <cluster_id>
    ```

#### `delete`

The `delete` command removes an object.

**Usage:**

```sh
fulfillment-cli delete <object_type> <object_id>
```

**Example:**

  * To delete a cluster order:
    ```sh
    fulfillment-cli delete clusterorder <order_id>
    ```

### Logging

The CLI tool generates log files to the user's cache directory. For example, on a Linux system, the log file for a binary named `fulfillment-cli` would be located at `~/.cache/fulfillment-cli/fulfillment-cli.log`. The default log level is `error`.

You can customize the logging behavior with the following flags:

  * `--log-level`: Sets the log level (`debug`, `info`, `warn`, `error`).
  * `--log-file`: Specifies a file to write logs to. Can be `stdout` or `stderr`.
  * `--log-redact`: Set to `false` to disable redaction of sensitive information.
