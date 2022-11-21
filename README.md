# Anthos Service Mesh

###Pre-requisite
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

```
kubectl describe gateway bookinfo-gateway
```

```
kubectl describe virtualservices bookinfo
```

```
kubectl exec -it \
$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}') -c ratings -- curl productpage:9080/productpage | grep -o "<title>.*</title>"
```

```
curl -I http://${GATEWAY_URL}/productpage
```

```
kubectl get virtualservices
```

```
kubectl describe virtualservices
```

```
kubectl get destinationrules
```
```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/master/samples/bookinfo/networking/destination-rule-all.yaml
```
```
kubectl get destinationrules
```
```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/master/samples/bookinfo/networking/virtual-service-all-v1.yaml
```
```
kubectl get virtualservices
```
```
echo $GATEWAY_URL
```
```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/master/samples/bookinfo/networking/virtual-service-reviews-test-v2.yaml
```
```
kubectl get virtualservice reviews
```
```
curl -c cookies.txt -F "username=jason" -L -X POST http://$GATEWAY_URL/login
cookie_info=$(grep -Eo "session.*" ./cookies.txt)
cookie_name=$(echo $cookie_info | cut -d' ' -f1)
cookie_value=$(echo $cookie_info | cut -d' ' -f2)
siege -c 5 http://$GATEWAY_URL/productpage --header "Cookie: $cookie_name=$cookie_value"
```
```
kubectl delete -f https://raw.githubusercontent.com/istio/istio/master/samples/bookinfo/networking/virtual-service-all-v1.yaml
```
```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/master/samples/bookinfo/networking/virtual-service-all-v1.yaml
```
```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/master/samples/bookinfo/networking/virtual-service-reviews-50-v3.yaml
```
```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/master/samples/bookinfo/networking/virtual-service-reviews-v3.yaml
```
```
kubectl delete -f https://raw.githubusercontent.com/istio/istio/master/samples/bookinfo/networking/virtual-service-all-v1.yaml
```
