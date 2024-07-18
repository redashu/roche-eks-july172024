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