## pod task1

```
  1. Create pod named  <yourname>pod1
  2. In POd docker image will be busybox 
  3. choose ping fb.com as default process
  4. check output of default process and store in a file  called logs.txt in client machine 
  5. now transfer logs.txt on your pods under /opt/logs.txt 
  6. check that pods is scheduled in which minion node and store that name in logs.txt inside pod 
  7. make sure previous data in logs.txt must be present 
  
  
```

## POd task 2 

```
  1. Create pod named  <yourname>mcpod1 
  2. In POd docker image will be alpine  
  3. choose default process whatever you want 
  4. create a file name hello.txt with some data under /mnt location of alpine container 
  5. second docker image will be nginx 
  6. choose container name as per your own convenience  
  7. transfer file from alpine container to nginx container 
  8. in nginx container file must be present under /root location 
 
  
```

### manifest task 1 

```
  1. Create YAML named mytask.yaml in your client side System 
  2. YAML must create A namespace named <yourname>k8s1 
  3. It Must create One Pod with anyname under same namespace you created above
  4. Pod Container can have ubuntu:latest docker image 
  5. ANy parent process for POd container that can keep pod UP and running 
  
  6. Create One service of NodePort type named <yourname>svc1  under same namespace you created above
  7. NodePort you have to choose statically in range of 30000-32768
  8. you don't have to match label of pods , created above  
  
  9.  Deploy the above created YAML 
  10. and check the pod and svc name that namespace 
  11. both must be running fine 
  
  12. Now copy any text file from Your client machine to the running pod 
  13. File location inside RUnning pod must be /tmp 
```

### Deployment SPlunk 

```
  1. Create a yaml file named  <yourname>splunk.yaml
  2. namespace called  kube-ashu and all the must be inside in this namespace only
  3. use splunk/splunk:latest image from docker hub  to create deployment 
  4. required ENV variable must be stored in ConfigMap  
  5. Required password must be stored in Secret 
  6. replica count 1 
  7. create service of Nodeport  type named <yourname>svc 
  8. access this from web browser 
  9. Note : default username of splunk is admin and splunk default port number is 8000 
  
  
```

### POD and service task 

```
  1. Create two Pods <yourname>pod1 and <yourname>Pod2
  2. In POd1 you can use busybox docker image 
  3. choose whatever parent process for pod1 container 
  4. Pod1 Restart Policy must be Never
  5. No label required to Pod1 
  
  6. IN Pod2 use nginx docker image 
  7. no need of parent process in pod2 container as it is already having
  8. Pod2 label will be delvex: <yourname>p11
  9. containerport is 80 
  10. Create a Service for Pod2 named <yourname>svc2 of ClusterIP type 
  11. Service must find Pod2 using labels 
  
  12. From Pod1 access Pod2 default web application page using Service IP 
  13. store the Output of default web page in Pod1 /tmp/mypage.txt 

  ```
  