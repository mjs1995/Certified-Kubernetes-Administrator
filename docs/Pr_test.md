# study 
[Day2-PODs](#practice-test---pods)<br>
[Day3-ReplicaSets](#practice-test---replicasets)<br>

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
