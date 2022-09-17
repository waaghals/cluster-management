# Cluster Infrastructure
This repository contains infrastructure applications which are deployed to most clusters.
These applications provide the developers with the necessary tools to easily deploy and manager their own applications.

## List of applications
| Application | Management cluster | Other Clusters |
|-------------|--------------------|----------------|
| ArcoCD      | yes                | no             |
| ArcoCD      | yes                | no             |
| CertManager | yes                | yes            |
| Prometheus  | yes                | yes            |
| Thanos      | yes                | no             |
| Grafana     | yes                | no             |
| Linkerd     | no                 | yes            |


## Bootstrapping
# ArgoCD
Because ArgoCD is not available on an empty cluster, there is no way for it to deploy itself.
When we initially manually deploy ArgoCD, it will attempt to fetch the configured github repository with the manifests.
This will fail.

We need to seed the cluster with a private key for sealed-secrets.

1. [Deploy a secret](https://github.com/bitnami-labs/sealed-secrets/blob/main/docs/bring-your-own-certificates.md) labeled `sealedsecrets.bitnami.com/sealed-secrets-key: active`
2. Generate sealed-secrets in the repository and commit them.
2. Manually deploy ArgoCD
    ```shell
    cd argocd
    kustomize build | kubectl apply -f -
    ```
   Because we deploy the CRDs from the same kustomization, we might need to deploy it multiple times until all CRD are succesfully registered.

# Configuring credentials
## Cert-manager
1. Create service-account 'cert-manager' with the role 'DNS Administrator'
2. Create new JSON key for this service account
3. Save the JSON as a secret in Vault at 'secret/cert-manager/gcloud'
4. Perform a hard refresh in Argocd for 'cert-manager-manifest-management'

## External-dns
1. Create service-account 'external-dns' with the role 'DNS Administrator'
2. Create new JSON key for this service account
3. Save the JSON as a secret in Vault at 'secret/external-dns/gcloud'
4. Perform a hard refresh in Argocd for 'external-dns-manifest-management'

## Loki
1. Create service-account 'loki' with the roles 'Storage Admin' & 'Storage Object Admin'
2. Create new JSON key for this service account
3. Save the JSON as a secret in Vault at 'secret/loki/gcloud'

1. Generate a password  and save it in Vault at 'secret/loki#password'
2. Encode the password as htpasswd
3. Store encoded password in Vault at 'secret/loki#htpasswd'

# Mimir
1. Create service-account 'mimir' with the roles 'Storage Admin' & 'Storage Object Admin'
2. Create new JSON key for this service account
3. Save the JSON as a secret in Vault at 'secret/mimir/gcloud'

1. Generate a password  and save it in Vault at 'secret/mimir#password'
2. Encode the password as htpasswd
3. Store encoded password in Vault at 'secret/mimir#htpasswd'
 

# TODO's
* Configure all credentials from sealed-secrets
* Enable autoscaling

## Checklist
☑
☒
☐
| Application    | Json log format | Prometheus metrics | Grafana dashboard | Sealed secrets     | Tracing | Alertmanager | 
|----------------|-----------------|--------------------|-------------------|--------------------|---------|--------------|
| ArgoCD         |                 |                    |                   |                    |         |              |
| Cert-Manager   |                 |                    |                   |                    |         |              |
| External-DNS   |                 |                    |                   |                    |         |              |
| Fluent-Bit     |                 |                    |                   |                    |         |              |
| Grafana        |                 |                    |                   |                    |         |              |
| Loki           |                 |                    |                   |                    |         |              |
| Mimi           |                 |                    |                   |                    |         |              |
| Prometheus     |                 |                    |                   |                    |         |              |
| Sealed secrets |                 |                    |                   |                    |         |              |


# Provinioning a new cluster
1. Create a cluster however you like
2. Install the private key for sealed-secrets into the cluster by using your pre-generated private key. 
3. Create a sealed-secret in `argocd/clusters` folder with the cluster credentials. (Don't forget the `argocd.argoproj.io/secret-type: cluster` label)
