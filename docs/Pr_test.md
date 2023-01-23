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
[Day7-Multiple Schedulers](#practice-test---multiple-schedulers)<br>
[Day7-Monitor Cluster Components](#practice-test---monitor-cluster-components)<br>
[Day7-Monitor Application Logs](#practice-test---application-logs)<br>
[Day7-Rolling Updates and Rollback](#practice-test---rolling-updates-and-rollback)<br>
[Day8-Commands and Arguments](#practice-test---commands-and-arguments)<br>
[Day8-Env Variables](#practice-test---env-variables)<br>
[Day9-Secrets](#practice-test---secrets)<br>
[Day9-Multi-Container Pods](#practice-test---multi-container-pods)<br>
[Day9-Init-Containers](#practice-test---init-containers)<br>
[Day10-OS Upgrades](#practice-test---os-upgrades)<br>
[Day10-Cluster Upgrade Process](#practice-test---cluster-upgrade-process)<br>
[Day10-Cluster Upgrade Process](#practice-test---cluster-upgrade-process)<br>
[Day11-Backup and Restore Methods](#practice-test---backup-and-restore-methods)<br>
[Day11-Backup and Restore Methods2](#practice-test---backup-and-restore-methods2)<br>
[Day12-View Certificates](#practice-test---view-certificates)<br>
[Day13-Certificates API](#practice-test---certificates-api)<br>
[Day13-RBAC](#practice-test---rbac)<br>
[Day13-KubeConfig](#practice-test---kubeconfig)<br>
[Day14-Cluster Roles](#practice-test---cluster-roles)<br>
[Day14-Service Accounts](#practice-test---service-accounts)<br>
[Day14-Image Security](#practice-test---image-security)<br>
[Day14-Security Context](#practice-test---security-context)<br>
[Day15-Network Policies](#practice-test---network-policies)<br>
[Day16-Persistent Volume Claims](#practice-test---persistent-volume-claims)<br>
[Day16-Storage Class](#practice-test---storage-class)<br>

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

# Application Lifecycle Management
## Practice Test - Commands and Arguments
1. <details>
    <summary>How many PODs exist on the system?</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

2. <details>
    <summary>What is the command used to run the pod ubuntu-sleeper?</summary>
  
     ```bash
     kubectl describe pod
     # kubectl describe pod ubuntu-sleeper 
     ```

     </details>

3. <details>
    <summary>Create a pod with the ubuntu image to run a container to sleep for 5000 seconds. Modify the file ubuntu-sleeper-2.yaml.</summary>
  
     ```bash
     vi ubuntu-sleeper-2.yaml #  command : ["sleep"] args: ["5000"]
     kubectl create -f ubuntu-sleeper-2.yaml
     ```

     </details>

4. <details>
    <summary>Create a pod using the file named ubuntu-sleeper-3.yaml. There is something wrong with it. Try to fix it!</summary>
  
     ```bash
     vi ubuntu-sleeper-3.yaml #  "1200" 
     kubectl create -f ubuntu-sleeper-3.yaml
     ```

     </details>

> N
5. <details>
    <summary>Update pod ubuntu-sleeper-3 to sleep for 2000 seconds.</summary>
  
     ```bash
     kubectl edit pod ubuntu-sleeper-3 # "/tmp/kubectl-edit-793660717.yaml
     kubectl replace --force -f /tmp/kubectl-edit-793660717.yaml
     ```

     </details>

6. <details>
    <summary>Inspect the file Dockerfile given at /root/webapp-color directory. What command is run at container startup?.</summary>
  
     ```bash
     cat /root/webapp-color/Dockerfile
     ```

     </details>

7. <details>
    <summary>Inspect the file Dockerfile2 given at /root/webapp-color directory. What command is run at container startup?</summary>
  
     ```bash
     cat /root/webapp-color/Dockerfile2
     ```

     </details>

8. <details>
    <summary>Inspect the two files under directory webapp-color-2. What command is run at container startup?</summary>
  
     ```bash
     cat webapp-color-2/webapp-color-pod.yaml
     ```

     </details>

9. <details>
    <summary>Inspect the two files under directory webapp-color-3. What command is run at container startup?</summary>
  
     ```bash
     cat webapp-color-3/webapp-color-pod-2.yaml
     ```

     </details>

> H
10. <details>
    <summary>Create a pod with the given specifications. By default it displays a blue background. Set the given command line arguments to change it to green.</summary>
  
     ```bash
     # kubectl run --help
     kubectl run webapp-green --image=kodekloud/webapp-color -- --color green
     ```

     </details>

## Practice Test - Env Variables
1. <details>
    <summary>How many PODs exist on the system?</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

2. <details>
    <summary>What is the environment variable name set on the container in the pod?</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

3. <details>
    <summary>What is the value set on the environment variable APP_COLOR on the container in the pod?</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

5. <details>
    <summary>Update the environment variable on the POD to display a green background</summary>
  
     ```bash
     kubectl edit pod webapp-color # /tmp/kubectl-edit-56807185.yaml
     kubectl replace --force -f /tmp/kubectl-edit-56807185.yaml
     ```

     </details>

7. <details>
    <summary>How many ConfigMaps exists in the default namespace?</summary>
  
     ```bash
     # k get configmap
     kubectl get configmaps
     ```

     </details>

8. <details>
    <summary>Identify the database host from the config map db-config</summary>
  
     ```bash
     kubectl describe configmaps
     ```

     </details>

9. <details>
    <summary>Create a new ConfigMap for the webapp-color POD. Use the spec given below.</summary>
  
     ```bash
     kubectl create configmap webapp-config-map --from-literal=APP_COLOR=darkblue
     k describe cm webapp-config-map
     ```

     </details>

10. <details>
    <summary>Update the environment variable on the POD to use the newly created ConfigMap</summary>
  
     ```bash
     kubectl edit pod webapp-color
     kubectl replace --force -f /tmp/kubectl-edit-599532790.yaml
     k describe pod webapp-color
     ```

     </details>

## Practice Test - Secrets
1. <details>
    <summary>How many Secrets exist on the system?</summary>
  
     ```bash
     kubectl get secrets
     ```

     </details>

2. <details>
    <summary>How many secrets are defined in the dashboard-token secret?</summary>
  
     ```bash
     kubectl get secrets
     ```

     </details>

3. <details>
    <summary>What is the type of the dashboard-token secret?</summary>
  
     ```bash
     kubectl describe secret
     ```

     </details>

4. <details>
    <summary>Which of the following is not a secret data defined in dashboard-token secret?</summary>
  
     ```bash
     kubectl describe secret
     ```

     </details>

> N
6. <details>
    <summary>The reason the application is failed is because we have not created the secrets yet. Create a new secret named db-secret with the data given below.</summary>
  
     ```bash
     k get deploy 
     k get pods 
     k get svc 
     k get secret 
     k create secret --help
     kubectl create secret generic db-secret --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123
     k get secret 
     ```

     </details>

7. <details>
    <summary>The reason the application is failed is because we have not created the secrets yet. Create a new secret named db-secret with the data given below.</summary>
  
     ```bash
     kubectl edit pod webapp-pod
     kubectl replace --force -f /tmp/kubectl-edit-1138477144.yaml
     ```

     </details>

## Practice Test - Multi-Container Pods
1. <details>
    <summary>Identify the number of containers created in the red pod.</summary>
  
     ```bash
     kubectl get pods
     ```

     </details>

2. <details>
    <summary>Identify the name of the containers running in the blue pod.</summary>
  
     ```bash
     kubectl describe pod blue
     ```

     </details>

3. <details>
    <summary>Create a multi-container pod with 2 containers.</summary>
  
     ```bash
     k run yellow --image=busybox --dry-run=client -o yaml > yellow.yaml
     vi yellow.yaml
     k create -f yellow.yaml
     ```

     </details>

6. <details>
    <summary>Inspect the app pod and identify the number of containers in it.</summary>
  
     ```bash
     k get pods -n elastic-stack
     k describe pod app -n elastic-stack
     ```

     </details>

> H
7. <details>
    <summary>The application outputs logs to the file /log/app.log. View the logs and try to identify the user having issues with Login.</summary>
  
     ```bash
     k logs app -n elastic-stack
     # kubectl -n elastic-stack exec -it app cat /log/app.log
     ```

     </details>

8. <details>
    <summary>Edit the pod to add a sidecar container to send logs to Elastic Search. Mount the log volume to the sidecar container.</summary>
  
     ```bash
     k edit pod app -n elastic-stack 
     kubectl replace --force -f /tmp/kubectl-edit-1380032120.yaml
     ```

     </details>

## Practice Test - Init-Containers
1. <details>
    <summary>Identify the pod that has an initContainer configured.</summary>
  
     ```bash
     kubectl get pods
     kubectl describe pods
     ```

     </details>

2. <details>
    <summary>What is the image used by the initContainer on the blue pod?</summary>
  
     ```bash
     kubectl describe pods
     ```

     </details>

3. <details>
    <summary>What is the state of the initContainer on pod blue?</summary>
  
     ```bash
     kubectl describe pods
     ```

     </details>

4. <details>
    <summary>Why is the initContainer terminated? What is the reason?</summary>
  
     ```bash
     kubectl describe pods
     ```

     </details>

5. <details>
    <summary>We just created a new app named purple. How many initContainers does it have?</summary>
  
     ```bash
     kubectl describe pod purple
     ```

     </details>

6. <details>
    <summary>What is the state of the POD?</summary>
  
     ```bash
     k get pods 
     ```

     </details>

7. <details>
    <summary>How long after the creation of the POD will the application come up and be available to users?</summary>
  
     ```bash
     kubectl describe pod purple
     ```

     </details>

8. <details>
    <summary>Update the pod red to use an initContainer that uses the busybox image and sleeps for 20 seconds</summary>
  
     ```bash
     k edit pod red 
     k replace --force -f /tmp/kubectl-edit-1816006413.yaml
     ```

     </details>

> N
9. <details>
    <summary>A new application orange is deployed. There is something wrong with it. Identify and fix the issue.</summary>
  
     ```bash
     k describe pod orange
     k logs orange
     k logs orange -c init-myservice # {initcontainer 이름}
     k edit pod orange 
     k replace --force -f /tmp/kubectl-edit-119883445.yaml
     ```

     </details>

# Cluster-Maintenance
## Practice Test - OS Upgrades
1. <details>
    <summary>Let us explore the environment first. How many nodes do you see in the cluster?</summary>
  
     ```bash
     # alias k=kubectl
     kubectl get nodes
     ```

     </details>

2. <details>
    <summary>How many applications do you see hosted on the cluster?</summary>
  
     ```bash
     kubectl get deploy
     ```

     </details>

3. <details>
    <summary>Which nodes are the applications hosted on?</summary>
  
     ```bash
     kubectl get pods -o wide
     ```

     </details>

4. <details>
    <summary>We need to take node01 out for maintenance. Empty the node of all applications and mark it unschedulable.</summary>
  
     ```bash
     k drain node01
     k drain node01 --ignore-daemonsets
     ```

     </details>

5. <details>
    <summary>What nodes are the apps on now?</summary>
  
     ```bash
     kubectl get pods -o wide 
     ```

     </details>

6. <details>
    <summary>The maintenance tasks have been completed. Configure the node node01 to be schedulable again.</summary>
  
     ```bash
     kubectl uncordon node01
     ```

     </details>

7. <details>
    <summary>How many pods are scheduled on node01 now?</summary>
  
     ```bash
     kubectl get pods -o wide
     ```

     </details>

9. <details>
    <summary>Why are the pods placed on the controlplane node?</summary>
  
     ```bash
     kubectl describe node controlplane
     ```

     </details>

11. <details>
    <summary>We need to carry out a maintenance activity on node01 again. Try draining the node again using the same command as before: kubectl drain node01 --ignore-daemonsets</summary>
  
     ```bash
     kubectl drain node01 --ignore-daemonsets
     ```

     </details>

12. <details>
    <summary>Why did the drain command fail on node01? It worked the first time!</summary>
  
     ```bash
     kubectl drain node01 --ignore-daemonsets
     ```

     </details>

13. <details>
    <summary>What is the name of the POD hosted on node01 that is not part of a replicaset?</summary>
  
     ```bash
     kubectl get pods -o wide
     ```

     </details>

14. <details>
    <summary>What would happen to hr-app if node01 is drained forcefully?</summary>
  
     ```bash
     kubectl drain node02 --ignore-daemonsets --force 
     ```

     </details>

16. <details>
    <summary>hr-app is a critical app and we do not want it to be removed and we do not want to schedule any more pods on node01.</summary>
  
     ```bash
     k cordon node01 
     ```

     </details>

## Practice Test - Cluster Upgrade Process
1. <details>
    <summary>This lab tests your skills on upgrading a kubernetes cluster. We have a production cluster with applications running on it. Let us explore the setup first.</summary>
  
     ```bash
     kubectl get nodes
     ```

     </details>

2. <details>
    <summary>How many nodes are part of this cluster?</summary>
  
     ```bash
     kubectl get nodes
     ```

     </details>

3. <details>
    <summary>How many nodes can host workloads in this cluster?</summary>
  
     ```bash
     k describe node | grep Taints
     ```

     </details>

4. <details>
    <summary>How many applications are hosted on the cluster?</summary>
  
     ```bash
     kubectl get deploy
     ```

     </details>

5. <details>
    <summary>What nodes are the pods hosted on?</summary>
  
     ```bash
     kubectl get pods -o wide
     ```

     </details>

7. <details>
    <summary>What is the latest stable version of Kubernetes as of today?</summary>
  
     ```bash
     kubeadm upgrade plan
     ```

     </details>

8. <details>
    <summary>What is the latest version available for an upgrade with the current version of the kubeadm tool installed?</summary>
  
     ```bash
     kubectl drain controlplane --ignore-daemonsets
     k get nodes
     ```

     </details>

> HHH
9. <details>
    <summary>Upgrade the controlplane components to exact version v1.26.0</summary>
  
     ```bash
     cat /etc/*release*
     apt update
     apt-cache madison kubeadm
     apt-get --version
     apt-get update && apt-get install -y kubeadm=1.26.0-00
     kubeadm upgrade plan
     sudo kubeadm upgrade apply v1.26.0
   
     apt-get update && apt-get install -y kubelet=1.26.0-00 kubectl=1.26.0-00 && \
     apt-mark hold kubelet kubectl

     sudo systemctl daemon-reload
     sudo systemctl restart kubelet
     k get nodes 
     ```

     </details>

11. <details>
    <summary>Mark the controlplane node as "Schedulable" again</summary>
  
     ```bash
     k uncordon controlplane
     k get nodes 
     ```

     </details>

12. <details>
    <summary>Next is the worker node. Drain the worker node of the workloads and mark it UnSchedulable</summary>
  
     ```bash
     k drain node01
     ```

     </details>

> HHH
13. <details>
    <summary>Upgrade the worker node to the exact version v1.26.0</summary>
  
     ```bash
     k get nodes
     k get pods -o wide
     k get nodes -o wide # internal ip 확인 
     ssh 10.55.91.3
   
     apt-mark unhold kubeadm && \
     apt-get update && apt-get install -y kubeadm=1.26.0-00 && \
     apt-mark hold kubeadm
   
     sudo kubeadm upgrade node
     
     apt-mark unhold kubelet kubectl && \
     apt-get update && apt-get install -y kubelet=1.26.0-00 kubectl=1.26.0-00 && \
     apt-mark hold kubelet kubectl
    
     sudo systemctl daemon-reload
     sudo systemctl restart kubelet
     exit 
     k get nodes 
     ```

     </details>

14. <details>
    <summary>Remove the restriction and mark the worker node as schedulable again.</summary>
  
     ```bash
     k uncordon node01
     k get nodes 
     ```

     </details>

## Practice Test - Backup and Restore Methods
1. <details>
    <summary>How many deployments exist in the cluster?</summary>
  
     ```bash
     kubectl get deployments
     ```

     </details>

2. <details>
    <summary>What is the version of ETCD running on the cluster?</summary>
  
     ```bash
     kubectl describe pod -n kube-system etcd-controlplane
     ```

     </details>

3. <details>
    <summary>At what address can you reach the ETCD cluster from the controlplane node?</summary>
  
     ```bash
     kubectl describe pod -n kube-system etcd-controlplane
     ```

     </details>

4. <details>
    <summary>Where is the ETCD server certificate file located?</summary>
  
     ```bash
     kubectl describe pod -n kube-system etcd-controlplane
     ```

     </details>

5. <details>
    <summary>Where is the ETCD CA Certificate file located?</summary>
  
     ```bash
     kubectl describe pod -n kube-system etcd-controlplane
     ```

     </details>

> H
6. <details>
    <summary>Where is the ETCD CA Certificate file located?</summary>
  
     ```bash
     # --listen-client-urls=https://127.0.0.1:2379,https://10.38.95.9:2379
     # --peer-trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt
     # --cert-file=/etc/kubernetes/pki/etcd/server.crt
     # --key-file=/etc/kubernetes/pki/etcd/server.key
     # backup file at location
     ETCDCTL_API=3 etcdctl snapshot save \
     --cacert=/etc/kubernetes/pki/etcd/ca.crt \
     --cert=/etc/kubernetes/pki/etcd/server.crt \
     --key=/etc/kubernetes/pki/etcd/server.key \
     /opt/snapshot-pre-boot.db
     ```

     </details>

8. <details>
    <summary>Wake up! We have a conference call! After the reboot the master nodes came back online, but none of our applications are accessible. Check the status of the applications on the cluster. What's wrong?</summary>
  
     ```bash
     k get deploy
     k get pods
     k get svc 
     ```

     </details>

> H
9. <details>
    <summary>Luckily we took a backup. Restore the original state of the cluster using the backup file.</summary>
  
     ```bash
     ETCDCTL_API=3 etcdctl snapshot restore \
     --data-dir /var/lib/etcd-from-backup \
     /opt/snapshot-pre-boot.db
     
     vi /etc/kubernetes/manifests/etcd.yaml # /var/lib/etcd-from-backup
     kubectl get deployments
     kubectl get services
     ```

     </details>

## Practice Test - Backup and Restore Methods2
2. <details>
    <summary>Before proceeding to the next question, explore the student-node and the clusters it has access to.</summary>
  
     ```bash
     kubectl config get-contexts
     ```

     </details>

3. <details>
    <summary>How many clusters are defined in the kubeconfig on the student-node?</summary>
  
     ```bash
     kubectl config get-contexts
     ```

     </details>

4. <details>
    <summary>How many nodes (both controlplane and worker) are part of cluster1?</summary>
  
     ```bash
     kubectl config use-context cluster1
     kubectl get nodes
     ```

     </details>

5. <details>
    <summary>What is the name of the controlplane node in cluster2?</summary>
  
     ```bash
     kubectl config use-context cluster2
     kubectl get nodes
     ```

     </details>

7. <details>
    <summary>How is ETCD configured for cluster1?</summary>
  
     ```bash
     kubectl config use-context cluster1
     kubectl get pods -n kube-system # etcd-cluster1-controlplane - Stacked ETCD
     ```

     </details>

8. <details>
    <summary>How is ETCD configured for cluster2?</summary>
  
     ```bash
     kubectl config use-context cluster2
     kubectl get pods -n kube-system # etcd-cluster2-controlplane 없음 -> External ETCD
     ```

     </details>

> N
9. <details>
    <summary>What is the IP address of the External ETCD datastore used in cluster2?</summary>
  
     ```bash
     kubectl config use-context cluster2
     kubectl get pods -n kube-system kube-apiserver-cluster2-controlplane -o yaml | grep etcd
     ```

     </details>

10. <details>
    <summary>What is the default data directory used the for ETCD datastore used in cluster1?</summary>
  
     ```bash
     kubectl config use-context cluster1
     kubectl get pods -n kube-system etcd-cluster1-controlplane -o yaml
     ```

     </details>

> H
12. <details>
    <summary>What is the default data directory used the for ETCD datastore used in cluster2?</summary>
  
     ```bash
     ssh etcd-server
     systemctl list-unit-files | grep etcd
     exit
     ```

     </details>

> HH
14. <details>
    <summary>Take a backup of etcd on cluster1 and save it on the student-node at the path /opt/cluster1.db</summary>
  
     ```bash
     ssh cluster1-controlplane
     ETCDCTL_API=3 etcdctl snapshot save \
     --cacert /etc/kubernetes/pki/etcd/ca.crt \
     --cert /etc/kubernetes/pki/etcd/server.crt \
     --key /etc/kubernetes/pki/etcd/server.key \
     cluster1.db
     
     exit
     scp cluster1-controlplane:~/cluster1.db /opt/
     ```

     </details>

> HHH
15. <details>
    <summary>Take a backup of etcd on cluster1 and save it on the student-node at the path /opt/cluster1.db</summary>
  
     ```bash
     scp /opt/cluster2.db etcd-server:~/ # Move the backup to the etcd-server node
     ssh etcd-server # Log into etcd-server node
     ls -ld /var/lib/etcd-data/
     
     # Do the restore
     ETCDCTL_API=3 etcdctl snapshot restore \
     --data-dir /var/lib/etcd-data-new \
     cluster2.db

     vi /etc/systemd/system/etcd.service

     systemctl daemon-reload
     systemctl restart etcd.service
     exit
     
     kubectl config use-context cluster2
     kubectl get all -n critical
     ```

     </details>

# Security
## Practice Test - View Certificates
1. <details>
    <summary>Identify the certificate file used for the kube-api server</summary>
  
     ```bash
     cat /etc/kubernetes/manifests/kube-apiserver.yaml
     ```

     </details>

2. <details>
    <summary>Identify the Certificate file used to authenticate kube-apiserver as a client to ETCD Server</summary>
  
     ```bash
     cat /etc/kubernetes/manifests/kube-apiserver.yaml
     ```

     </details>

3. <details>
    <summary>Identify the key used to authenticate kubeapi-server to the kubelet server</summary>
  
     ```bash
     cat /etc/kubernetes/manifests/kube-apiserver.yaml
     ```

     </details>

4. <details>
    <summary>Identify the ETCD Server Certificate used to host ETCD server</summary>
  
     ```bash
     cat /etc/kubernetes/manifests/kube-apiserver.yaml
     cat /etc/kubernetes/manifests/etcd.yaml
     ```

     </details>

5. <details>
    <summary>Identify the ETCD Server CA Root Certificate used to serve ETCD Server</summary>
  
     ```bash
     cat /etc/kubernetes/manifests/etcd.yaml
     ```

     </details>

6. <details>
    <summary>What is the Common Name (CN) configured on the Kube API Server Certificate?</summary>
  
     ```bash
     openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
     ```

     </details>

7. <details>
    <summary>What is the name of the CA who issued the Kube API Server Certificate?</summary>
  
     ```bash
     openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
     ```

     </details>

8. <details>
    <summary>Which of the below alternate names is not configured on the Kube API Server Certificate?</summary>
  
     ```bash
     openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
     ```

     </details>

9. <details>
    <summary>What is the Common Name (CN) configured on the ETCD Server certificate?</summary>
  
     ```bash
     cat /etc/kubernetes/manifests/etcd.yaml
     openssl x509 -in /etc/kubernetes/pki/etcd/server.crt -text -noout
     ```

     </details>

10. <details>
    <summary>What is the Common Name (CN) configured on the ETCD Server certificate?</summary>
  
     ```bash
     openssl x509 -in /etc/kubernetes/pki/etcd/server.crt -text -noout
     ```

     </details>

11. <details>
    <summary>How long, from the issued date, is the Root CA Certificate valid for?</summary>
  
     ```bash
     openssl x509 -in /etc/kubernetes/pki/ca.crt -text -noout
     ```

     </details>

12. <details>
    <summary>Kubectl suddenly stops responding to your commands. Check it out! Someone recently modified the /etc/kubernetes/manifests/etcd.yaml file</summary>
  
     ```bash
     kubectl get pods 
     # docker ps -a | grep kube-apiserver
     # docker logs 
     # docker ps -a | grep etcd 
     cat /etc/kubernetes/manifests/etcd.yaml | grep server-certificate.crt
     vi /etc/kubernetes/manifests/etcd.yaml
     # docker ps -a | grep etcd 
     # docker logs 
     # kubectl get pods 
     # docker ps -a | grep kube-api
     ```

     </details>

> H
13. <details>
    <summary>The kube-api server stopped again! Check it out. Inspect the kube-api server logs and identify the root cause and fix the issue.</summary>
  
     ```bash
     kubectl get nodes
     crictl ps -a
     crictl logs container-id dbb9d35b819b9 
     cat /etc/kubernetes/manifests/kube-apiserver.yaml
     cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep "\-\-etcd"
     vi /etc/kubernetes/manifests/kube-apiserver.yaml
     crictl ps -a
     k get nodes 
     ```
   
     </details>

## Practice Test - Certificates API
1. <details>
   <summary>A new member akshay joined our team. He requires access to our cluster. The Certificate Signing Request is at the /root location.</summary>
  
   ```bash
   pwd
   ls -l /root 
   ```
  
   </details>

> H
2. <details>
   <summary>Create a CertificateSigningRequest object with the name akshay with the contents of the akshay.csr file</summary>
  
   ```bash
   cat > akshay.yaml {링크} # https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/
   cat akshay.yaml  
   cat  akshay.csr | base64 -w 0
   vi akshay.yaml
   kubectl create -f akshay.yaml
   kubectl get csr
   ```
  
   </details>

3. <details>
   <summary>What is the Condition of the newly created Certificate Signing Request object?</summary>
  
   ```bash
   kubectl get csr
   ```
  
   </details>

4. <details>
   <summary>Approve the CSR Request</summary>
  
   ```bash
   kubectl certificate approve akshay
   kubectl get csr
   ```
  
   </details>

5. <details>
   <summary>How many CSR requests are available on the cluster?</summary>
  
   ```bash
   kubectl get csr
   ```
  
   </details>

6. <details>
   <summary>During a routine check you realized that there is a new CSR request in place. What is the name of this request?</summary>
  
   ```bash
   kubectl get csr
   ```
  
   </details>

7. <details>
   <summary>Hmmm.. You are not aware of a request coming in. What groups is this CSR requesting access to?</summary>
  
   ```bash
   kubectl get csr agent-smith -o yaml
   ```
  
   </details>

8. <details>
   <summary>That doesn't look very right. Reject that request.</summary>
  
   ```bash
   kubectl certificate deny agent-smith
   ```
  
   </details>

9. <details>
   <summary>Let's get rid of it. Delete the new CSR object</summary>
  
   ```bash
   kubectl delete csr agent-smith
   ```
  
   </details>

## Practice Test - KubeConfig
1. <details>
   <summary>Where is the default kubeconfig file located in the current environment?</summary>
  
   ```bash
   echo %HOME
   pwd
   ls -l /root/.kube
   ls .kube/config
   cat .kube/config
   ```
  
   </details>

2. <details>
   <summary>How many clusters are defined in the default kubeconfig file?</summary>
  
   ```bash
   kubectl config view
   ```
  
   </details>

3. <details>
   <summary>How many Users are defined in the default kubeconfig file?</summary>
  
   ```bash
   kubectl config view
   ```
  
   </details>

4. <details>
   <summary>How many contexts are defined in the default kubeconfig file?</summary>
  
   ```bash
   kubectl config view
   ```
  
   </details>

5. <details>
   <summary>What is the user configured in the current context?</summary>
  
   ```bash
   kubectl config view
   ```
  
   </details>

6. <details>
   <summary>What is the name of the cluster configured in the default kubeconfig file?</summary>
  
   ```bash
   kubectl config view
   ```
  
   </details>

7. <details>
   <summary>A new kubeconfig file named my-kube-config is created. It is placed in the /root directory. How many clusters are defined in that kubeconfig file?</summary>
  
   ```bash
   # cat /root/my-kube-config
   kubectl config view --kubeconfig my-kube-config
   ```
  
   </details>

8. <details>
   <summary>How many contexts are configured in the my-kube-config file?</summary>
  
   ```bash
   kubectl config view --kubeconfig my-kube-config
   ```
  
   </details>

9. <details>
   <summary>What user is configured in the research context?</summary>
  
   ```bash
   kubectl config view --kubeconfig my-kube-config
   ```
  
   </details>

10. <details>
    <summary>What is the name of the client-certificate file configured for the aws-user?</summary>
  
    ```bash
    kubectl config view --kubeconfig my-kube-config
    ```
  
    </details>

11. <details>
    <summary>What is the current context set to in the my-kube-config file?</summary>
  
    ```bash
    kubectl config view --kubeconfig my-kube-config
    ```
  
    </details>

12. <details>
    <summary>I would like to use the dev-user to access test-cluster-1. Set the current context to the right one so I can do that.</summary>
  
    ```bash
    # kubectl config --kubeconfig=/root/my-kube-config use-context research
    kubectl config use-context research --kubeconfig=/root/my-kube-config
    ```
  
    </details>

> H
13. <details>
    <summary>We don't want to have to specify the kubeconfig file option on each command. Make the my-kube-config file the default kubeconfig.</summary>
  
    ```bash
    # mv .kube/config .kube/config.bak $ cp /root/my-kube-config .kube/config
    mv /root/my-kube-config /root/.kube/config
    ```
  
    </details>

14. <details>
    <summary>With the current-context set to research, we are trying to access the cluster. However something seems to be wrong. Identify and fix the issue.</summary>
  
    ```bash
    kubectl get nodes 
    cat /root/.kube/config
    ls /etc/kubernetes/pki/users/dev-user
    vi /root/.kube/config # dev-user.crt
    kubectl get nodes
    ```
  
    </details>

## Practice Test - RBAC
1. <details>
   <summary>Inspect the environment and identify the authorization modes configured on the cluster.</summary>
  
   ```bash
   # kubectl describe pod kube-apiserver-master -n kube-system
   cat /etc/kubernetes/manifests/kube-apiserver.yaml
   ps -aux | grep authorization
   ```
  
   </details>

2. <details>
   <summary>How many roles exist in the default namespace?</summary>
  
   ```bash
   k get roles 
   ```
  
   </details>

3. <details>
   <summary>How many roles exist in all namespaces together?</summary>
  
   ```bash
   # kubectl get roles --all-namespaces
   k get roles -A --no-headers | wc -l
   ```
  
   </details>

4. <details>
   <summary>What are the resources the kube-proxy role in the kube-system namespace is given access to?</summary>
  
   ```bash
   kubectl describe role kube-proxy -n kube-system
   ```
  
   </details>

5. <details>
   <summary>What actions can the kube-proxy role perform on configmaps?</summary>
  
   ```bash
   kubectl describe role kube-proxy -n kube-system
   ```
  
   </details>

6. <details>
   <summary>Which of the following statements are true?</summary>
  
   ```bash
   kubectl describe role kube-proxy -n kube-system
   ```
  
   </details>

7. <details>
   <summary>Which account is the kube-proxy role assigned to?</summary>
  
   ```bash
   k get rolebinding -n kube-system
   k describe rolebinding kube-proxy -n kube-system
   ```
  
   </details>

8. <details>
   <summary>A user dev-user is created. User's details have been added to the kubeconfig file. Inspect the permissions granted to the user. Check if the user can list pods in the default namespace.</summary>
  
   ```bash
   kubectl config view
   k get pods --as dev-user 
   ```
  
   </details>

> H
9. <details>
   <summary>Create the necessary roles and role bindings required for the dev-user to create, list and delete pods in the default namespace.</summary>
  
   ```bash
   k create role developer --verb=list,create,delete --resource=pods
   k describe role developer
   k create rolebinding --help
   k create rolebinding dev-user-binding --role=developer --user=dev-user
   k describe rolebinding dev-user-binding
   ```
  
   </details>

> H
10. <details>
    <summary>A set of new roles and role-bindings are created in the blue namespace for the dev-user. However, the dev-user is unable to get details of the dark-blue-app pod in the blue namespace. Investigate and fix the issue.</summary>
  
    ```bash
    k --as dev-user get pods dark-blue-app -n blue 
    k get roles -n blue
    k get rolebinding -n blue 
    k describe role developer -n blue 
    k edit role developer -n blue # dark-blue-app
    k --as dev-user get pods dark-blue-app -n blue 
    ```
  
    </details>

> H
11. <details>
    <summary>Add a new rule in the existing role developer to grant the dev-user permissions to create deployments in the blue namespace.</summary>
  
    ```bash
    k --as dev-user create deployment nginx --image=nginx -n blue
    k edit role developer -n blue # apps 추가 
    k describe role developer -n blue 
    k --as dev-user create deployment nginx --image=nginx -n blue
    ```
  
    </details>

## Practice Test - Cluster Roles
2. <details>
    <summary>How many ClusterRoles do you see defined in the cluster?</summary>
  
    ```bash
    k get clusterroles --no-headers | wc -l
    ```
  
    </details>

3. <details>
    <summary>How many ClusterRoleBindings exist on the cluster?</summary>
  
    ```bash
    k get clusterrolebindings --no-headers | wc -l
    ```
  
    </details>

4. <details>
    <summary>What namespace is the cluster-admin clusterrole part of?</summary>
  
    ```bash
    k get clusterroles
    ```
  
    </details>

5. <details>
    <summary>What user/groups are the cluster-admin role bound to?</summary>
  
    ```bash
    k get clusterrolebindings | grep cluster-admin
    k describe clusterrolebindings cluster-admin
    k describe clusterrolebindings helm-kube-system-traefik-crd
    ```
  
    </details>

6. <details>
    <summary>What level of permission does the cluster-admin role grant?</summary>
  
    ```bash
    k describe clusterrole cluster-admin
    ```
  
    </details>

> H
7. <details>
    <summary>A new user michelle joined the team. She will be focusing on the nodes in the cluster. Create the required ClusterRoles and ClusterRoleBindings so she gets access to the nodes.</summary>
  
    ```bash
    kubectl create clusterrole michelle-role --verb=get,list,watch --resource=nodes
    kubectl create clusterrolebinding michelle-role-binding --clusterrole=michelle-role --user=michelle
    k describe clusterrole michelle-role
    k describe clusterrolebindings michelle-role-binding
    k get nodes --as michelle
    ```
  
    </details>

> H
8. <details>
    <summary>michelle's responsibilities are growing and now she will be responsible for storage as well. Create the required ClusterRoles and ClusterRoleBindings to allow her access to Storage.</summary>
  
    ```bash
    kubectl api-resources
    k create clusterrole storage-admin --resource=persistentvolumes,storageclasses --verb=list,create,get,watch
    k describe clusterrole storage-admin
    k get clusterrole storage-admin -o yaml
    k create clusterrolebinding michelle-storage-admin --user=michelle --clusterrole=storage-admin
    k describe clusterrolebindings michelle-storage-admin
    k --as michelle get storageclass
    ```
  
    </details>

## Practice Test - Service Accounts
1. <details>
    <summary>How many Service Accounts exist in the default namespace?</summary>
  
    ```bash
    kubectl get serviceaccounts
    ```
  
    </details>

2. <details>
    <summary>What is the secret token used by the default service account?</summary>
  
    ```bash
    kubectl describe serviceaccount default
    ```
  
    </details>

3. <details>
    <summary>We just deployed the Dashboard application. Inspect the deployment. What is the image used by the deployment?</summary>
  
    ```bash
    kubectl describe deployment
    ```
  
    </details>

7. <details>
    <summary>Which account does the Dashboard application use to query the Kubernetes API?</summary>
  
    ```bash
    kubectl get po -o yaml | grep -i serviceaccount
    ```
  
    </details>

8. <details>
    <summary>Inspect the Dashboard Application POD and identify the Service Account mounted on it.</summary>
  
    ```bash
    kubectl describe pod
    ```
  
    </details>

9. <details>
    <summary>At what location is the ServiceAccount credentials available within the pod?</summary>
  
    ```bash
    kubectl describe pod
    ```
  
    </details>

10. <details>
    <summary>The application needs a ServiceAccount with the Right permissions to be created to authenticate to Kubernetes. The default ServiceAccount has limited access. Create a new ServiceAccount named dashboard-sa.</summary>
  
    ```bash
    kubectl create serviceaccount dashboard-sa
    ```
  
    </details>

11. <details>
    <summary>You shouldn't have to copy and paste the token each time. The Dashboard application is programmed to read token from the secret mount location. However currently, the default service account is mounted. Update the deployment to use the newly created ServiceAccount</summary>
  
    ```bash
    # kubectl create token dashboard-sa
    kubectl edit deploy web-dashboard # serviceAccountName: dashboard-sa
    ```
  
    </details>

## Practice Test - Image Security
1. <details>
    <summary>What secret type must we choose for docker registry?</summary>
  
    ```bash
    kubectl create secret
    ```
  
    </details>

2. <details>
    <summary>We have an application running on our cluster. Let us explore it first. What image is the application using?</summary>
  
    ```bash
    kubectl get deploy -o wide
    k describe deploy web
    ```
  
    </details>

3. <details>
    <summary>We decided to use a modified version of the application from an internal private registry. Update the image of the deployment to use a new image from myprivateregistry.com:5000</summary>
  
    ```bash
    k edit deployment web 
    k describe deploy web
    ```
  
    </details>

4. <details>
    <summary>Are the new PODs created with the new images successfully running?</summary>
  
    ```bash
    k get pods
    k describe pod web-87bb989dc-5bkzt
    ```
  
    </details>

5. <details>
    <summary>Create a secret object with the credentials required to access the registry.</summary>
  
    ```bash
    k create secret docker-registry private-reg-cred --docker-username=dock_user --docker-password=dock_password --docker-server=myprivateregistry.com:5000 --docker-email=dock_user@myprivateregistry.com
    ```
  
    </details>

> N
6. <details>
    <summary>Configure the deployment to use credentials from the new secret to pull images from the private registry</summary>
  
    ```bash
    k edit deploy web # https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ 
    # imagePullSecrets:  - name: private-reg-cred
    k describe deploy web
    ```
  
    </details>

## Practice Test - Security Context
1. <details>
    <summary>What is the user used to execute the sleep process within the ubuntu-sleeper pod?</summary>
  
    ```bash
    k exec ubuntu-sleeper -- whoami
    ```
  
    </details>

> N
2. <details>
    <summary>Edit the pod ubuntu-sleeper to run the sleep process with user ID 1010.</summary>
  
    ```bash
    # https://kubernetes.io/docs/tasks/configure-pod-container/security-context/
    k edit pod ubuntu-sleeper # securityContext : \ runAsUser: 1010
    k replace --force -f /tmp/kubectl-edit-1786819119.yaml
    k exec ubuntu-sleeper -- whoami
    ```
  
    </details>

3. <details>
    <summary>A Pod definition file named multi-pod.yaml is given. With what user are the processes in the web container started?</summary>
  
    ```bash
    cat multi-pod.yaml
    ```
  
    </details>

4. <details>
    <summary>With what user are the processes in the sidecar container started?</summary>
  
    ```bash
    cat multi-pod.yaml
    ```
  
    </details>

> H
5. <details>
    <summary>Update pod ubuntu-sleeper to run as Root user and with the SYS_TIME capability.</summary>
  
    ```bash
    # https://kubernetes.io/docs/tasks/configure-pod-container/security-context/
    k edit pod ubuntu-sleeper # capabilities:        add: ["SYS_TIME"]
    k replace --force -f /tmp/kubectl-edit-79364768.yaml
    ```
  
    </details>

6. <details>
    <summary>Now update the pod to also make use of the NET_ADMIN capability.</summary>
  
    ```bash
    # https://kubernetes.io/docs/tasks/configure-pod-container/security-context/
    k edit pod ubuntu-sleeper # capabilities:        add: ["NET_ADMIN", "SYS_TIME"]
    k replace --force -f /tmp/kubectl-edit-2192387685.yaml
    ```
  
    </details>

# Practice Test - Network Policies
1. <details>
    <summary>How many network policies do you see in the environment?</summary>
  
    ```bash
    kubectl get networkpolicy
    k get netpol
    ```
  
    </details>

2. <details>
    <summary>What is the name of the Network Policy?</summary>
  
    ```bash
    k get netpol
    ```
  
    </details>

3. <details>
    <summary>Which pod is the Network Policy applied on?</summary>
  
    ```bash
    k get netpol
    ```
  
    </details>

4. <details>
    <summary>What type of traffic is this Network Policy configured to handle?</summary>
  
    ```bash
    k describe networkpolicy
    ```
  
    </details>

5. <details>
    <summary>What is the impact of the rule configured on this Network Policy?</summary>
  
    ```bash
    k describe networkpolicy
    ```
  
    </details>

6. <details>
    <summary>What is the impact of the rule configured on this Network Policy?</summary>
  
    ```bash
    k describe networkpolicy
    ```
  
    </details>

> H
10. <details>
    <summary>Create a network policy to allow traffic from the Internal application only to the payroll-service and db-service.</summary>
  
    ```bash
    # https://kubernetes.io/docs/concepts/services-networking/network-policies/
    vi internal-policy.yaml
    k create -f internal-policy.yaml
    k describe netpol internal-policy 
    ```
  
    </details>

# Storage
## Practice Test - Persistent Volume Claims
1. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pods
    ```
  
    </details>

2. <details>
    <summary>Create a </summary>
  
    ```bash
    k exec webapp --cat /log/app.log
    ```
  
    </details>

3. <details>
    <summary>Create a </summary>
  
    ```bash
    k describe webapp 
    ```
  
    </details>

4. <details>
    <summary>Create a </summary>
  
    ```bash
    ls /var/log/webapp 
    k edit pod webapp # name:log-volume, hstPath: path: /var/log/webapp, type: Directory / nmae: loge-volume
    k replace --force -f .yaml    
    cd /var/log/webapp 
    cat app.log
    ```
  
    </details>

5. <details>
    <summary>Create a </summary>
  
    ```bash
    # https://kubernetes.io/docs/concepts/storage/persistent-volumes/
    cd ~ 
    vi pv.yaml
    k create -f pv.yaml 
    k get pv
    ```
  
    </details>

6. <details>
    <summary>Create a </summary>
  
    ```bash
    # https://kubernetes.io/docs/concepts/storage/persistent-volumes/
    vi pvc.yaml
    k create -f pvc.yaml 
    k get pvc
    ```
  
    </details>

7. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pvc
    ```
  
    </details>

8. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pv
    ```
  
    </details>

9. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pv
    cat pv.yaml 
    cat pvc.yaml 
    ```
  
    </details>

10. <details>
    <summary>Create a </summary>
  
    ```bash
    vi pvc.yaml 
    k replace --force -f pvc.yaml    
    ```
  
    </details>

11. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pv
    k get pvc 
    ```
  
    </details>


12. <details>
    <summary>Create a </summary>
  
    ```bash
    # https://kubernetes.io/docs/concepts/storage/persistent-volumes/
    k edit pod webapp 
    k replace --force -f .yaml
    cat /pv/log/app.log
    ```
  
    </details>

13. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pv pv-log
    ```
  
    </details>

14. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pv pv-log
    ```
  
    </details>

15. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pvc
    k delete pvc claim-log-1
    k get pvc 
    ```
  
    </details>

16. <details>
    <summary>Create a </summary>
  
    ```bash
    k describe pvc claim-log-1
    ```
  
    </details>

17. <details>
    <summary>Create a </summary>
  
    ```bash
    k delete pod webapp
    ```
  
    </details>

18. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pvc 
    ```
  
    </details>

19. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pv 
    ```
  
    </details>

## Practice Test - Storage Class
1. <details>
    <summary>Create a </summary>
  
    ```bash
    k get storageclass
    k get sc 
    ```
  
    </details>

2. <details>
    <summary>Create a </summary>
  
    ```bash
    k get sc 
    ```
  
    </details>

6. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pv
    k get pvc
    ```
  
    </details>

7. <details>
    <summary>Create a </summary>
  
    ```bash
    # https://kubernetes.io/docs/concepts/storage/persistent-volumes/
    vi pvc.yaml 
    k create -f pvc.yaml
    k get pvc 
    ```
  
    </details>

8. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pvc 
    ```
  
    </details>

9. <details>
    <summary>Create a </summary>
  
    ```bash
    k describe pvc local-pvc 
    ```
  
    </details>

11. <details>
    <summary>Create a </summary>
  
    ```bash
    k run nginx --image=ngix:alpine --dry-run=client -o yaml
    k run nginx --image=ngix:alpine --dry-run=client -o yaml > nginx.yaml
    k create -f nginx.yaml
    k get pod
    ```
  
    </details>

12. <details>
    <summary>Create a </summary>
  
    ```bash
    k get pvc
    ```
  
    </details>

> N
13. <details>
    <summary>Create a </summary>
  
    ```bash
    # https://kubernetes.io/docs/concepts/storage/storage-classes/
    vi delayed-volume-sc.yaml
    k create -f delayed-volume-sc.yaml
    k get sc 
    ```
  
    </details>

