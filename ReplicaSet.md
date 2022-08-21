A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods. It ensures how many replica of pod should be running.   

![img](https://www.fosstechnix.com/wp-content/uploads/2020/10/replicaset-controllers-arch.png)

A ReplicaSet is linked to its Pods via the Pod's metadata.ownerReferences field, which specifies what resource the current object is owned by. All Pods acquired by a ReplicaSet have their owning ReplicaSet's identifying information within their ownerReferences field. It's through this link that the ReplicaSet knows of the state of the Pods it is maintaining and plans accordingly.  

Example of a replica set and how it is deployed:  File name = `backend.yaml`

```
apiVersion: apps/v1 
kind: ReplicaSet 
metadata:
	name: Tomcat-ReplicaSet
spec:
	replicas: 3
	selector:
	    matchLabels:
	        tier: Backend 
	template:
		metadata:
		    labels:
			    tier: Backend
		spec:
			containers:
			- name: Tomcat
			image: tomcat: 8.0
		    ports:
		    - containerPort: 3000
```

```
$ kubectl apply -f frontend.yaml
```

To see all the current ReplicaSets of the [[Pods]] deployed: 

```
$ kubectl get rs
```

