# ArgoCD
ArgoCD is the tool user to automatically deploy applications to multiple clusters.
ArgoCD also manages itself, which allows for easy upgrading.

## Bootstrapping
Because ArgoCD is not available on an empty cluster, there is no way for it to deploy itself.
To deploy a fresh ArgoCD installation, first deploy the kustomize manifest for ArgoCD manually in the management cluster.

## Helm
Helm is used to deploy ArgoCD. But we use a umbrella chart to deploy ArgoCD.
ArgoCD is taken on as a dependency in the umbrella chart.
This allows us to install other resources related to ArgoCD together with the ArgoCD Helm Chart.
One of those resources we deploy next to ArgoCD is the root application.

## Root application
The root application is a ArgoCD application which deploys other ArgoCD application(set)s.
It does this according to the ArgoCD apps-in-apps strategy.
