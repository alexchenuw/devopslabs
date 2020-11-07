## Lab 18. create an init container and a liveness container for a pod
___

> ### Create an init container for a pod

_Have the init container perform an operation, until the return is successful, continue to create the other containers in the same pod.
the init container will first download a webpage from a repository and place it at a shared dir, once it completes that, the web server container will be spun up._

cat lab_init_container.yaml
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
    - http://www.google.com
    volumeMounts:
    - name: workdir
      mountPath: "/work-dir"
  dnsPolicy: Default
  volumes:
  - name: workdir
    emptyDir: {}
``` 


> ### Create a liveness container for a pod

> liveness container

cat liveness_container.yaml
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
