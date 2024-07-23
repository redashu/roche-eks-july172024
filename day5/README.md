# Intro to container security 

<img src="sec1.png">

## kubearmor github profile 

[click_here](https://github.com/kubearmor/KubeArmor)

### creating pod and  checking ops

```
[ashu@roche-client kubearmor-test]$ kubectl  run ashupod1 --image=nginx --port 80 
pod/ashupod1 created
[ashu@roche-client kubearmor-test]$ kubectl  get po 
NAME       READY   STATUS    RESTARTS   AGE
ashupod1   1/1     Running   0          6s
[ashu@roche-client kubearmor-test]$ kubectl  exec -it  ashupod1 -- bash 
root@ashupod1:/# cd /usr/share/nginx/html/
root@ashupod1:/usr/share/nginx/html# ls
50x.html  index.html
root@ashupod1:/usr/share/nginx/html# rm index.html 
root@ashupod1:/usr/share/nginx/html# ls
50x.html
root@ashupod1:/usr/share/nginx/html# apt udpate
E: Invalid operation udpate
root@ashupod1:/usr/share/nginx/html# apt update
Get:1 http://deb.debian.org/debian bookworm InRelease [151 kB]
Get:2 http://deb.debian.org/debian bookworm-updates InRelease [55.4 kB]
Get:3 http://deb.debian.org/debian-security bookworm-security InRelease [48.0 kB]
Get:4 http://deb.debian.org/debian bookworm/main amd64 Packages [8788 kB]
Get:5 http://deb.debian.org/debian bookworm-updates/main amd64 Packages [13.8 kB]
Get:6 http://deb.debian.org/debian-security bookworm-security/main amd64 Packages [169 kB]
Fetched 9225 kB in 1s (6632 kB/s)                         
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
4 packages can be upgraded. Run 'apt list --upgradable' to see them.
root@ashupod1:/usr/share/nginx/html# 
```

### policy yaml

```
apiVersion: security.kubearmor.com/v1
kind: KubeArmorPolicy
metadata:
  name: ashu-pod-armor-policy
spec:
  selector:
    matchLabels: # matching label of pod here
      run: ashupod1 
  process:
    matchPaths:
    - path: /usr/bin/apt
    - path: /usr/bin/apt-get
  action:
    Block
```

### apply 

```
kubectl create -f kubearm.yaml 
kubearmorpolicy.security.kubearmor.com/ashu-pod-armor-policy created
[ashu@roche-client kubearmor-test]$ kubectl  get  KubeArmorPolicy
NAME                    AGE
ashu-pod-armor-policy   14s
[ashu@roche-client kubearmor-test]$ 

```



