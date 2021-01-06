# k8s_gitops_localdev

This project creates a local CICD environment for Kubernetes, using the GitOps paradigm: everything should be under version control, including k8s and ArgoCD install steps and configuration.

Having a local CICD environment is much faster and practical than having to push to some external server to only then find out if the tests passed or not.

## Requirements

- Ansible

- Docker

## Installation

This will install pip requirements, k3d, and argocd in localhost:

    ansible-playbook install_tools_localhost.yml

This will install the basic resources in k8s:

    ansible-playbook bootstrap_k8s.yml

It will:

1. Install a local k8s cluster using k3d. **Warning: It overwrites the local .kube/conf**

2. Export the local k8s_gitops_localdev repository in the cluster, creating a read-only git server

3. Install ArgoCD in the cluster 

4. Make ArgoCD watch the local repo

Hereafter, any application to be installed in k8s should be added by modifying the local repo.


