## Understanding container runtime engine and os / arch 

<img src="cre1.png">

### checking docker client and server details

```
[ashu@roche-client ~]$ docker  version  
Client:
 Version:           25.0.3
 API version:       1.44
 Go version:        go1.20.12
 Git commit:        4debf41
 Built:             Mon Feb 12 00:00:00 2024
 OS/Arch:           linux/amd64
 Context:           default

Server:
 Engine:
  Version:          25.0.3
  API version:      1.44 (minimum version 1.24)
  Go version:       go1.20.12
  Git commit:       f417435
  Built:            Mon Feb 12 00:00:00 2024
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.7.11
  GitCommit:        64b8a811b07ba6288238eefc14d898ee0b5b99ba
 runc:
  Version:          1.1.11
  GitCommit:        4bccb38cc9cf198d52bebf2b3a90cd14e7af8c06
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0

```

### creating a directory strucuter

```
[ashu@roche-client ~]$ mkdir  -p ashu-project/{javaapp,pythonapp,webapp}
[ashu@roche-client ~]$ ls
ashu-project
[ashu@roche-client ~]$ ls  ashu-project/
javaapp  pythonapp  webapp
[ashu@roche-client ~]$ 


```

