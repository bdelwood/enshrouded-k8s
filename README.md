# enshrouded-k8s

A Helm chart to deploy an Enshrouded dedicated server. This chart relies on the [`mornedhels/enshrouded-server`](https://github.com/mornedhels/enshrouded-server) image.

# How to use

```bash
helm repo add enshrouded-k8s https://bdelwood.github.io/enshrouded-k8s/
helm repo update
helm install enshrouded-server enshrouded-k8s/enshrouded-k8s  \
  --set gameServer.serverName=enshrouded-example \
  --set gameServer.password=changeme
```

As Enshrouded seems to rely on the query port being enabled to find and connect to servers, the server is configured with the query port exposed by default.

The chart will generate a server password, which can be retrieved with

```bash
kubectl get secrets <secrets-name> -o json | jq '.data | map_values(@base64d)'
```

Alternatively, the password can be supplied in the `values` file or by specifying existing secrets. The secret must have a `server-password` key.

By default, the chart will provision a PVC using the default StorageClass. You can also provide an existing PVC, or change the StorageClass.

# Configuration

Full configuration options are detailed in the [Chart readme](/chart/enshrouded-k8s/README.md).

# Roadmap

- [ ] Implement health check/readiness check
