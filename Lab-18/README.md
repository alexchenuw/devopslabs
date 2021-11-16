## Lab 18. create an init container and a liveness container for a pod
___

> ### Create an init container for a pod

_Have the init container perform an operation, until the return is successful, continue to create the other containers in the same pod.
the init container will first download a webpage from a repository and place it at a shared dir, once it completes that, the web server container will be spun up._

Create a file called `lab_init_container.yaml` with the following content.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-demo
  labels:
     disk: ssd
spec:
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: workdir
      mountPath: /usr/share/nginx/html
  initContainers:
  - name: install
    image: busybox
    command:
    - wget
    - "-O"
    - "/work-dir/index.html"
    - https://github.com/alexchenuw/devopslabs/blob/main/Lab-18/index.html
    volumeMounts:
    - name: workdir
      mountPath: "/work-dir"
  dnsPolicy: Default
  volumes:
  - name: workdir
    emptyDir: {}
``` 

* create the new pod and use kubectl describe the details and check the deploying events, it should show the events in order.

```bash
kubectl create -f lab_init_container.yaml
kubectl describe pod init-demo
```

* we can also expose the pod service to find out what it is showing

```
kubectl expose pod/init-demo --type=NodePort --port=80xx --target-port=80
kubectl get svc
```
* open a browser on your local laptop and browse to http://node-public-ip:80xx, you should be able to get the webpage


> ### Create a liveness container for a pod

* create a liveness container in a pod 

create a file called `liveness_container.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    test: liveness
  name: liveness-exec
spec:
  containers:
  - name: liveness
    image: k8s.gcr.io/busybox
    args:
    - /bin/sh
    - -c
    - touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; sleep 600
    livenessProbe:
      exec:
        command:
        - cat
        - /tmp/healthy
      initialDelaySeconds: 5
      periodSeconds: 5
```

* create the pod

```bash
kubectl create -f liveness_container.yaml
```
* check the deploy events with the pod multiple times

```bash
kubectl describe pod liveness-exec
```

* show the pod and check how many times it has been restarted

```bash
kubectl get pod liveness-exec
```


