# k8s_gitops_localdev

WIP - Not ready yet

This project creates a local CICD environment for Kubernetes, using the GitOps paradigm: everything should be under version control, including k8s and ArgoCD install steps and configuration.

Having a local CICD environment is much faster and practical than having to push to some external server to only then find out if the tests passed or not.

## Overview

Ansible will install the basic system:

1. Install a local k8s cluster using k3d

2. Install ArgoCD in the cluster 

3. Export the local k8s_gitops_localdev repository in the cluster, creating a read-only git server

4. Make ArgoCD watch the local repo

Hereafter, any application that should be installed in k8s should be added by modifying the local repo.


## Requirements

## Installation
