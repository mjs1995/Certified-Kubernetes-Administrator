# study 
[Day2-PODs](#practice-test---pods)<br>
[Day3-ReplicaSets](#practice-test---replicasets)<br>
[Day3-Deployments](#practice-test---deployments)<br>
[Day4-Services](#practice-test---services)<br>
[Day4-Namespace](#practice-test---namespace)<br>
[Day4-Imperative Commands](#practice-test---imperative-commands)<br>

# Practice Test - PODs
1. <details>
   <summary>How many pods exist on the system? In the current(default) namespace.</summary>
  
   ```bash
   kubectl get pods
   ```
  
   </details>

2. <details>
   <summary>Create a new pod with the nginx image.</summary>
  
   ```bash
   kubectl run nginx --image=nginx
   ```
  
   </details>

3. <details>
   <summary>How many pods are created now? Note: We have created a few more pods. So please check again. </summary>
  
   ```bash
   kubectl get pods
  
   kubectl get pods --no-headers | wc -l # 4 
   ```
  
   </details>

4. <details>
   <summary>What is the image used to create the new pods? You must look at one of the new pods in detail to figure this out.</summary>
  
   ```bash
   kubectl describe pod newpods | grep image
   ```
  
   </details>
   
5. <details>
   <summary>Which nodes are these pods placed on? You must look at all the pods in detail to figure this out.</summary>
  
   ```bash
   kubectl get pods -o wide
   ```
  
   </details>

6. <details>
   <summary>How many containers are part of the pod webapp?Note: We just created a new POD. Ignore the state of the POD for now.</summary>
  
   ```bash
   kubectl describe pod webapp
   ```
  
   </details>


7. <details>
   <summary>What images are used in the new webapp pod?You must look at all the pods in detail to figure this out.</summary>
  
   ```bash
   kubectl describe pod webapp | grep images
   ```
  
   </details>

8. <details>
   <summary>What is the state of the container agentx in the pod webapp? Wait for it to finish the ContainerCreating state </summary>
  
   ```bash
   kubectl describe pod webapp | grep agentx
   ```
  
   </details>

9. <details>
   <summary>Why do you think the container agentx in pod webapp is in error? Try to figure it out from the events section of the pod.</summary>
  
   ```bash
   kubectl describe pod webapp | grep agentx
   ```
  
   </details>

10. <details>
    <summary>What does the READY column in the output of the kubectl get pods command indicate?</summary>
  
     ```bash
     kubectl get pods 
     ```

     </details>
   
11. <details>
    <summary>Delete the webapp Pod.Once deleted, wait for the pod to fully terminate. </summary>
  
     ```bash
     kubectl delete pod webapp
     ```

     </details>

> H
12. <details>
    <summary>Create a new pod with the name redis and with the image redis123.Use a pod-definition YAML file. And yes the image name is wrong! </summary>
  
     ```bash
     # --dry-run=clientkubectl실제로 아무것도 하지 않고 테스트
     # o yaml"API 서버에 보낼 내용을 콘솔에 출력"이라고 말하면 명명된 파일로 리디렉션됨
     kubectl run redis --image=redis123 --dry-run=client -o yaml > redis-definition.yaml
     
     kubectl create -f redis-definition.yaml 
  
     kubectl get pods
     ```

     </details>

> H
13. <details>
    <summary>Now change the image on this pod to redis.Once done, the pod should be in a running state.Check </summary>
  
     ```bash
     kubectl edit pod redis
     kubectl apply -f redis-definition.yaml 
    
     # 2
     cat redis.yaml
     vi redis.yaml

     # 3
     kubectl set image pod/redis redis=redis 
     ```

     </details>

# Practice Test - ReplicaSets
1. <details>
    <summary>How many PODs exist on the system? </summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

2. <details>
    <summary>How many ReplicaSets exist on the system? </summary>
  
     ```bash
     kubectl get replicaset
     ```

     </details>

3. <details>
    <summary>How about now? How many ReplicaSets do you see? </summary>
  
     ```bash
     kubectl get replicaset
     ```

     </details>
     
4. <details>
    <summary>How many PODs are DESIRED in the new-replica-set? </summary>
  
     ```bash
     kubectl get replicaset
     ```

     </details>

> N
5. <details>
    <summary>What is the image used to create the pods in the new-replica-set? </summary>
  
     ```bash
     kubectl describe pod new-replica-set | grep image
   
     kubectl get rs -o wide
     ```

     </details>
     
6. <details>
    <summary>How many PODs are READY in the new-replica-set? </summary>
  
     ```bash   
     kubectl get rs
     ```

     </details>

7. <details>
    <summary>Why do you think the PODs are not ready? </summary>
  
     ```bash
     kubectl describe pods
     ```

     </details>

8. <details>
    <summary>Delete any one of the 4 PODs. </summary>
  
     ```bash
     kubectl get pods
     kubectl delete pod new-replica-set-lzp4m
     ```

     </details>
     
9. <details>
    <summary>How many PODs exist now? </summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

10. <details>
    <summary>Why are there still 4 PODs, even after you deleted one? </summary>
  
     ```bash
     ReplicaSets ensures that desired number of PODs always run
     ```

     </details>

11. <details>
    <summary>Create a ReplicaSet using the replicaset-definition-1.yaml file located at /root/. </summary>
  
     ```bash
     kubectl explain replicaset | grep VERSION # VERSION:  apps/v1
     vi replicaset-definition-1.yaml
     kubectl create -f replicaset-definition-1.yaml
     ```

     </details>

12. <details>
    <summary>Fix the issue in the replicaset-definition-2.yaml file and create a ReplicaSet using it. </summary>
  
     ```bash
     vi replicaset-definition-2.yaml # 라벨 동일하게 만듬
     kubectl create -f replicaset-definition-2.yaml
     ```

     </details>

13. <details>
    <summary>Delete the two newly created ReplicaSets - replicaset-1 and replicaset-2 </summary>
  
     ```bash
     kubectl delete replicaset replicaset-1
     kubectl delete rs replicaset-2
      
     kubectl delete replicaset replicaset-1 replicaset-2
     ```

14. <details>
    <summary>Fix the original replica set new-replica-set to use the correct busybox image. Either delete and recreate the ReplicaSet or Update the existing ReplicaSet and then delete all PODs, so new ones with the correct image will be created.</summary>
  
     ```bash
     kubectl edit replicaset new-replica-set # Image busybox777 -> busybox , 이미지 이름이 업데이트 되어도 파드는 자동으로 생성되지 않음. 삭제하고 다시 생성해야함 
     kubectl describe rs
     kubectl get pods
     kubectl delete pod new-replica-set-gdx9p new-replica-set-sc49p new-replica-set-zxcnm new-replica-set-4b5wr
     kubectl get rs
     ```

     </details>

15. <details>
    <summary>Scale the ReplicaSet to 5 PODs.Use kubectl scale command or edit the replicaset using kubectl edit replicaset.</summary>
  
     ```bash
     kubectl edit replicaset new-replica-set # 직접 변경
     kubectl scale rs new-replica-set --replicas 5 
     ```

     </details>

16. <details>
    <summary>Now scale the ReplicaSet down to 2 PODs.Use the kubectl scale command or edit the replicaset using kubectl edit replicaset.</summary>
  
     ```bash
     kubectl edit replicaset new-replica-set 
     kubectl scale rs new-replica-set --replicas 2
     ```

     </details>

# Practice Test - Deployments
1. <details>
    <summary>How many PODs exist on the system?</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

2. <details>
    <summary>How many ReplicaSets exist on the system?</summary>
  
     ```bash
     kubectl get rs
     ```

     </details>

3. <details>
    <summary>How many Deployments exist on the system?</summary>
  
     ```bash
     kubectl get deployment
     ```

     </details>

4. <details>
    <summary>How many Deployments exist on the system?</summary>
  
     ```bash
     kubectl get deployment
     ```

     </details>


5. <details>
    <summary>How many ReplicaSets exist on the system now?</summary>
  
     ```bash
     kubectl get rs
     ```

     </details>

6. <details>
    <summary>How many PODs exist on the system now?</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

7. <details>
    <summary>Out of all the existing PODs, how many are ready?</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

8. <details>
    <summary>What is the image used to create the pods in the new deployment?</summary>
  
     ```bash
     kubectl describe pods | grep image
     kubectl get deployment -o wide
     ```

     </details>

9. <details>
    <summary>Why do you think the deployment is not ready?</summary>
  
     ```bash
     kubectl describe pods | grep image
     ```

     </details>

10. <details>
    <summary>Create a new Deployment using the deployment-definition-1.yaml file located at /root/.</summary>
  
     ```bash
     kubectl create -f deployment-definition-1.yaml 
     vi deployment-definition-1.yaml # kind : deployment -> kind : Deployment
     kubectl create -f deployment-definition-1.yaml
     ```

     </details>

11. <details>
    <summary>Create a new Deployment with the below attributes using your own deployment definition file.Name: httpd-frontend;Replicas: 3;Image: httpd:2.4-alpine</summary>
  
     ```bash
     kubectl create deployment httpd-frontend --image=httpd:2.4-alpine --replicas=3
     kubectl get deploy
   
     kubectl create -f my-deployment.yaml
     ```

     </details>

# Practice Test - Services
1. <details>
    <summary>How many Services exist on the system?</summary>
  
     ```bash
     kubectl get services
     ```

     </details>

3. <details>
    <summary>What is the type of the default kubernetes service?</summary>
  
     ```bash
     kubectl get services
     ```

     </details>

4. <details>
    <summary>What is the targetPort configured on the kubernetes service?</summary>
  
     ```bash
     kubectl describe services | grep TargetPort
     ```

     </details>

5. <details>
    <summary>How many labels are configured on the kubernetes service?</summary>
  
     ```bash
     kubectl describe services
     
     ```

     </details>

6. <details>
    <summary>How many Endpoints are attached on the kubernetes service?</summary>
  
     ```bash
     kubectl describe services
     ```

     </details>

7. <details>
    <summary>How many Deployments exist on the system now?</summary>
  
     ```bash
     kubectl get deployments
     ```

     </details>

8. <details>
    <summary>What is the image used to create the pods in the deployment?</summary>
  
     ```bash
     kubectl get deployments
     kubectl get deployment -o wide
     kubectl describe deployments | grep Image
     ```

     </details>

9. <details>
    <summary>Are you able to accesss the Web App UI?Try to access the Web Application UI using the tab simple-webapp-ui above the terminal.</summary>
  
     ```bash
     가운데 상단의 simple-webapp-ui 클릭
     ```

     </details>

10. <details>
    <summary>Create a new service to access the web application using the service-definition-1.yaml file.</summary>
  
     ```bash
     vi service-definition-1.yaml
     kubectl create -f service-definition-1.yaml
     ```

     </details>

# Practice Test - Namespace
1. <details>
    <summary>How many Namespaces exist on the system?</summary>
  
     ```bash
     kubectl get namespace
     ```

     </details>

2. <details>
    <summary>How many pods exist in the research namespace?</summary>
  
     ```bash
     kubectl get pods --namespace=research
     ```

     </details>

> H
3. <details>
    <summary>Create a POD in the finance namespace.</summary>
  
     ```bash
     kubectl run redis --image=redis --namespace=finance
     kubectl get pods -n=finance
     ```

     </details>

4. <details>
    <summary>Which namespace has the blue pod in it?</summary>
  
     ```bash
     kubectl get pods --all-namespaces
     ```

     </details>

6. <details>
    <summary>What DNS name should the Blue application use to access the database db-service in its own namespace - marketing?You can try it in the web application UI. Use port 6379.</summary>
  
     ```bash
     kubectl get pods -n=marketing
     kubectl get svc -n=marketing
     ```

     </details>

7. <details>
    <summary>What DNS name should the Blue application use to access the database db-service in the dev namespace?You can try it in the web application UI. Use port 6379.</summary>
  
     ```bash
     kubectl get pods -n=marketing
     kubectl get svc -n=marketing
     kubectl get svc -n=dev
     ```

     </details>

# Practice Test - Imperative Commands
2. <details>
    <summary>Deploy a pod named nginx-pod using the nginx:alpine image.</summary>
  
     ```bash
     kubectl run nginx-pod --image=nginx:alpine
     ```

     </details>

> N
3. <details>
    <summary>Deploy a redis pod using the redis:alpine image with the labels set to tier=db.</summary>
  
     ```bash
     kubectl run redis --image=redis:alpine --labels="tier=db"
     kubectl run redis --image=redis:alpine -l tier=db
     ```

     </details>

4. <details>
    <summary>Create a service redis-service to expose the redis application within the cluster on port 6379.</summary>
  
     ```bash
     kubectl create service --help
     kubectl create service clusterip --help
     kubectl expose pod redis --port=6379 --name redis-service
     kubectl get svc redis-service
     ```

     </details>

5. <details>
    <summary>Create a deployment named webapp using the image kodekloud/webapp-color with 3 replicas.</summary>
  
     ```bash
     kubectl create deployment webapp --image=kodekloud/webapp-color --replicas=3
     ```

     </details>

6. <details>
    <summary>Create a new pod called custom-nginx using the nginx image and expose it on container port 8080.</summary>
  
     ```bash
     kubectl run custom-nginx --image=nginx --port=8080
     ```

     </details>

7. <details>
    <summary>Create a new namespace called dev-ns.</summary>
  
     ```bash
     kubectl create namespace dev-ns    
     kubectl create ns dev-ns
     ```

     </details>

8. <details>
    <summary>Create a new deployment called redis-deploy in the dev-ns namespace with the redis image. It should have 2 replicas.</summary>
  
     ```bash
     kubectl create deployment redis-deploy -n dev-ns --image redis --replicas 2
     ```

     </details>

9. <details>
    <summary>Create a pod called httpd using the image httpd:alpine in the default namespace. Next, create a service of type ClusterIP by the same name (httpd). The target port for the service should be 80.</summary>
  
     ```bash
     kubectl run httpd --image httpd:alpine --expose --port 80
     ```

     </details>
