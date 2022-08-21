Service is an abstract layer on top of pods which provides a single static IP address and DNS name by which pods can be accessed. 

Service and Pods have different lifecycles so whenever a pod is destroyed, service will be unaffected. So whenever a new pod is created, it will be connected to the particular service. So service will manage the load balancing configuration of the pods and help them scale easily.   

![Imgur](https://imgur.com/wPhG1Ak.png)

Services can be internal service or external service. Suppose you want to access the application from outside the cluster so for that you'd create an external service and foryour database you'd create an internal service because from outside you should not be allowed to access the database from the outside.  

How to define a Service? 
Suppose you have a pod that we created in pod.yml listening on port 8000 and contains a label `app.kubernetes.io/name=MyApp`: 
```
spiVersion: v1
kind: Service
metadata: 
	name: my-service
spec: 
	selector:
		app.kubernetes.io/name: MyApp
	ports: 
		- protocol: TCP
		  port: 30
		  targetPort: 8000
```

So when you create an external service, that service will be having an IP address and port details. But this is not a good practice to share your application with your users. You need to have a specific DNS or domain name to share with the users so how can it be handled when a user hits that particular domain name then from that domain name your service IP address is called for external user to access the application.   

To solve this issue,  “[[Ingress]]” component plays a big part.    
