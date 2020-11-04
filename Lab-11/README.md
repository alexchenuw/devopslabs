## Lab 11. Create a two container pod using YAML
___

* Now we are going to create a yaml file called **multi-pod.yaml** to define a pod with two containers. Be sure to use your netID as part of the pod name so it does not conflict with others instances in the shared kubernetes cluster.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: $USER-podwith2containers
spec:
      containers:
      - name: busyboxcontainer
        image: busybox
        command: ['sh', '-c', 'echo "Hello, Kubernetes!" && sleep 3600']

      - name: redis
        image: redis
```
* create the pod with your yaml file

```bash
kubectl create -f multi-pod.yaml
```

* run some pod related command to inspect pod information

```bash
kubectl get pods
kubect get pods $USER-podwith2containers
kubectl describe pod $USER-podwith2containers
```

* Now we log in to the pod directly and spawn a shell

```bash
kubectl exec -it $USER-podwith2containers sh
```
_did you get an error message trying to run the interactive with a pod? what was the issue?_

_it is because, when there are more than one container in a pod, you need -c to specify which container you want to run into, or you will run into the default (first) container in the pod._

```bash
kubectl exec -it $USER-podwith2containers -c redis sh
exit
kubectl exec -it $USER-podwith2containers -c busyboxcontainer sh
```
