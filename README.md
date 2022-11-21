# anthos-service-mesh

```
sudo apt install siege
```

```
kubectl get pods
```

```
kubectl get svc
```

```
kubectl describe svc istio-ingressgateway -n istio-system
```

```
export GATEWAY_URL=$(kubectl get svc istio-ingressgateway -o=jsonpath='{.status.loadBalancer.ingress[0].ip}' -n istio-system)
echo "The gateway address is $GATEWAY_URL"
```

```
siege http://${GATEWAY_URL}/productpage
```

```
export CLUSTER_NAME=gke
export CLUSTER_ZONE=
export GCLOUD_PROJECT=$(gcloud config get-value project)
gcloud container clusters get-credentials $CLUSTER_NAME --zone $CLUSTER_ZONE --project $GCLOUD_PROJECT
export GATEWAY_URL=$(kubectl get svc istio-ingressgateway -o=jsonpath='{.status.loadBalancer.ingress[0].ip}' -n istio-system)
```
