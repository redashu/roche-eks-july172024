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

### to create service make sure pod is having label 

```
[ashu@roche-client k8s-resources]$ kubectl   get pods  ashupodweb  --show-labels
NAME         READY   STATUS    RESTARTS   AGE   LABELS
ashupodweb   1/1     Running   0          84m   run=ashupodweb
[ashu@roche-client k8s-resources]$ kubectl   get pods   --show-labels
NAME           READY   STATUS    RESTARTS   AGE   LABELS
amitpod1       1/1     Running   0          83m   run=amitpod1
amitvpodweb    1/1     Running   0          84m   run=amitvpodweb
anipodweb      1/1     Running   0          84m   run=anipodweb
ashupodweb     1/1     Running   0          85m   run=ashupodweb
dppodweb       1/1     Running   0          84m   run=dppodweb
gauripodweb    1/1     Running   0          84m   run=gauripodweb
inayatweb      1/1     Running   0          84m   run=inayatweb
kdpodweb       1/1     Running   0          84m   run=kdpodweb
kudduspodweb   1/1     Running   0          84m   run=kudduspodweb
mg-nginx       1/1     Running   0          83m   run=mg-nginx
rajeshpodweb   1/1     Running   0          82m   run=rajeshpodweb
rajpodweb      1/1     Running   0          81m   run=rajpodweb
riyapodweb     1/1     Running   0          82m   run=riyapodweb
sanpodweb      1/1     Running   0          82m   run=sanpodweb
shobhitweb     1/1     Running   0          82m   run=shobhitweb
[ashu@roche-client k8s-resources]$ 

```

### we can change label in a running pod also 

```
[ashu@roche-client k8s-resources]$ kubectl  apply -f day2pod.yaml 
Warning: resource pods/ashupodweb is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
pod/ashupodweb configured
[ashu@roche-client k8s-resources]$ 
[ashu@roche-client k8s-resources]$ kubectl   get pods  ashupodweb  --show-labels
NAME         READY   STATUS    RESTARTS   AGE   LABELS
ashupodweb   1/1     Running   0          87m   run=ashupodweb,x1=helloashu
[ashu@roche-client k8s-resources]$ 

```
### creating service manifest 

```
[ashu@roche-client k8s-resources]$ kubectl   create  service
Create a service using a specified subcommand.

Aliases:
service, svc

Available Commands:
  clusterip      Create a ClusterIP service
  externalname   Create an ExternalName service
  loadbalancer   Create a LoadBalancer service
  nodeport       Create a NodePort service

Usage:
  kubectl create service [flags] [options]

Use "kubectl create service <command> --help" for more information about a given command.
Use "kubectl options" for a list of global command-line options (applies to all commands).


[ashu@roche-client k8s-resources]$ kubectl   create  service  loadbalancer  ashulb1   --tcp  80:80  --dry-run=client -o yaml
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: ashulb1
  name: ashulb1
```

### checking service status

```
ashu@roche-client k8s-resources]$ kubectl   create  -f ashuinternal_lb.yaml 
service/ashulb1 created
[ashu@roche-client k8s-resources]$ kubectl   get  service 
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP                                                              PORT(S)        AGE
amitlb1      LoadBalancer   10.100.136.63   <pending>                                                                80:31042/TCP   1s
ashulb1      LoadBalancer   10.100.50.192   a896c5766f97b4601b98ff7bce4dab2f-449321438.us-east-1.elb.amazonaws.com   80:31446/TCP   10s
kubernetes   ClusterIP      10.100.0.1      <none>                                    
                               443/TCP        3h57m


[ashu@roche-client k8s-resources]$ 
[ashu@roche-client k8s-resources]$ kubectl   get  endpoints  ashulb1  
NAME      ENDPOINTS   AGE
ashulb1   <none>      2m13s
[ashu@roche-client k8s-resources]$ 

```

### updating svc selector 

