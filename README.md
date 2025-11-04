## Kubeflow Manifests for DATUM

The Kubeflow installation manifests for **Defence Analytics, Trust, and Unified Mission-Insight (DATUM)**.

DATUM currently targets **Kubeflow AI Platform v1.10.2**, while the underlying base was originally derived from the **v1.7.0** upstream manifests.
Work is actively underway to modernize and replace legacy components incrementally, ensuring full compatibility with the Aurora Platform (AUR) and future Kubeflow releases.

## Prerequisites

- **[K3D][k3d-install]** – for local testing
- **[kubectl][kubectl-install]** – for applying manifests
- **[Taskfile][taskfile-install]** – for task automation

## Commands

Generate and save the rendered manifests locally for debugging:

```sh
# kubectl kustomize stacks/datum
task stack:datum:preview
```

Deploy Kubeflow on top of the Aurora Platform (AUR):

```sh
# kubectl apply --kustomize stacks/datum
task stack:datum
```

## Documentation

This `kustomize` directory mirrors the structure of the upstream **[Kubeflow Manifests][kubeflow-manifests]** repository.

While the upstream project organizes its content under three main directories, an additional one — `stacks` — has been added for DATUM-specific configurations.

| Directory      | Purpose                                                                             |
|----------------|-------------------------------------------------------------------------------------|
| `applications` | Kubeflow’s official components, maintained by the respective Working Groups (WGs)   |
| `common`       | Common services, maintained by the Manifests WG                                     |
| `experimental` | Third-party integrations and platform experiments                                   |
| `stacks`       | Environment-specific overlays for Kubeflow and dependencies (`datum`, `argo`, etc.) |

## Stacks

Different configuration layers for Kubeflow and its dependencies.

| Directory | Purpose                                                                                                  |
|-----------|----------------------------------------------------------------------------------------------------------|
| `datum`   | Installs Kubeflow v1.10.2 on top of the Aurora Platform (AUR); migration from v1.7.0 base is in progress |
| `argo`    | Provides Argo CD Application metadata for the `das` stack                                                |
| `local`   | Adjustments for running the `das` stack in local, dev, and CI environments                               |

### DATUM

The `datum` stack is designed to deploy Kubeflow on top of the **Aurora Platform (AUR)**, which already provides core dependencies such as networking, observability, and security baselines.

<!-- Links Referenced -->

[k3d-install]:        https://k3d.io/v5.2.2/#installation
[kubectl-install]:    https://kubernetes.io/docs/tasks/tools/#kubectl
[taskfile-install]:   https://taskfile.dev/#/installation
[kubeflow-manifests]: https://github.com/kubeflow/manifests
