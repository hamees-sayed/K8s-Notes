The smalles unit of a k8s cluster is a Pod. It is a collection of one or more docker containers. Any given pod can be composed of multiple, tightly coupled containers or just a single container. Whenever a pod is created, a new created IP address is assigned to that pod

![Imgur](https://imgur.com/xtUIIjy.png)


How to create a Pod?  

- First write a `pod.yml` file: 
```
apiVersion: v1
kind: Pod
metadata:
	name: nginx
	labels: 
		environment: production
		app: nginx
spec: 
	containers:
	- name: nginx
	  image: nginx:1.14.2
	  ports: 
	  - containerPort: 8000
```

To create the pod shown above, type: 
```
$ kubectl apply -f pod.yml
```


Now let's take an example of a Go application that is connected to a Redis database and we have deployed the database and application on two seperate containers and these two containers are deployed on two seperate pods each. Hence, each pod will have their own IP address, if one pod breaks or dies and a new pod is created to replace it a new a IP address will be allocated to this newly formed pod. In that case managing the pod configuration becomes difficult and to solve this problem, another k8s component named “[[Service]]” comes into picture. 

