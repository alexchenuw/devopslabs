## Lab 17. create a configmap then use it in a pod
___

> create a configmap
cat lab17_configmap.yaml
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
```
kubectl create -f lab17_configmap.yaml
```

> create a pod that uses the configmap data

cat pod_use_configmap.yaml
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
```
kubectl create -f pod_use_configmap.yaml
```
* log into the pod/container to verify if the variables are passed into:

```
kubectl exec -it configmap-game sh

echo $PLAYER_INIT_GOLD

echo $PLAYER_INIT_LIVES
```


## optional lab: create a secrets and use it on a pod

> create a secrets
```
kubectl create secret generic mycredential --from-literal=username=alex --from-literal=password=abc123
```
* show and inspect the secrets
```
kubectl get secrets mycredential
```
> create a pod that uses the secrets

cat pod_usesecret_vol.yaml
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

* create the pod and login to the container

```
kubectl create -f pod_usesecret_vol.yaml 
kubectl exec -it podwithsecretvolume sh
```
* check the vol directory, you should see the username and password are sved as two files there.

```
cd /home/mykey
cat username
cat password
````



