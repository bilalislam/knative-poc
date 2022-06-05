## install brew
```sh
$ brew install kn # knative
$ brew install knative-sandbox/kn-plugins/admin
$ brew install hey # loadtest
```

## tunnel for loadbalances
```sh
$ kn quickstart minikube
$ minikube tunnel --profile knative
$ http://hello.default.127.0.0.1.sslip.io/
$ kn revision list
```

## install dashboard
```sh
$ minikube addons enable dashboard --profile=knative
$ minikube -p knative addons enable metrics-server
$ minikube dashboard --url --profile knative
```

## first-service (microservice) like  100k and more more requests
```sh
$ kubectl apply -f hello.yaml
```

## scale to zero like auto start/stop
```sh
$ kubectl get pod -l serving.knative.dev/service=hello -w
```

## traffic splitting
```sh
$ kn service update hello \
--env TARGET=Knative
```

## monitoring
```sh
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm repo update
$ helm install prometheus prometheus-community/kube-prometheus-stack -n default -f values.yaml
$ kubectl port-forward -n default svc/prometheus-operated 9090

$ helm repo add grafana https://grafana.github.io/helm-charts
$ kubectl apply -f https://raw.githubusercontent.com/knative-sandbox/monitoring/main/grafana/dashboards.yaml
$ kubectl --namespace default port-forward $POD_NAME 3000 
$ kubectl get secret --namespace default prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
$ https://github.com/argoproj/argo-cd/blob/master/examples/dashboard.json
```

Note : May manually load from grafana dashboard  



## loadtest
```sh
$ hey -c 100 -n 200 -z 1m http://hello.default.127.0.0.1.sslip.io/
$ kubectl get pods --watch
```


## references
1. https://www.youtube.com/watch?v=fLcLgL53gqQ
2. https://knative.tips/
3. https://github.com/meteatamel/knative-tutorial
4. https://github.com/anksos/awesome-knative
5. https://ahmet.im/blog/knative-better-kubernetes-networking/
6. https://www.youtube.com/watch?v=OPSIPr-Cybs
7. https://github.com/knative/docs/blob/8f742c9f48/docs/serving/autoscaling/autoscale-go/README.md
    1. https://knative.dev/docs/serving/autoscaling/autoscale-go/
8. https://github.com/knative/serving/blob/main/docs/scaling/SYSTEM.md
9. https://raw.githubusercontent.com/knative/docs/8f742c9f4800ab88a086ba21ee814d55b7c4e952/docs/serving/autoscaling/autoscale-go/request-dashboard.png
10. https://raw.githubusercontent.com/knative/docs/8f742c9f4800ab88a086ba21ee814d55b7c4e952/docs/serving/autoscaling/autoscale-go/scale-dashboard.png
11. https://medium.com/@josephburnett_75496/knative-v0-3-autoscaling-a-love-story-d6954279a67a
12. https://stackoverflow.com/questions/21854191/generating-prime-numbers-in-go/21854246#21854246 
13. https://www.youtube.com/watch?v=hpOJHpn3z_M&list=PLj6h78yzYM2OQP0DXXmtdIHNtfFSJqVAU&t=449s
14. https://www.youtube.com/watch?v=hpOJHpn3z_M&list=PLj6h78yzYM2OQP0DXXmtdIHNtfFSJqVAU&t=180s
15. https://linkedin.github.io/school-of-sre/
16. https://raw.githubusercontent.com/knative/docs/8f742c9f4800ab88a086ba21ee814d55b7c4e952/docs/serving/autoscaling/autoscale-go/request-dashboard.png
17. https://raw.githubusercontent.com/knative/docs/8f742c9f4800ab88a086ba21ee814d55b7c4e952/docs/serving/autoscaling/autoscale-go/scale-dashboard.png
17. https://sre.google/sre-book/table-of-contents/ 
18. https://www.youtube.com/watch?v=PFmiMlobp_U
19. https://www.youtube.com/watch?v=rZKaju9h7fQ
