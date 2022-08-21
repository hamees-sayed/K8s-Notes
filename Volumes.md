In Kubernetes, a volume can be thought of as a directory which is accessible to the containers in a pod. We have different types of volumes in Kubernetes and the type defines how the volume is created and its content.   

![img](https://img-blog.csdnimg.cn/20210616220302300.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1JhbmNoZXJMYWJz,size_16,color_FFFFFF,t_70)

You can use kubernetes volumes to persist the data beyond pod lifecycle. Volumes are simpy physcial storage drives ike hdd and ssd.  

There are mainly two types of volumes: 

- **Local Volume(Inside Cluster)** : A local volume is a mounted local storage device such as a disk, partition or directory. Local volumes can only be used as a statically created PersistentVolume.   

- **Remote Volume(Outside Cluster)** : You can create volume in any cloud provider and attach those volumes to the k8s cluster.   

Let's write persistent volume: File name = `persistent-volume.yaml`

```
apiVersion: v1
kind: PersistenVolume
metadata:
	name: pv1
	labels:
		type: local
spec:
	capacity:
		storage: 5Gi  //5 gb volume
	accessModes:
		- ReadWriteOnce
		hostPath: 
			path: "/tmp/data"
```

To create the persistent volume, type: 
```
$ kubectl create -f persistent-volume.yaml
```



In any case, consider that your main application pod is deleted and a new pod is created, new pod will take some time to be created. Meanwhile the user won't be able to access the application. To solve this problem, “[[ReplicaSet]]” is another component.