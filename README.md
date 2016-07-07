# VerneMQube
## VerneMQ on Kubernetes - Auto Discovery Cluster

### Prerquisties

- First you need a [Kubernetes Cluster](http://kubernetes.io/gettingstarted/)
- Then you need to run [Kubernetes Pod IP finder](https://github.com/thesandlord/kubernetes-pod-ip-finder) for nodes discovery

NOTE: I didn't managed to make the node discovery work with services because of Erlang Port Mapper daemon logic and Service ClusterIP limitation. If you make it work let me know what did you do.

### How to Use

1. Launch Service
   - ```kubectl create -f vernemq-service.yaml```
1. Launch Deployment
   - ```kubectl create -f vernemq-deployment.yaml```

### Checking cluster status

```kubectl get pods```

```
vernemq-3099899313-7gkrr          2/2       Running   0          17s
vernemq-3099899313-qbi91          2/2       Running   0          17s
vernemq-3099899313-u5rrq          2/2       Running   0          17s
kubernetes-pod-ip-finder-6le9j   1/1       Running   0          4h
```

```kubectl exec vernemq-3099899313-7gkrr vmq-admin cluster status```

```
+------------------+-------+
|       Node       |Running|
+------------------+-------+
|VerneMQ@172.17.0.6| true  |
|VerneMQ@172.17.0.7| true  |
|VerneMQ@172.17.0.8| true  |
+------------------+-------+
```
