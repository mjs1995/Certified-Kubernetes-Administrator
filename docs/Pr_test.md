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
