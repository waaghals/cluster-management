# Cluster Infrastructure
This repository contains infrastructure applications which are deployed to most clusters.
These applications provide the developers with the necessary tools to easily deploy and manager their own applications.

## List of applications
| Application | Management cluster | Other Clusters |
|-------------|--------------------|-----------------|
| ArcoCD      | yes                | no              |
| ExternalDNS | yes                | yes             |
| CertManager | yes                | yes             |
| Prometheus  | yes                | yes             |
| Thanos      | yes                | no              |
| Grafana     | yes                | no              |
| Linkerd     | no                 | yes             |

# Deployment order
Yellow: ApplicationSet
Orange: Application
```mermaid
graph LR
 style root stroke:yellow
 style argocd stroke:orange
 style prometheus-operator stroke:yellow
 style external-dns stroke:yellow
 style cert-manager stroke:yellow
 style grafana stroke:orange
 style linkerd stroke:yellow
 style prometheus-operator-cluster-a stroke:orange
 style prometheus-operator-cluster-b stroke:orange
 style prometheus-operator-cluster-c stroke:orange
 style external-dns-cluster-a stroke:orange
 style external-dns-cluster-b stroke:orange
 style external-dns-cluster-c stroke:orange
 style cert-manager-cluster-a stroke:orange
 style cert-manager-cluster-b stroke:orange
 style cert-manager-cluster-c stroke:orange
 style linkerd-cluster-a stroke:orange
 style linkerd-cluster-b stroke:orange
 style linkerd-cluster-c stroke:orange
 
 root-->argocd
 argocd-->root
 root-->prometheus-operator
 prometheus-operator-->prometheus-operator-cluster-a
 prometheus-operator-->prometheus-operator-cluster-b
 prometheus-operator-->prometheus-operator-cluster-c
 root-->external-dns
 external-dns-->external-dns-cluster-a
 external-dns-->external-dns-cluster-b
 external-dns-->external-dns-cluster-c
 root-->cert-manager
 cert-manager-->cert-manager-cluster-a
 cert-manager-->cert-manager-cluster-b
 cert-manager-->cert-manager-cluster-c
 root-->grafana
 root-->linkerd
 linkerd-->linkerd-cluster-a
 linkerd-->linkerd-cluster-b
 linkerd-->linkerd-cluster-c
```