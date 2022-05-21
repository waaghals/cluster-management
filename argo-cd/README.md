# ArgoCD
ArgoCD is the tool user to automatically deploy applications to multiple clusters.
ArgoCD also manages itself, which allows for easy upgrading.

## Bootstrapping
Because ArgoCD is not available on an empty cluster, there is no way for it to deploy itself.
To deploy a fresh ArgoCD installation, first deploy the kustomize manifest for ArgoCD manually into the management cluster.

This repository does not include the secrets needed to access the git repositories.
After ArgoCD is deployed, create the neccesary secrets to access the repository, from the ArgoCD UI.
