# Managing Multiple Clusters

## Understand your current context

```shell
$> kubectl config get-contexts
CURRENT   NAME                                CLUSTER                         AUTHINFO                        NAMESPACE
*         konvoy-docker-admin@konvoy-docker   konvoy-docker                   konvoy-docker-admin
          smacgregor-kubernetes-cluster       smacgregor-kubernetes-cluster   smacgregor-kubernetes-cluster
```
## Import a new `admin.conf` with `konfig`

```shell
kubectl konfig import --save admin.conf
kubectl config use-context 'kubernetes-admin@kommander'
```

## Inspect this new cluster

```shell
$> kubectl get cluster-info
Kubernetes master is running at https://kommander-1510-lb-control-1171959130.us-west-2.elb.amazonaws.com:6443
KubeDNS is running at https://kommander-1510-lb-control-1171959130.us-west-2.elb.amazonaws.com:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'
```
## D2iQ Clusters - Addons

```
kubectl get clusteraddons kommander -o wide
kubectl get deployments kubeaddons-controller-manager -n kubeaddons -o wide
```

```
NAME        READY   STAGE      REVISION
kommander   true    deployed   1.1.2-1

NAME                            READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES                          SELECTOR
kubeaddons-controller-manager   1/1     1            1           26h   manager      mesosphere/kubeaddons:v0.16.2   control-plane=kubeaddons-controller-manager
```

### D2iQ Clusters - OPS Portal

Get the OPS portal URL

Secret are stored in - "ops-portal-credentials"
Portal URL is exposed via "svc traefik-kubeaddons -n kubeaddons"

You can run `ops-portal-creds.sh`

```shell
*****------*****------*****------*****------*****------*****------*****
https://bc08bd812e7544c4399773801bd7056f-28404426.us-west-2.elb.amazonaws.com/ops/landing
OPSPortal Login: little_juice / AWklrZLvkt2jxWAxal37OKDiNq1uoXNRoQNlf3Bo0xOIGNpT3jSmd7a4lZcKUJM3
*****------*****------*****------*****------*****------*****------*****
```

## Cleanup your config
```
kubectl config_cleanup > ~/.kube/config.swap
kubectl config_swap
```
