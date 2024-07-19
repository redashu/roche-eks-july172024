### k8s Revision 

<img src="rev1.png">

### enable tab feature in kubectl 

```
[ashu@roche-client ashu-project]$ vim  ~/.bashrc   ^C
[ashu@roche-client ashu-project]$ 
[ashu@roche-client ashu-project]$ tail -2  ~/.bashrc 
unset rc
source <(kubectl completion bash)
[ashu@roche-client ashu-project]$ 
[ashu@roche-client ashu-project]$ source ~/.bashrc 
[ashu@roche-client ashu-project]$ 
[ashu@roche-client ashu-project]$ kubectl  get p
persistentvolumeclaims                                    policyendpoints.networking.k8s.aws
persistentvolumes                                         priorityclasses.scheduling.k8s.io
poddisruptionbudgets.policy                               prioritylevelconfigurations.flowcontrol.apiserver.k8s.io
podmonitors.monitoring.coreos.com                         probes.monitoring.coreos.com
pods                                                      prometheusagents.monitoring.coreos.com
pods.metrics.k8s.io                                       prometheuses.monitoring.coreos.com
podtemplates                                              prometheusrules.monitoring.coreos.com
[ashu@roche-client ashu-project]$ kubectl  get pod
No resources found in ashu-app namespace.
[ashu@roche-client ashu-project]$ kubectl config get-contexts 
CURRENT   NAME                                         CLUSTER                                  AUTHINFO                                     NAMESPACE
*         eks@delvex-cluster-new.us-east-1.eksctl.io   delvex-cluster-new.us-east-1.eksctl.io   eks@delvex-cluster-new.us-east-1.eksctl.io   ashu-app
[ashu@roche-client ashu-project]$ 

```

### Deploy two teir webapp

<img src="webapp1.png">

### flask directory structure 

```
tree  ashu-pythonfask/
ashu-pythonfask/
├── Dockerfile
├── app.py
├── compose.yaml
└── templates
    ├── index.html
    └── success.html

1 directory, 5 files
```