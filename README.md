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

1. Optionaly install a pull through registry cache in docker, but outside k8s

2. Install a local k8s cluster using k3d.

3. Overwrite the local .kube/conf

4. Export the local k8s_gitops_localdev repository in the cluster, creating a read-only git server

5. Install ArgoCD in the cluster 

6. Make ArgoCD watch the local repo

Hereafter, any application to be installed in k8s should be added by modifying the local repo, particularly the argocd-apps/argocd-apps folder.

## To add a new application

1. Create a new ArgoCD application file in argocd-apps/argocd-apps. selfreference.yml can be used as an example.

2. Commit the change in the local repo (no need to push to github).

3. Auto-refresh occurs every 3 minutes. To trigger it manually,  you have to use `kubectl port-forward svc/argocd-server -n argocd 8080:443`,  `argocd login localhost:8080`, and `argocd app sync argocd-apps`. The user is 'admin' and the password is the name of the argocd-server pod.

TODO: include some sample CI workflows
