Based on the provided files, here is an example YAML for a `Cluster` object. This example is derived from the structure and comments found in the `cluster_type.pb.go` file.

You can use this YAML with the `fulfillment-cli create -f <filename>` command.

```yaml
# cluster.yaml
full_name: fulfillment.v1.Cluster
spec:
  node_sets:
    compute:
      host_class: "acme_1tb"
      size: 3
    gpu:
      host_class: "acme_1tb_h100"
      size: 3
```

### Explanation of Fields

  * **`full_name`**: This specifies the full name of the message type, which is `fulfillment.v1.Cluster`.
  * **`spec`**: This section contains the desired details for the cluster.
  * **`node_sets`**: This is a map defining the desired sets of nodes for the cluster. In this example, there are two node sets named `compute` and `gpu`.
      * **`host_class`**: This is a string that identifies the class of hosts for the node set. For example, `acme_1tb`. The user does not have permission to change this field after creation.
      * **`size`**: This is an integer specifying the number of nodes in the set. This field can be updated by the user.
