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


### docker platform mishmatch error 

```
docker run -itd --name x1  13d89941a404
WARNING: The requested image's platform (linux/arm64/v8) does not match the detected host platform (linux/amd64/v3) and no specific platform was requested
f796f7837e1b4db1e31a0d2a9afc8d4a6db2301755ee478e3a214dcb964349ab
[ashu@roche-client ashu-project]$ 
```

## app containerization

<img src="c1.png">


### taking sample code 

```
git clone https://github.com/schoolofdevops/html-sample-app.git

```

### understanding hosting platform 

<img src="host1.png">

### building iamge 

```
[ashu@roche-client ashu-project]$ ls
html-sample-app  javaapp  pythonapp  webapp
[ashu@roche-client ashu-project]$ docker  build  -t   ashunginx:appv1    html-sample-app/ 
[+] Building 0.2s (7/7) FINISHED                                                                                  docker:default
 => [internal] load build definition from Dockerfile                                                                        0.0s
 => => transferring dockerfile: 534B                                                                                        0.0s
 => [internal] load metadata for docker.io/library/nginx:latest                                                             0.0s
 => [internal] load .dockerignore                                                                                           0.0s
 => => transferring context: 134B                                                                                           0.0s
 => [internal] load build context                                                                                           0.1s
 => => transferring context: 2.05MB                                                                                         0.0s
 => [1/2] FROM docker.io/library/nginx:latest                                                                               0.0s
 => CACHED [2/2] COPY  .  /usr/share/nginx/html/                                                                            0.0s
 => exporting to image                                                                                                      0.0s
 => => exporting layers                                                                                                     0.0s
 => => writing image sha256:a03355c44409b5a02412c5038a67b867d764707995dd38552236177f70ad29f5                                0.0s
 => => naming to docker.io/library/ashunginx:appv1                                                                          0.0s
[ashu@roche-client ashu-project]$ 
```

### pushing images

<img src="push.png">

```
[ashu@roche-client ashu-project]$ docker  images |  grep ashu
ashunginx            appv1             a03355c44409   6 minutes ago       190MB
dockerashu/roche     17july            13d89941a404   About an hour ago   619MB
[ashu@roche-client ashu-project]$ 
[ashu@roche-client ashu-project]$ 
[ashu@roche-client ashu-project]$ docker  tag    ashunginx:appv1   docker.io/dockerashu/ashuroche:nginxappv1  
[ashu@roche-client ashu-project]$ 
[ashu@roche-client ashu-project]$ docker login 
Log in with your Docker ID or email address to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com/ to create one.
You can log in with your password or a Personal Access Token (PAT). Using a limited-scope PAT grants better security and is required for organizations using SSO. Learn more at https://docs.docker.com/go/access-tokens/

Username: dockerashu
Password: 
WARNING! Your password will be stored unencrypted in /home/ashu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
[ashu@roche-client ashu-project]$ docker  push docker.io/dockerashu/ashuroche:nginxappv1



```

