# k8s_gitops_localdev

WIP - Not ready yet

This project creates a local CICD environment for Kubernetes, using the GitOps paradigm: everything should be under version control, including k8s and ArgoCD install steps and configuration.

Having a local CICD environment is much faster and practical than having to push to some external server to only then find out if the tests passed or not.

## Overview

Ansible will install the basic system:

1. Install a local k8s cluster using k3d.
  *Attention: It overwrites the local .kube/conf*

2. Export the local k8s_gitops_localdev repository in the cluster, creating a read-only git server

3. Install ArgoCD in the cluster 

4. Make ArgoCD watch the local repo

Hereafter, any application to be installed in k8s should be added by modifying the local repo.


## Requirements

- Ansible

- Docker

## Installation

    ansible-playbook install_tools_localhost.yml
    ansible-playbook bootstrap_k8s.yml