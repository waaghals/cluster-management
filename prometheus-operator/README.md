# Prometheus operator
Prometheus operator is installed from the kube-prometheus helm chart.
During installation both grafana and alert-manager are disabled. As these are managed separately.

## CustomResourceDefinitions and kubectl apply limitations
Because the CRD of prometheus-operator are too big to be `kubectl apply`'ed because of annotation size limit, we deploy the crds seperatly.
See The following [Github issue](https://github.com/prometheus-operator/prometheus-operator/issues/4439), and [this related comment](https://github.com/prometheus-operator/prometheus-operator/issues/4439#issuecomment-1030198014) with the suggested fix. 

Issues tracking server-side apply fix for Argo-cd
* [#2267](https://github.com/argoproj/argo-cd/issues/2267)
* [#8812](https://github.com/argoproj/argo-cd/pull/8812)