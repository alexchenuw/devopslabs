## Lab 16. Create a emptyDir volume for two containers in a pod
___

This lab is to create a emptyDir volume and containers insie a pod can mount it to its local directory to share data with other containers in the same pod

* create a yaml file that defines two containers, one emptydir volume and both containers mount the volume to its local directory

pod_with_2containers_emptydir.yaml
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
```
kubectl create -f pod_with_2containers_emptydir.yaml
```

* get into one container and create/modify files inside the /shareddir
```
kubectl exec -it podwithvolume -c busyboxcontainer sh
```
add or remove files inside /shareddir

* get into the shared directory on the other container and check if the files you created/modified showing up in the directory
```
kubectl exec -it podwithvolume -c redis sh
```
