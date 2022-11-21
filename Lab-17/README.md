## Lab 17. create a configmap then use it in a pod
___

> create a configmap file called `player_configmap.yaml`

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mygamedata
data:
  player_initial_lives: "3"
  player_initial_gold: "10000"
```

create the configmap

```bash
kubectl create -f player_configmap.yaml
kubectl get configmaps
kubectl describe configmaps mygamedata
```

Now create a pod that uses the configmap data called `player_configmap_pod.yaml` 
> Note: This pod definition references data values defined in the previous configmap.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: configmap-game
spec:
  containers:
    - name: nginx
      image: nginx
      env:
        - name: PLAYER_INIT_LIVES 
          valueFrom:
            configMapKeyRef:
              name: mygamedata       
              key: player_initial_lives
        - name: PLAYER_INIT_GOLD 
          valueFrom:
            configMapKeyRef:
              name: mygamedata      
              key: player_initial_gold
```

* create the pod with kubectl

```bash
kubectl create -f player_configmap_pod.yaml
kubectl get pod/configmap-game -o wide
```
* log into the pod/container to verify if the variables have been passed into the containers.

```
kubectl exec -it configmap-game sh
echo $PLAYER_INIT_GOLD
echo $PLAYER_INIT_LIVES
```

## optional lab: create a secrets for use with a pod

First create a secret

```bash
kubectl create secret generic mycredential --from-literal=username=uwUberDevOp --from-literal=password=abc123
```
* show and inspect the secrets
```
kubectl get secrets mycredential
kubectl describe secrets mycredential
```

Create a new file called `pod_usesecret_vol.yaml` to create a pod that uses the secrets 

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: podwithsecretvolume
spec:
      containers:
      - name: nginx
        image: nginx
        volumeMounts:
        - mountPath: /home/mykey
          name: share-volume

      volumes:
      - name: share-volume
        secret:
          secretName: mycredential
```

Now create the pod and check the status

```bash
kubectl create -f pod_usesecret_vol.yaml
kubectl get pod podwithsecretvolume -o wide
kubectl describe pod podwithsecretvolume

```
Finally login to the container and check the vol directory, you should see the username and password are sved as two files there.

```bash
kubectl exec -it podwithsecretvolume sh
cd /home/mykey
cat username
cat password
exit
````

> Question: Why did we not have to define a container when logging into the podwithsecretvolume container?



