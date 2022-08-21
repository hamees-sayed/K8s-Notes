Secrets can be defined as Kubernetes objects used to store sensitive data such as user name and passwords in base64 encoded format. 

![img](https://images.prismic.io/macstadium/7278f809-5d29-40c1-941b-8c47ef1692a4_Kubernetes+secrets+diagram.png?auto=compress,format)

- This is how we create a secret from yaml file: File name = `secrets.yaml`

```
apiVersion: v1
kind: Secret
metadata:
	name: tomcat-pass
	type: Opaque
	data: 
		password: <user password>
		username: <user name>
```

```
$ kubectl create -f secrets.yaml
secrets/tomcat-pass
```


- In order to us the secret as environment variable, we will use **env** under the spec section of pod yaml file.  

```
env:
- name: SECRET_USERNAME
	valueFrom: 
		secretKeyRef: 
			name: mysecret
			key: tomcat-pass
```

We have already learnt that whenever there's an issue in the database, the db pod dies and newly created pod is created to replace the older pod. So along with the old pod the data stored in it is also deleted but that's not what we want, we have to save the data and pass it onto the new pod. To achieve this we have another component named “[[Volumes]]”.