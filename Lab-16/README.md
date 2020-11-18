## Lab 16. Create a emptyDir volume for two containers in a pod
___

This lab will create a emptyDir volume in which both containers inside the pod can mount in their local directory and share data with other containers in the same pod.

* create a yaml file that defines two containers, one emptydir volume and both containers mount the volume to its local directory

pod_with_2containers_volume.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: podwithvolumes
spec:
      containers:
      - name: busyboxcontainer
        image: busybox
        command: ['sh', '-c', 'echo "Hello, Kubernetes!" && sleep 3600']
        volumeMounts:
        - mountPath: /shareddir
          name: share-volume

      - name: redis
        image: redis
        volumeMounts:
        - mountPath: /shareddir
          name: share-volume

      volumes:
      - name: share-volume
        emptyDir: {}
```

* create the pod

```bash
kubectl create -f pod_with_2containers_emptydir.yaml
kubectl get pod/podwithvolumes -o wide
```

* login to the busybox container and create a file inside the /shareddir folder.

```bash
kubectl exec -it podwithvolumes -c busyboxcontainer sh
cd /shareddir
echo "I created this content in the busy container!" > data.txt
cat data.txt
exit
```

* Now login to the redis container in your pod and confirm that the data.txt file just created is availble there too.

```bash
kubectl exec -it podwithvolumes -c redis sh
cd /shareddir
ls
cat data.txt
exit
```
> Question: What will happen to the data if the pod is stopped or deleted?
