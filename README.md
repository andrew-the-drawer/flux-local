# Experimentation with Flux

- Flux: https://fluxcd.io/flux/concepts/
- Capacitor: https://github.com/gimlet-io/capacitor

## PostgreSQL

We can deploy postgreSQL cluster with [zalando-operator](https://github.com/zalando/postgres-operator)

```bash
kind create cluster --name=trung
```

Note: Sample cluster config is in [k8s-local](https://github.com/andrew-the-drawer/k8s-local/blob/main/kind/cluster.yml)

We might need to deploy LB with [cloud-provider-kind](https://github.com/kubernetes-sigs/cloud-provider-kind)

```bash
sudo cloud-provider-kind
```

Then we deploy Flux to the cluster:

```bash
flux --context=kind-trung bootstrap git \
    --url=ssh://git@<host>/<org>/<repository> \
    --branch=main \
    --private-key-file=<path/to/private.key> \
    --path trung
```

Port-forward the `trung-pooler` service (in the `default` namespace) to access to PostgreSQL database

```bash
kubectl --context=kind-trung port-forward svc/trung-pooler 54321:5432
```

and access via `postgresql://localhost:54321`

(For the user name and password, please check the K8s cluster secrets in the `default` namepsace)

To create more cluster via `postgres-operator-ui`, port-forward the service to access it:

```bash
kubectl --context=kind-trung port-forward svc/postgres-operator-ui 8081:80
```

and access via http://localhost:8081
