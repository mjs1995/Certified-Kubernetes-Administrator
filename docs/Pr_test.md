# study 
[Day2-PODs](#practice-test---pods)<br>
[Day3-ReplicaSets](#practice-test---replicasets)<br>
[Day3-Deployments](#practice-test---deployments)<br>
[Day4-Services](#practice-test---services)<br>
[Day4-Namespace](#practice-test---namespace)<br>
[Day4-Imperative Commands](#practice-test---imperative-commands)<br>
[Day5-Manual Scheduling](#practice-test---manual-scheduling)<br>
[Day5-Labels and Selectors](#practice-test---labels-and-selectors)<br>
[Day5-Taints and Tolerations](#practice-test---taints-and-tolerations)<br>
[Day6-Node Affinity](#practice-test---node-affinity)<br>
[Day6-Resource Limits](#practice-test---resource-limits)<br>
[Day6-DaemonSets](#practice-test---daemonsets)<br>
[Day6-Static Pods](#practice-test---static-pods)<br>

# Core Concepts
## Practice Test - PODs
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

## Practice Test - ReplicaSets
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

## Practice Test - Deployments
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

## Practice Test - Services
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

## Practice Test - Namespace
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

## Practice Test - Imperative Commands
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

# Scheduling
## Practice Test - Manual Scheduling
1. <details>
    <summary>A pod definition file nginx.yaml is given. Create a pod using the file.</summary>
  
     ```bash
     kubectl create -f nginx.yaml
     ```

     </details>

2. <details>
    <summary>What is the status of the created POD?</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

3. <details>
    <summary>Why is the POD in a pending state?</summary>
  
     ```bash
     kubectl describe pods nginx
     kubectl get pods --namespace kube-system
     ```

     </details>

4. <details>
    <summary>Manually schedule the pod on node01.</summary>
  
     ```bash
     vi nginx.yaml # nodeName : node01
     kubectl replace --force -f nginx.yaml # kubectl delete -f nginx.yaml -> kubectl create -f nginx.yaml
     ```

     </details>

5. <details>
    <summary>Now schedule the same pod on the controlplane node.</summary>
  
     ```bash
     vi nginx.yaml # nodeName : controlplane
     kubectl replace --force -f nginx.yaml # kubectl delete -f nginx.yaml -> kubectl create -f nginx.yaml
     kubectl get pods
     ```

     </details>

## Practice Test - Labels and Selectors
1. <details>
    <summary>We have deployed a number of PODs. They are labelled with tier, env and bu. How many PODs exist in the dev environment (env)?</summary>
  
     ```bash
     kubectl get pods --selector env=dev
     kubectl get pods --selector env=dev --no-headers | wc -l
     ```

     </details>

2. <details>
    <summary>How many PODs are in the finance business unit (bu)?</summary>
  
     ```bash
     kubectl get pods --selector bu=finance --no-headers | wc -l
     ```

     </details>

3. <details>
    <summary>How many objects are in the prod environment including PODs, ReplicaSets and any other objects?</summary>
  
     ```bash
     kubectl get all --selector env=prod --no-headers | wc -l
     ```

     </details>

4. <details>
    <summary>Identify the POD which is part of the prod environment, the finance BU and of frontend tier?</summary>
  
     ```bash
     kubectl get all --selector env=prod,bu=finance,tier=frontend
     ```

     </details>

5. <details>
    <summary>A ReplicaSet definition file is given replicaset-definition-1.yaml. Try to create the replicaset. There is an issue with the file. Try to fix it.</summary>
  
     ```bash
     vi replicaset-definition-1.yaml
     kubectl create -f replicaset-definition-1.yaml
     kubectl get rs 
     ```

     </details>

## Practice Test - Taints and Tolerations
1. <details>
    <summary>How many nodes exist on the system?Including the controlplane node.</summary>
  
     ```bash
     kubectl get nodes
     ```

     </details>

2. <details>
    <summary>Do any taints exist on node01 node?</summary>
  
     ```bash
     kubectl describe node node01 | grep Taint
     ```

     </details>

3. <details>
    <summary>Create a taint on node01 with key of spray, value of mortein and effect of NoSchedule</summary>
  
     ```bash
     kubectl taint nodes node01 spray=mortein:NoSchedule
     ```

     </details>

> N
4. <details>
    <summary>Create a new pod with the nginx image and pod name as mosquito.</summary>
  
     ```bash
     kubectl run mosquito --image=nginx 
     kubectl get pods 
     ```

     </details>

5. <details>
    <summary>What is the state of the POD?</summary>
  
     ```bash
     kubectl get pods 
     ```

     </details>

6. <details>
    <summary>Why do you think the pod is in a pending state?</summary>
  
     ```bash
     kubectl describe pods 
     ```

     </details>

> HH
7. <details>
    <summary>Create another pod named bee with the nginx image, which has a toleration set to the taint mortein.</summary>
  
     ```bash
     kubectl run bee --image=nginx --dry-run=client -o yaml
     kubectl run bee --image=nginx --dry-run=client -o yaml > bee.yaml
     vi bee.yaml # tolerations : ~
     kubectl create -f bee.yaml
     kubectl get pods --watch
     ```

     </details>

9. <details>
    <summary>Do you see any taints on controlplane node?</summary>
  
     ```bash
     kubectl describe node controlplane | grep Taint
     ```

     </details>

> H
10. <details>
    <summary>Remove the taint on controlplane, which currently has the taint effect of NoSchedule.</summary>
  
     ```bash
     # kubectl taint nodes controlplane node-role.kubernetes.io/master:NoSchedule-
     kubectl taint nodes controlplane node-role.kubernetes.io/control-plane:NoSchedule-
     kubectl describe node controlplane
     ```

     </details>

11. <details>
    <summary>What is the state of the pod mosquito now?</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

12. <details>
    <summary>Which node is the POD mosquito on now?</summary>
  
     ```bash
     kubectl get pods -o wide
     ```

     </details>

## Practice Test - Node Affinity
1. <details>
    <summary>How many Labels exist on node node01?</summary>
  
     ```bash
     kubectl describe node node01
     ```

     </details>

2. <details>
    <summary>What is the value set to the label key beta.kubernetes.io/arch on node01?</summary>
  
     ```bash
     kubectl describe node node01
     ```

     </details>

3. <details>
    <summary>Apply a label color=blue to node node01</summary>
  
     ```bash
     kubectl label node node01 color=blue
     ```

     </details>

4. <details>
    <summary>Create a new deployment named blue with the nginx image and 3 replicas.</summary>
  
     ```bash
     kubectl create deployment blue --image=nginx
     kubectl scale deployment blue --replicas=3
     # kubectl create deployment blue --image=nginx --replicas=3
     ```

     </details>

5. <details>
    <summary>Which nodes can the pods for the blue deployment be placed on?</summary>
  
     ```bash
     kubectl describe nodes|grep -i Taints
     kubectl get pods -o wide
     ```

     </details>

> H
6. <details>
    <summary>Set Node Affinity to the deployment to place the pods on node01 only.</summary>
  
     ```bash
     # https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes-using-node-affinity/
     kubectl edit deployment blue # ctrl + v -> esc -> shift + . 
     ```

     </details>

7. <details>
    <summary>Which nodes are the pods placed on now?</summary>
  
     ```bash
     kubectl get pods -o wide
     ```

     </details>

> H
8. <details>
    <summary>Create a new deployment named red with the nginx image and 2 replicas, and ensure it gets placed on the controlplane node only.Use the label key - node-role.kubernetes.io/control-plane - which is already set on the controlplane node.</summary>
  
     ```bash
     kubectl describe node controlplane
     kubectl create deployment red --image=nginx --replicas=2 --dry-run=client -o yaml
     kubectl create deployment red --image=nginx --replicas=2 --dry-run=client -o yaml > red.yaml
     vi red.yaml
     # https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes-using-node-affinity/ - operator: Exists
     kubectl create -f red.yaml
     ```

     </details>

## Practice Test - Resource Limits
1. <details>
    <summary>A pod called rabbit is deployed. Identify the CPU requirements set on the Pod</summary>
  
     ```bash
     kubectl describe pod rabbit
     ```

     </details>

2. <details>
    <summary>Delete the rabbit Pod.Once deleted, wait for the pod to fully terminate.</summary>
  
     ```bash
     kubectl delete pod rabbit
     ```

     </details>

3. <details>
    <summary>Another pod called elephant has been deployed in the default namespace. It fails to get to a running state. Inspect this pod and identify the Reason why it is not running.</summary>
  
     ```bash
     kubectl get pods
     kubectl describe pod elephant
     ```

     </details>

5. <details>
    <summary>The elephant pod runs a process that consumes 15Mi of memory. Increase the limit of the elephant pod to 20Mi.</summary>
  
     ```bash
     kubectl get pods elephant -o yaml > elephant.yaml
     vi elephant.yaml
     kubectl delete pod elephant
     kubectl create -f elephant.yaml
     kubectl get pods
     ```

     </details>

7. <details>
    <summary>Delete the elephant Pod.</summary>
  
     ```bash
     kubectl delete pod elephant
     ```

     </details>

## Practice Test - DaemonSets
1. <details>
    <summary>How many DaemonSets are created in the cluster in all namespaces?</summary>
  
     ```bash
     kubectl get daemonsets --all-namespaces
     kubectl get daemonsets --A
     ```

     </details>

2. <details>
    <summary>Which namespace are the DaemonSets created in?</summary>
  
     ```bash
     kubectl get daemonsets --all-namespaces
     ```

     </details>

3. <details>
    <summary>Which of the below is a DaemonSet?</summary>
  
     ```bash
     kubectl get all --all-namespaces
     ```

     </details>

4. <details>
    <summary>On how many nodes are the pods scheduled by the DaemonSet kube-proxy?</summary>
  
     ```bash
     kubectl describe daemonset kube-proxy --namespace=kube-system
     ```

     </details>

5. <details>
    <summary>What is the image used by the POD deployed by the kube-flannel-ds DaemonSet?</summary>
  
     ```bash
     kubectl get daemonsets --all-namespaces
     kubectl describe ds kube-flannel-ds --namespace=kube-flannel
     ```

     </details>

> H
6. <details>
    <summary>Deploy a DaemonSet for FluentD Logging.</summary>
  
     ```bash
     kubectl create deployment elasticsearch -n kube-system --image=registry.k8s.io/fluentd-elasticsearch:1.20 --dry-run=client -o yaml          
     kubectl create deployment elasticsearch -n kube-system --image=registry.k8s.io/fluentd-elasticsearch:1.20 --dry-run=client -o yaml > fluentd.yaml
     vi fluentd.yaml
     kubectl create -f fluentd.yaml
     kubectl get ds -n kube-system
     ```

     </details>

## Practice Test - Static Pods
1. <details>
    <summary>How many static pods exist in this cluster in all namespaces?</summary>
  
     ```bash
     kubectl get pods --all-namespaces
     ```

     </details>

2. <details>
    <summary>Which of the below components is NOT deployed as a static pod?</summary>
  
     ```bash
     kubectl get pods --all-namespaces
     ```

     </details>

3. <details>
    <summary>Which of the below components is NOT deployed as a static POD?</summary>
  
     ```bash
     kubectl get pods --all-namespaces
     ```

     </details>

4. <details>
    <summary>On which nodes are the static pods created currently?</summary>
  
     ```bash
     kubectl get pods --all-namespaces -o wide
     ```

     </details>

5. <details>
    <summary>On which nodes are the static pods created currently?</summary>
  
     ```bash
     ps -aux | grep config.yaml
     cat /var/lib/kubelet/config.yaml
     ```

     </details>

6. <details>
    <summary>How many pod definition files are present in the manifests folder?</summary>
  
     ```bash
     ls /etc/kubernetes/manifests/   
     ```

7. <details>
    <summary>What is the docker image used to deploy the kube-api server as a static pod?</summary>
  
     ```bash
     cat /etc/kubernetes/manifests/kube-apiserver.yaml   
     ```

     </details>

> H
8. <details>
    <summary>Create a static pod named static-busybox that uses the busybox image and the command sleep 1000</summary>
  
     ```bash
     kubectl run --restart=Never --image=busybox static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
     kubectl get pods
     ```

     </details>

9. <details>
    <summary>Create a static pod named static-busybox that uses the busybox image and the command sleep 1000</summary>
  
     ```bash
     vi /etc/kubernetes/manifests/static-busybox.yaml
     kubectl get pods --watch
     # kubectl run --restart=Never --image=busybox:1.28.4 static-busybox--dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
     ```

     </details>

> H
10. <details>
    <summary>We just created a new static pod named static-greenbox. Find it and delete it.</summary>
  
     ```bash
     kubectl get pods -o wide
     kubectl delete pods static-greenbox-node01
     ls /etc/kubernetes/manifests/   
     kubectl get nodes -o wide
     ssh 10.24.105.9
     cat /var/lib/kubelet/config.yaml # grep staticPodPath /var/lib/kubelet/config.yaml
     cd /etc/just-to-mess-with-you # node01 $ rm -rf /etc/just-to-mess-with-you/greenbox.yaml
     ls 
     rm greenbox.yaml
     exit
     kubectl get pods --watch
     ```

     </details>

## Practice Test - Multiple Schedulers
1. <details>
    <summary>What is the name of the POD that deploys the default kubernetes scheduler in this environment?</summary>
  
     ```bash
     kubectl get pods --namespace=kube-system
     ```

     </details>

2. <details>
    <summary>What is the image used to deploy the kubernetes scheduler?</summary>
  
     ```bash
     kubectl describe pod kube-scheduler-controlplane --namespace=kube-system
     ```

     </details>

3. <details>
    <summary>We have already created the ServiceAccount and ClusterRoleBinding that our custom scheduler will make use of</summary>
  
     ```bash
     # kubectl describe pod kube-scheduler-controlplane --namespace=kube-system
     kubectl get sa my-scheduler -n kube-system
     ```

     </details>

4. <details>
    <summary>Let's create a configmap that the new scheduler will employ using the concept of ConfigMap as a volume.</summary>
  
     ```bash
     kubectl create configmap my-scheduler-config --from-file=/root/my-scheduler-config.yaml -n kube-system
     kubectl get configmap my-scheduler-config -n kube-system

     ```

     </details>

5. <details>
    <summary>Deploy an additional scheduler to the cluster following the given specification.</summary>
  
     ```bash
     kubectl describe pod kube-scheduler-controlplane --namespace=kube-system | grep Image # registry.k8s.io/kube-scheduler:v1.26.0
     vi my-scheduler.yaml
     kubectl create -f my-scheduler.yaml
     kubectl get pods -n kube-system
     ```

     </details>

6. <details>
    <summary>A POD definition file is given. Use it to create a POD with the new custom scheduler.</summary>
  
     ```bash
     vi nginx-pod.yaml # spec > schedulerName : my-scheduler
     kubectl create -f nginx-pod.yaml
     ```

     </details>

# Logging & Monitoring
## Practice Test - Monitor Cluster Components
1. <details>
    <summary>We have deployed a few PODs running workloads. Inspect them.</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

2. <details>
    <summary>Let us deploy metrics-server to monitor the PODs and Nodes. Pull the git repository for the deployment files.</summary>
  
     ```bash
     git clone https://github.com/kodekloudhub/kubernetes-metrics-server.git
     ```

     </details>

3. <details>
    <summary>Deploy the metrics-server by creating all the components downloaded.</summary>
  
     ```bash
     cd kubernetes-metrics-server
     kubectl create -f .
     ```

     </details>

4. <details>
    <summary>It takes a few minutes for the metrics server to start gathering data.</summary>
  
     ```bash
     kubectl top node
     ```

     </details>

5. <details>
    <summary>Identify the node that consumes the most CPU.</summary>
  
     ```bash
     kubectl top node
     ```

     </details>

6. <details>
    <summary>Identify the node that consumes the most Memory.</summary>
  
     ```bash
     kubectl top node
     ```

     </details>

7. <details>
    <summary>Identify the POD that consumes the most Memory.</summary>
  
     ```bash
     kubectl top pod
     ```

     </details>

8. <details>
    <summary>Identify the POD that consumes the least CPU.</summary>
  
     ```bash
     kubectl top pod
     ```

     </details>

## Practice Test - Application Logs
1. <details>
    <summary>We have deployed a POD hosting an application. Inspect it. Wait for it to start.</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

2. <details>
    <summary>A user - USER5 - has expressed concerns accessing the application. Identify the cause of the issue.</summary>
  
     ```bash
     kubectl logs webapp-1
     ```

     </details>

3. <details>
    <summary>We have deployed a new POD - webapp-2 - hosting an application. Inspect it. Wait for it to start.</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

4. <details>
    <summary>A user is reporting issues while trying to purchase an item. Identify the user and the cause of the issue.</summary>
  
     ```bash
     kubectl logs webapp-2
     ```

     </details>

# Practice Test - Rolling Updates and Rollback
1. <details>
    <summary>We have deployed a simple web application. Inspect the PODs and the Services</summary>
  
     ```bash
     kubectl get pods
     kubectl get services
     ```

     </details>

3. <details>
    <summary>Run the script named curl-test.sh to send multiple requests to test the web application. Take a note of the output.</summary>
  
     ```bash
     kubectl describe deployment
     ./curl-test.sh
     ```

     </details>

> N
4. <details>
    <summary>Inspect the deployment and identify the number of PODs deployed by it </summary>
  
     ```bash
     kubectl describe deployment
     k get deploy
     ```

     </details>

5. <details>
    <summary>What container image is used to deploy the applications?</summary>
  
     ```bash
     kubectl describe deployment frontend
     ```

     </details>

6. <details>
    <summary>Inspect the deployment and identify the current strategy</summary>
  
     ```bash
     kubectl describe deployment frontend
     ```

     </details>

7. <details>
    <summary>If you were to upgrade the application now what would happen?</summary>
  
     ```bash
     kubectl describe deployment frontend
     ```

     </details>

8. <details>
    <summary>Let us try that. Upgrade the application by setting the image on the deployment to kodekloud/webapp-color:v2</summary>
  
     ```bash
     # kubectl edit deployment frontend
     kubectl describe deployment frontend
     k set image deploy frontend simple-webapp=kodekloud/webapp-color:v2
     ```

     </details>

10. <details>
    <summary>Up to how many PODs can be down for upgrade at a time</summary>
  
     ```bash
     k describe deployment frontend
     ```

     </details>

11. <details>
    <summary>Change the deployment strategy to Recreate</summary>
  
     ```bash
     k edit deployment frontend
     k describe deployment frontend
     ```

     </details>

12. <details>
    <summary>Upgrade the application by setting the image on the deployment to kodekloud/webapp-color:v3</summary>
  
     ```bash
     k set image deploy frontend simple-webapp=kodekloud/webapp-color:v3
     ```

     </details>
