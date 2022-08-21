Ingress refers to the act of entering. It is the same in Kubernetes world as well. Ingress means the traffic that enters the cluster and egress is the traffic that exits the cluster. The role of Ingress is to maintain the DNS routing configurations. The Ingress controller does the actual routing by reading the routing rules from ingress objects stored in etcd.  

![img](https://miro.medium.com/max/958/1*K27cGIItdm_OBLLB8i0gAA.png)

Ingress is like an extra layer on top of k8s service, all services are [loadbalanced](https://www.nginx.com/resources/glossary/load-balancing/) as well. So if you have multiple pods deployed to k8s cluster and all those pods are connected to a single k8s service, as we know the service is loadbalanced, the service will internally decide to which pod the request has to be passed.  

To create an Ingress resource, we need to deploy an Ingress Controller. [ingress-nginx] is the most widely used ingress controller. 
Once you have deployed the ingress controller, we can create an ingress resource.  
For example: 

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-resource-backend
spec:
  defaultBackend:
    resource:
      apiGroup: k8s.example.com
      kind: StorageBucket
      name: static-assets
  rules:
    - http:
        paths:
          - path: /icons
            pathType: ImplementationSpecific
            backend:
              resource:
                apiGroup: k8s.example.com
                kind: StorageBucket
                name: icon-assets
```

To view the above ingress, you type:  
```
$ kubectl describe ingress ingress-resource-backend
```

For example we have deployed application and db to seperate pods and the db has to be changed so the application pod has to now connect to the new database that we have deployed to work properly. Typically we must have created the configurations for the db to connect to the database. So to change the config, we'll have to again build the application and deploy the application which is not a viable option.    

And that's where “[[ConfigMap]]” comes into picture.
