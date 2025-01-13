# Experimentation with Flux

- Flux: https://fluxcd.io/flux/concepts/
- Capacitor: https://github.com/gimlet-io/capacitor

## Architecture:

1 cluster with 2 namespaces:
- dev
- prod

On both namespaces, deploy 1 PostgreSQL cluster.

Deploy a simple NodeJS app connecting to PostgreSQL with local registry on both envs: dev and prod.
