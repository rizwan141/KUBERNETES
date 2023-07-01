
### pv.yaml
```yml
kind: PersistentVolume
apiVersion: v1
metadata:
    name: test-pv
spec:
    accessModes: [ "ReadWriteOnce" ]
    capacity:
     storage: 1Gi
    hostPath:
     path: /tmp/data
```

### pvc.yaml
```yml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: test-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```



### pod.yaml
```yml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
    command: ["/bin/sh", "-c"]
    args: ["while true; do shuf -i 0-100 -n 1 >> /opt/number.out; sleep 1; done"]
    volumeMounts:
    - mountPath: /opt
      name: data-volume
  volumes:
  - name: data-volume
    persistentVolumeClaim:
        claimName: test-pvc
```
