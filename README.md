# enshrouded-k8s

[![GitHub License](https://img.shields.io/github/license/bdelwood/enshrouded-k8s?style=flat-square)](https://github.com/bdelwood/enshrouded-k8s/blob/master/LICENSE)
[![GitHub release](https://img.shields.io/github/v/release/bdelwood/enshrouded-k8s?style=flat-square)](https://github.com/bdelwood/enshrouded-k8s/releases)
[![GitHub Downloads](https://img.shields.io/github/downloads/bdelwood/enshrouded-k8s/total?style=flat-square)](https://github.com/bdelwood/enshrouded-k8s/releases)

A Helm chart to deploy an Enshrouded dedicated server. This chart relies on the [`mornedhels/enshrouded-server`](https://github.com/mornedhels/enshrouded-server) image.

# How to use

```bash
helm repo add enshrouded-k8s https://bdelwood.github.io/enshrouded-k8s/
helm repo update
helm install enshrouded-server enshrouded-k8s/enshrouded-k8s  \
  --set gameServer.serverName=enshrouded-example \
  --set gameServer.password=changeme
```

The chart will generate a server password, which can be retrieved with

```bash
kubectl get secrets <secrets-name> -o json | jq '.data | map_values(@base64d)'
```

Alternatively, the password can be supplied in the `values` file or by specifying existing secrets. The secret must have a `server-password` key.

> [!TIP]
> Passwords for roles can be provided in the same secret as `<role-name>-password`.

By default, the chart will provision a PVC using the default StorageClass. You can also provide an existing PVC, or change the StorageClass.

# Configuration

Full configuration options are detailed in the [Chart readme](/chart/enshrouded-k8s/README.md).
