## FerretDB –  a truly Open Source MongoDB alternative

### External access

By default, external access to the FerretDB port isn't available. 
This could be changed by applying the following YAML to your cluster with `kubectl apply -f ferretdb-service.yaml` 
(or whatever you call the file containing the contents below) 
which will launch a [Civo Load Balancer](https://www.civo.com/load-balancers) (at an additional charge):

```
apiVersion: v1
kind: Service
metadata:
  name: ferretdb-service
spec:
  type: LoadBalancer
  ports:
    - port: 27017
      targetPort: 27017
      protocol: TCP
  selector:
    app: ferretdb
```

This will open up `YOUR_CLUSTER_ID.k8s.civo.com:27017` to the whole world. 
You should lock this down in the [firewall](https://www.civo.com/account/firewalls) 
automatically created in Civo for your Kubernetes cluster. 
Locking down the firewall will only affect access from OUTSIDE of your Kubernetes cluster, 
access from your applications within Kubernetes will not be affected.
