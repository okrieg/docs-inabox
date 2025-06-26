I'll generate comprehensive GitHub-ready documentation for the `innabox/fulfillment-cli` repository based on the codebase structure and functionality I can see.

# Fulfillment CLI

A command-line interface for managing Kubernetes clusters through the fulfillment API service. [1](#1-0) 

## Overview

The Fulfillment CLI provides a comprehensive set of tools for managing cluster resources including clusters, cluster templates, cluster orders, and host classes through a gRPC-based API. [2](#1-1)  The CLI is built using the Cobra framework and supports multiple output formats for flexible data consumption.

## Features

- **Multi-platform support**: Linux, Windows, and macOS [3](#1-2) 
- **Multiple authentication methods**: Direct token and dynamic token script authentication
- **Flexible output formats**: Table, JSON, and YAML output [4](#1-3) 
- **Advanced filtering**: CEL (Common Expression Language) expressions for result filtering [5](#1-4) 
- **Secure communication**: TLS support with configurable security options
- **Automatic logging**: File-based logging to avoid output interference [6](#1-5) 

## Installation

### Pre-built Binaries

Download the latest release for your platform from the [releases page](https://github.com/innabox/fulfillment-cli/releases). The CLI is built without CGO dependencies for maximum portability. [7](#1-6) 

### Building from Source

**Requirements:**
- Go 1.22.9 or later [8](#1-7) 

```bash
git clone https://github.com/innabox/fulfillment-cli.git
cd fulfillment-cli
go build -o fulfillment-cli main.go
```

## Quick Start

### 1. Authentication

Before using the CLI, authenticate with the fulfillment service:

```bash
# Direct token authentication
fulfillment-cli login --address <server-address> --token <your-token>

# Dynamic token authentication (e.g., Kubernetes service accounts)
fulfillment-cli login --address <server-address> --token-script "kubectl create token -n example client --duration 1h"
``` [9](#1-8) 

### 2. Basic Usage

```bash
# List all clusters
fulfillment-cli get clusters

# Get specific cluster details
fulfillment-cli get clusters <cluster-id>

# Create a new cluster
fulfillment-cli create clusters -f cluster.yaml

# Get cluster kubeconfig
fulfillment-cli get kubeconfig <cluster-id>
``` [10](#1-9) 

## Commands

### Core Commands

| Command | Description |
|---------|-------------|
| `get` | Retrieve objects from the fulfillment service |
| `create` | Create new objects |
| `delete` | Delete objects |
| `describe` | Get detailed information about objects |
| `edit` | Modify existing objects |
| `login` | Save connection and authentication details |
| `logout` | Remove stored authentication | [2](#1-1) 

### Supported Resource Types

- **clusters** - Kubernetes clusters
- **clustertemplates** - Cluster templates
- **clusterorders** - Cluster provisioning orders
- **hostclasses** - Available hardware specifications

### Advanced Features

#### Output Formats

```bash
# Table format (default)
fulfillment-cli get clusters

# JSON format
fulfillment-cli get clusters -o json

# YAML format
fulfillment-cli get clusters -o yaml
```

#### Filtering with CEL Expressions

Use Common Expression Language (CEL) for powerful filtering:

```bash
# Filter clusters by name pattern
fulfillment-cli get clusters --filter "metadata.name.startsWith('prod')"

# Filter by multiple conditions
fulfillment-cli get clusters --filter "status.state == 'READY' && spec.node_sets.size() > 1"
``` [5](#1-4) 

#### Include Deleted Objects

```bash
fulfillment-cli get clusters --include-deleted
``` [11](#1-10) 

## Configuration

### Environment Variables

| Variable | Description |
|----------|-------------|
| `FULFILLMENT_SERVICE_ADDRESS` | Server address |
| `FULFILLMENT_SERVICE_TOKEN` | Authentication token |
| `FULFILLMENT_SERVICE_TOKEN_SCRIPT` | Token generation script | [12](#1-11) 

### Connection Options

| Flag | Description |
|------|-------------|
| `--plaintext` | Disable TLS for communications |
| `--insecure` | Disable TLS certificate and hostname verification | [13](#1-12) 

### Configuration Storage

Configuration is automatically saved in your user cache directory. [14](#1-13)  The configuration includes: [15](#1-14) 

- Connection details (server address)
- Authentication information (token or token script)
- TLS settings

## Data Types

The CLI works with several core data types representing cluster infrastructure:

### Cluster Types
- **Cluster**: Main cluster resource with spec and status [16](#1-15) 
- **ClusterSpec**: Desired cluster configuration
- **ClusterStatus**: Current cluster state and conditions
- **ClusterNodeSet**: Homogeneous groups of nodes within a cluster

### Host Class Types
- **HostClass**: Hardware specifications available for cluster nodes [17](#1-16) 

Host classes abstract hardware details similar to cloud provider instance types, with fields for unique identification, metadata, title, and detailed markdown descriptions.

## Development

### Project Structure

```
├── internal/
│   ├── api/          # Generated gRPC clients and Protocol Buffer types
│   ├── auth/         # Authentication logic
│   ├── cmd/          # Command implementations
│   ├── config/       # Configuration management
│   ├── logging/      # Logging utilities
│   ├── reflection/   # gRPC reflection utilities
│   └── testing/      # Test utilities
├── main.go          # Application entry point
├── go.mod           # Go module definition
└── .goreleaser.yaml # Release configuration
```

### Key Dependencies [18](#1-17) 

- **Cobra** - CLI framework
- **gRPC** - API communication  
- **Protocol Buffers** - Data serialization
- **CEL-Go** - Expression language for filtering
- **OAuth2** - Authentication support

### Testing

The project uses Ginkgo and Gomega for testing. [19](#1-18) 

```bash
# Run tests
go test ./...
```

### API Code Generation

The CLI uses Protocol Buffer definitions for API code generation. [20](#1-19)  Generated code includes both standard and proto-opaque variants for different usage patterns.

## Logging

The CLI automatically configures logging to avoid mixing log messages with command output. [6](#1-5) 

**Log file location**: `~/.cache/fulfillment-cli/fulfillment-cli.log`

Logging behavior can be customized using command-line flags. [21](#1-20) 

## License

This project is licensed under the Apache License 2.0. [22](#1-21) 

Copyright (c) 2025 Red Hat Inc.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Run the test suite
6. Submit a pull request

## Support

For issues and questions:
- Open an issue on GitHub
- Check the documentation for common use cases
- Review the CLI help: `fulfillment-cli --help`

**Notes**

This CLI requires proper authentication before use. All commands that communicate with the fulfillment service will fail without valid credentials. The CLI automatically handles gRPC reflection to discover available operations and supports both individual object operations and bulk listing with advanced filtering capabilities.

Wiki pages you might want to explore:
- [Data Types (innabox/fulfillment-cli)](/wiki/innabox/fulfillment-cli#5.2)
- [Service APIs (innabox/fulfillment-cli)](/wiki/innabox/fulfillment-cli#5.3)
