# roche-eks-july172024

### generating pod manifest 

```
kubectl   run  ashupodweb --image=docker.io/dockerashu/ashuroche:nginxappv1 --port 80 --dry-run=client -o yaml  >day2pod.yaml 
```

### creating pod 

```
ashu@roche-client k8s-resources]$ kubectl  create -f day2pod.yaml 
pod/ashupodweb created
[ashu@roche-client k8s-resources]$ kubectl   get pods
NAME           READY   STATUS              RESTARTS   AGE
ashupodweb     1/1     Running             0          5s
kudduspodweb   0/1     ContainerCreating   0          3s
[ashu@roche-client k8s-resources]$ kubectl   get pods  ashupodweb  -o wide
NAME         READY   STATUS    RESTARTS   AGE   IP              NODE                             NOMINATED NODE   READINESS GATES
ashupodweb   1/1     Running   0          12s   192.168.47.51   ip-192-168-62-198.ec2.internal   <none>           <none>
[ashu@roche-client k8s-resources]$ 
```

### understnading using service as internal k8s lb 

<img src="svc1.png">

### understanding loadbalancer service with cloud  controlled k8s 

<img src="lb1.png">

### understandign service discovery with svc type and label

<img src="svc2.png">