```
kubectl  replace  -f  ashuinternal_lb.yaml 
service/ashulb1 replaced
[ashu@roche-client k8s-resources]$ kubectl   get  service ashulb1 -o wide
NAME      TYPE           CLUSTER-IP      EXTERNAL-IP                                                              PORT(S)        AGE    SELECTOR
ashulb1   LoadBalancer   10.100.50.192   a896c5766f97b4601b98ff7bce4dab2f-449321438.us-east-1.elb.amazonaws.com   80:31446/TCP   6m7s   run=ashupodweb,x1=helloashu
[ashu@roche-client k8s-resources]$ kubectl   get  endpoints  ashulb1  
NAME      ENDPOINTS          AGE
ashulb1   192.168.47.51:80   6m12s
[ashu@roche-client k8s-resources]$ 

[ashu@roche-client k8s-resources]$ kubectl   get  pods ashupodweb -o wide
NAME         READY   STATUS    RESTARTS   AGE    IP              NODE                             NOMINATED NODE   READINESS GATES
ashupodweb   1/1     Running   0          105m   192.168.47.51   ip-192-168-62-198.ec2.internal   <none>           <none>
[ashu@roche-client k8s-resources]$ 



```

### understanding k8s controller 

<img src="ctr.png">

### checking api resources in k8s 

```
humanfirmware@darwin  ~/Desktop/Tranings  kubectl   api-resources 
NAME                              SHORTNAMES   APIVERSION                        NAMESPACED   KIND
bindings                                       v1                                true         Binding
componentstatuses                 cs           v1                                false        ComponentStatus
configmaps                        cm           v1                                true         ConfigMap
endpoints                         ep           v1                                true         Endpoints
events                            ev           v1                                true         Event
limitranges                       limits       v1                                true         LimitRange
namespaces                        ns           v1                                false        Namespace
nodes                             no           v1                                false        Node
persistentvolumeclaims            pvc          v1                                true         PersistentVolumeClaim
persistentvolumes                 pv           v1                                false        PersistentVolume
pods                              po           v1                                true         Pod
podtemplates                                   v1                                true         PodTemplate
replicationcontrollers            rc           v1                                true         ReplicationController
resourcequotas                    quota        v1                                true         ResourceQuota
secrets                                        v1                                true         Secret
serviceaccounts                   sa           v1                                true         ServiceAccount
services                          svc          v1                                true         Service
mutatingwebhookconfigurations                  admissionregistration.k8s.io/v1   false        MutatingWebhookConfiguration
validatingwebhookconfigurations                admissionregistration.k8s.io/v1   false        ValidatingWebhookConfiguration
customresourcedefinitions         crd,crds     apiextensions.k8s.io/v1           false        CustomResourceDefinition
apiservices                                    apiregistration.k8s.io/v1         false        APIService
controllerrevisions                            apps/v1                           true         ControllerRevision
daemonsets                        ds           apps/v1                           true         DaemonSet
deployments                       deploy       apps/v1                           true         Deployment
replicasets                       rs           apps/v1                           true         ReplicaSet
statefulsets                      sts          apps/v1                           true         StatefulSet

```
### Creating deployment manifest 

```

[ashu@roche-client k8s-resources]$ kubectl   create  deployment  ashu-deploy  --image=docker.io/dockerashu/ashuroche:nginxappv1 --port 80 --dry-run=client  -o yaml   >deploy1.yaml 
```

### creating 

```
kubectl  create -f deploy1.yaml 
deployment.apps/ashu-deploy created
[ashu@roche-client k8s-resources]$ kubectl   get  deploy
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
ashu-deploy   1/1     1            1           5s
dp-deploy     1/1     1            1           2m16s
mg-deploy     1/1     1            1           6s
[ashu@roche-client k8s-resources]$ kubectl   get  rs
NAME                      DESIRED   CURRENT   READY   AGE
ashu-deploy-56bbcb766d    1         1         1       18s
dp-deploy-66df65c6f       2         2         2       2m29s
kuddusdeploy-5bb478dcb8   1         1         1       6s
mg-deploy-6dd8cfd69c      1         1         1       19s
[ashu@roche-client k8s-resources]$ kubectl   get  pod
NAME                            READY   STATUS              RESTARTS   AGE
ashu-deploy-56bbcb766d-qcv5w    1/1     Running             0          23s
dp-deploy-66df65c6f-55phd       1/1     Running             0          2m34s
dp-deploy-66df65c6f-lvkmx       1/1     Running             0          11s
kuddusdeploy-5bb478dcb8-bhpjd   1/1     Running             0          11s
mg-deploy-6dd8cfd69c-bb7jp      1/1     Running             0          24s
rajesh-deploy-d894bf668-n7rrs   0/1     ContainerCreating   0          1s
```

### creating service using expose 

```
kubectl  expose  deployment  ashu-deploy   --type LoadBalancer --port 80 --name ashulb2  --dry-run=client -o yaml  >svc2.yaml 
```

