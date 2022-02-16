Issue #1:
ERROR: Warning  FailedCreate  14m (x832 over 9d)  statefulset-controller  create Pod couture-nifi-zookeeper-0 in StatefulSet couture-nifi-zookeeper failed error: failed to create PVC data-couture-nifi-zookeeper-0: persistentvolumeclaims "data-couture-nifi-zookeeper-0" is forbidden: Internal error occurred: 2 default StorageClasses were found
REASON: Volume is not being binded
SOLUTION: Statefulset => 
```
$ kubectl get sc
- Use "efs-sc"
change in values.yaml -> 
from storageClass: "-" to:
storageClass: "efs-sc"
```


Issue #2:
ERROR: chown: changing ownership of '/var/lib/cassandra': Operation not permitted
SOLUTION: enable securityContext in values.yaml which is being used in statefulset.yaml
```
securityContext:
  enabled: true
```
