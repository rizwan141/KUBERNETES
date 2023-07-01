```
aws ec2 create-volume \
    --volume-type gp2 \
    --size 80 \
    --availability-zone us-east-1a
```

### pv.yaml
```yml
kind: PersistentVolume
apiVersion: v1
metadata:
    name: test-pv
spec:
    accessModes: [ "ReadWriteOnce" ]
    capacity:
     storage: 5Gi
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
  name: test-pod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: test
  volumes:
    - name: test
      persistentVolumeClaim:
        claimName: test-pvc
```
