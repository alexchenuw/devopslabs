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

