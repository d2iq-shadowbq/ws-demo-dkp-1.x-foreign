#!/usr/bin/env bash
uname=$(kubectl get secrets -n kubeaddons ops-portal-credentials -o jsonpath={.data.username} | base64 -d -)
pass=$(kubectl get secrets -n kubeaddons ops-portal-credentials -o jsonpath={.data.password} | base64 -d -)
echo "*****------*****------*****------*****------*****------*****------*****"
echo "https://$(kubectl get svc traefik-kubeaddons -n kubeaddons -o jsonpath={.status.loadBalancer.ingress[*].hostname})/ops/landing"
echo "OPSPortal Login: $uname / $pass"
echo "*****------*****------*****------*****------*****------*****------*****"