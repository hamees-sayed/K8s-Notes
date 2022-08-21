ConfigMaps are Kubernetes objects that allow you to separate configuration data/files from the services to keep containerized applications portable.   

![img](https://imgur.com/e08wbSi.png)

ConfigMaps bind configuration files, command-line arguments, surroundings variables, port numbers, and alternative configuration artifacts to your Pods containers and system parts at run-time.   

Let's create a configMap: To create a configMap, we write a Pod `spec` that refers to a ConfigMap and configures the container(s) in that Pod based on the data in the ConfigMap.  

```
$ mkdir configmap-example # we have sample files in this dir to generate configMap

$ kubectl create configmap game-config-example --from-file=configmap-example/

$ kubectl get configmaps game-config-example -o yaml
```

Now, there might be other scenarios where you have to store your credentials and passwords. Storing all those credentials in ConfigMap is not favourable.  

Here's where another component namely “[[Secrets]]” comes into play.

