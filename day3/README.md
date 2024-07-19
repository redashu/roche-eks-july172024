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

### pushing iamge to ECR 

```
[ashu@roche-client ashu-pythonfask]$ docker  images  | grep ashu
ashuflask                  appv1     435703f8778b   15 minutes ago   315MB
[ashu@roche-client ashu-pythonfask]$ 
[ashu@roche-client ashu-pythonfask]$ 
[ashu@roche-client ashu-pythonfask]$ 
[ashu@roche-client ashu-pythonfask]$ docker   tag   ashuflask:appv1   public.ecr.aws/h7s5d3t1/rocheflask:ashuappv1   
[ashu@roche-client ashu-pythonfask]$ 


====
aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/h7s5d3t1
WARNING! Your password will be stored unencrypted in /home/ashu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
[ashu@roche-client ashu-pythonfask]$ docker push public.ecr.aws/h7s5d3t1/rocheflask:ashuappv1
The push refers to repository [public.ecr.aws/h7s5d3t1/rocheflask]
aee9de48b79b: Pushed 
7619ced1a792: Pushed 
9ce4f9c24974: Pushed 
8678a8b5654d: Layer already exists 
a58d16c447ed: Layer already exists 
b88d8bda5e53: Layer already exists 
8cddf1d30fbd: Layer already exists 
b9fc95825e61: Layer already exists 
32148f9f6c5a: Layer already exists 
ashuappv1: digest: sha256:01f404f7b642156221877ea2400dd68077ae3d72a74394ce2439eb28b74650ce size: 2203
[ashu@roche-client ashu-pythonfask]$ docker logout  public.ecr.aws
Removing login credentials for public.ecr.aws
[ashu@roche-client ashu-pythonfask]$ 

```

### deployment vs statefulsets

<img src="state.png">

## Db deployemnt as single pod 

### creating deployment 

```
 kubectl   create  deployment  ashu-db --image=mysql:8.0 --port 3306  --dry-run=client -o yaml >db.yaml 
[ashu@roche-client ashu-pythonfask]$ 

```
### understanding secrets in k8s 

<img src="sec.png">

### creating secret

```
 kubectl  create secret 
Create a secret with specified type.

 A docker-registry type secret is for accessing a container registry.

 A generic type secret indicate an Opaque secret type.

 A tls type secret holds TLS certificate and its associated key.

Available Commands:
  docker-registry   Create a secret for use with a Docker registry
  generic           Create a secret from a local file, directory, or literal value
  tls               Create a TLS secret
```

### crewating 

```
kubectl  create secret   generic  ashudb-root-cred  --from-literal  ashurootKey="AshuExample@12345"  --dry-run=client -o yaml  >rootcred.yaml 
[ashu@roche-client ashu-pythonfask]$ 
[ashu@roche-client ashu-pythonfask]$ kubectl create -f rootcred.yaml 
secret/ashudb-root-cred created
[ashu@roche-client ashu-pythonfask]$ kubectl  get secrets
NAME               TYPE     DATA   AGE
ashudb-root-cred   Opaque   1      4s
[ashu@roche-client ashu-pythonfask]$ 

```