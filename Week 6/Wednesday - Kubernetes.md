**Kubernetes -** Greek for *helmsmen* 

It was a Google project that they open-sourced, and put on AWS.

**Pods** go within **Clusters**, ... **Node**

## Control-Side
**API** - Cental hub for communications - all data goes through it.
 - It's an HTTPS endpoint - so we need a public/private key.
 - We have a client that then contacts the API - **exposing the API is done through Kubectl**
**Controller Manager** - The "brains" of the control-side.
 - Manages the statefulness - for example, if we expect 2 pods to be available, CM will add another. 
	 - It keeps track of all of this information through **etcd**
**etcd** - A database for keeping track of control-side information (CHECK THIS)
**Scheduler** - Schedules pods.

*All of the above components connect via the API*

## Data-Side
**Node**
 - Has a part called a **Kubelet**
	 - A process running on the node - manages control plane services.
	 - Sends communications from itself to the **engine**
 - **Container Runtime Engine**
**CoreDNS** - As containers/pods come up and go down, their IP addresses change a lot.
 - We use the DNS names instead for this reason.

All of the data side is being contained with **containerd**

![](../Images/Pasted%20image%2020240814092623.png)

---

`kubectl version`
https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

![](../Images/Pasted%20image%2020240814094232.png)
The * means we are on that context
 - If it's on another one, use `kubectl config use-context ...`

![](../Images/Pasted%20image%2020240814094335.png)

Note that there are playgrounds at killercoda.com/playgrounds/scenarios/kubernetes

![](../Images/Pasted%20image%2020240814095124.png)

**Q: Where does Kubernetes get the image to run the container?**

![](../Images/Pasted%20image%2020240814095223.png)

`kubectl api-resources`

Note that NAMESPACED is a logical separation - not a hard separation.

`kubectl run nginx --image nginx`
Note that when it doesn't have the image, it'll pull one from Docker Hub.
![](../Images/Pasted%20image%2020240814095935.png)

---

So we have Bob, who has his own computer (a client), and he's trying to communicate with our Kubernetes cluster. He wants to access a website we're hosting in DNS.

We have our own DNS internally, but there's a DNS for the wider internet that requires registrars through an ISP. We have a "service" within our cluster, which connects to our pods - the service knowing where that pod is via a **label**, connecting through a port - **this is all done through CoreDNS.** (Thankfully, this part is abstracted away from us -- it should just work.)

`kubectl expose pod nginx --port 80 --target-port 80 --type LoadBalancer`
![](../Images/Pasted%20image%2020240814102543.png)

If we navigate to localhost:80, we should see a nginx demo page. 

---

https://kubernetes.io/docs/concepts/workloads/pods/

Make a new folder, called Kubernetes
Make a file called `pod.yaml`, enter this from the above link:
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```

Node that the `spec` is the specification for the pod. Containers/pods are a 1:1 relationship. (CHECK THIS)

In the console:
`kubectl create -f .\pod.yaml`
`kubectl apply -f .\pod.yaml`
`kubectl delete pod nginx`

Now, make a new file - `deployment.yaml` - with this content:
```
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment
  labels:
    app: nginx
    
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
        
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

The first `spec` is for the deployment specification, while the second one is for the pod.

Note that the spec from the pod is contained within the spec for the deployment - 

`kubectl apply -f .\deployment.yaml`
`kubectl get deployments`

![](../Images/Pasted%20image%2020240814105028.png)

These 3 pods we have created are identical.

`kubectl describe deployments` will show all of the information for the pods, their events, etc.
`kubectl get all -A`

Note the `replicaset`s at the bottom - we have a "desired", "current", and "ready" count for the pods.

Note that the name will be different when you have a deployment, they'll have different hashes appended to the end of the name, since they can't be identical.

Also note that if you kill a pod, since it is self-healing, it'll create a new pod to help pick it back up.

![](../Images/Pasted%20image%2020240814105420.png)

Deployments are **stateless applications**

Deployments will have multiple sets of itself - and let's say we had a database connected to some type of storage.
 - Because we had pods with names that changed all the time, it'll get hard to track specifically what pod is accessing what resources.
 - Having every pod have it's own access to the DB would therefore become really hard, and could cause all sorts of corruption issues.

We can then have a **Stateful Set**
 - Each pod has it's own **persistent volume**, which connects to a storage class.
 - Each pod will also lose the random hash - and instead have a number.
	 - Each time the pod is relaunched, it'll retain the number.
 - Pod 0 will only access persistent volume 1, but each PV will copy the changes instantaneously to the other PVs, which the other pods can only read.
![](../Images/Pasted%20image%2020240814110227.png)
 - If pod 0 fails, another pod will be promoted to read/write access as pod 0, and the newly generated pod will be added to the list.
	 - If all pods failed, the PVs will just hang on until they come back up - they're independent of the pod for data storage purposes.

Make a new file - `statefulset.yaml`
https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/
```
apiVersion: v1
kind: Service
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  ports:
  - port: 80
    name: web
  clusterIP: None
  selector:
    app: nginx

apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  selector:
    matchLabels:
      app: nginx # has to match .spec.template.metadata.labels
  serviceName: "nginx"
  replicas: 3 # by default is 1
  minReadySeconds: 10 # by default is 0
  template:
    metadata:
      labels:
        app: nginx # has to match .spec.selector.matchLabels
    spec:
      terminationGracePeriodSeconds: 10
      containers:
      - name: nginx
        image: registry.k8s.io/nginx-slim:0.24
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: nginx
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: nginx
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: "hostpath"
      resources:
        requests:
          storage: 1Gi
```

If we run `kubectl get sc`, we'll see the Docker's storage path.

`kubectl apply -f .\statefulset.yaml`

![](../Images/Pasted%20image%2020240814111134.png)

Make a new file - `config.yaml`
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: configmap-demo
data:
  player_initial_lives: "3"
  ui_properties_file_name: "user-interface.properties"
```

`kubectl apply -f .\config.yaml`

New file - `secret.yaml`

```
apiVersion: v1
kind: Secret
metadata:
  name: dotfile-secret
data:
  .secret-file: dmFsdWUtMg0KDQo=
```

^ NOTE THAT I AM MISSING SOME STEPS HE WENT SO FAST LOL
tldr he did something involving generating a base64 key, he's setting those keys in `deployment.yaml` below:

Update `deployment.yaml:`

```
apiVersion: apps/v1
kind: Deployment #Stateless applications

metadata:
  name: nginx-deployment
  labels:
    app: nginx

spec: #Deployment
  replicas: 5
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx

    spec: #Pod 
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
        env:


        - name: KEY1
          valueFrom:
            configMapKeyRef:
              name: configmap-demo
              key: ui_properties_file_name
        - name: KEY2
          valueFrom:
            configMapKeyRef:
              name: configmap-demo
              key: player_initial_lives


        - name: USERNAME
          valueFrom:
            secretKeyRef:
              name: dotfile-secret
              key: username
        - name: PASSWORD
          valueFrom:
            secretKeyRef:
              name: dotfile-secret
              key: password
      #   volumeMounts:
      #     - name: config-volume
      #       mountPath: /etc/config
      # volumes:
      #   - name: config-volume
      #     configMap:
      #       name: configmap-demo
```

To restart the deployment  - `kubectl rollout restart deployment nginx-deployment`

`kubectl exec -it nginx-deployment-<hash value> -- /bin/bash`
Within here, we can do `echo KEY1` to ensure that our properties have been injected properly.

---

**Project 2 is going to likely use AWS Elastic Beanstalk**
***Project 3 WILL use Kubernetes***

We may have to use Eureka to manage Kubernetes with Java?