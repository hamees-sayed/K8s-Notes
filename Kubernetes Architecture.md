Kubernetes consists of two things: Master Node and Worker Node.  
Nodes are physical servers on which application services are created. Master Node and Worker Node combining everything creates a K8s cluster.   

![img](https://i.imgur.com/kUAIzCq.png)


**Worker Nodes**: Your applications are deployed on worker nodes, all worker nodes have a kubelet. Kubelet is basically a node agent that runs on each node in the cluster. It's role is to constantly communicate with the master node. So if there is any change in the architecture then kubelet is responsible to do those changes and forward them to the master node.   


**Master Nodes**: The components of master nodes are as follows; 

- API Server : API server is the front end for the kubernetes control plane and is responsible to pass on the all the information to the kubernetes cluster. So whenever we want to interact with k8s, API server comes into picture. There are three ways of connecting to the API server as follows - UI, CLI or API.

- Controller Manager : Controller managers keeps tracks of what is happening in the k8s cluster. Control manager is divided into 4 different components, namely: 
		- Node Controller
		- Replication Controller
		- Endpoints Controller
		- Service accound and Token controller  

- Scheduler : Scheduler is responsible for pod placement. Suppose from api server you created a request to deploy the web application to the k8s cluster so scheduler is responsible to determine on which nodes should the application pods be placed withing the cluster.  

- etcd : etcd key value store is the most important component in k8s cluster. Etcd key value stores the entire data of the k8s cluster. 


So how do Master node, Worker node and all their different components work together? The answer is an internal “Virtual Network”.

![Imgur](https://imgur.com/fk9TTby.png)


This is what a typical Kubernetes work flow looks like: 

Master Node -> Worker Nodes -> [[Pods]] -> [[Service]] -> [[Ingress]] -> [[ConfigMap]] -> [[Secrets]] -> [[Volumes]] -> [[ReplicaSet]] 
