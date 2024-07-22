## building java spring webapp to war

```
[ashu@roche-client ashu-project]$ ls -a  java-springboot/
.  ..  .dockerignore  .git  Dockerfile  README.md  pom.xml  src
[ashu@roche-client ashu-project]$ docker build  -t  ashujavaweb:springv1  java-springboot/
[+] Building 119.7s (11/11) FINISHED                                                                              docker:default
 => [internal] load build definition from Dockerfile                                                                        0.0s
 => => transferring dockerfile: 342B                                                                                        0.0s
 => [internal] load metadata for docker.io/library/oraclelinux:8.4                                                          0.3s
 => [auth] library/oraclelinux:pull token for registry-1.docker.io                                                          0.0s
 => [internal] load .dockerignore                                                                                           0.0s
 => => transferring context: 139B                                                                                           0.0s
 => [1/5] FROM docker.io/library/oraclelinux:8.4@sha256:b81d5b0638bb67030b207d28586d0e714a811cc612396dbe3410db406998b3ad    6.5s
 => => resolve docker.io/library/oraclelinux:8.4@sha256:b81d5b0638bb67030b207d28586d0e714a811cc612396dbe3410db406998b3ad    0.0s
 => => sha256:a4df6f21af842935f0b80f5f255a88caf5f16b86e2642b468f83b8976666c3d7 90.36MB / 90.36MB                            1.8s
 => => sha256:b81d5b0638bb67030b207d28586d0e714a811cc612396dbe3410db406998b3ad 547B / 547B                                  0.0s
 => => sha256:ef0327c1a51e3471e9c2966b26b6245bd1f4c3f7c86d7edfb47a39adb446ceb5 529B / 529B                                  0.0s
 => => sha256:97e22ab49eea70a5d500e00980537605d56f30f9614b3a6d6c4ae9ddbd642489 1.48kB / 1.48kB                              0.0s
 => => extracting sha256:a4df6f21af842935f0b80f5f255a88caf5f16b86e2642b468f83b8976666c3d7                                   4.4s
 => [internal] load build context                                                                                           0.0s
 => => transferring context: 6.17kB                                                                                         0.0s
 => [2/5] RUN dnf install java-1.8.0-openjdk.x86_64  java-1.8.0-openjdk-devel.x86_64  maven  -y                            78.4s
 => [3/5] WORKDIR /ashu-java                                                                                                0.1s 
 => [4/5] COPY .  .                                                                                                         0.1s 
 => [5/5] RUN mvn clean package                                                                                            20.1s 
 => exporting to image                                                                                                     13.7s 
 => => exporting layers                                                                                                    13.7s 
 => => writing image sha256:f84bc7bb2913942af6d11ecc19afbad3f3e5406d82b7855d6e739c1ef8f06f3a                                0.0s 
 => => naming to docker.io/library/ashujavaweb:springv1                                                                     0.0s 
[ashu@roche-client ashu-project]$                            
```


### tomcat with maven 

<img src="tom.png">

### Cleaning namespace data

```
kubectl  delete all,secret,ing,cm --all 
secret "ashudb-root-cred" deleted
secret "flask-db-cred" deleted
ingress.networking.k8s.io "minimal-ingress-ashu-routing" deleted
configmap "ashu-db-svc" deleted
configmap "kube-root-ca.crt" deleted
configmap "seccomp-profile" deleted

```

