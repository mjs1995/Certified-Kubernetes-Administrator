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
[Day17-Explore Env](#practice-test---explore-env)<br>
[Day18-CNI weave](#practice-test---cni-weave)<br>
[Day18-Deploy Networking Solution](#practice-test---deploy-networking-solution)<br>
[Day18-Networking Weave](#practice-test---networking-weave)<br>
[Day18-Service Networking](#practice-test---service-networking)<br>
[Day19-CoreDNS in Kubernetes](#practice-test---coredns-in-kubernetes)<br>
[Day19-Ingress Networking 1](#practice-test---ingress-networking-1)<br>
[Day20-Ingress Networking 2](#practice-test---ingress-networking-2)<br>
[Day21-Install kubernetes cluster using kubeadm tool](#practice-test---install-kubernetes-cluster-using-kubeadm-tool)<br>
[Day21-Application Failure](#practice-test---application-failure)<br>
[Day22-Control Plane Failure](#practice-test---control-plane-failure)<br>
[Day22-Worker Node Failure](#practice-test---worker-node-failure)<br>
[Day22-Troubleshoot Network](#practice-test---troubleshoot-network)<br>
[Day22-Advance Kubectl Commands](#practice-test---advance-kubectl-commands)<br>
[Day22-Lightning Lab1](#practice-test---lightning-lab1)<br>
[Day23-Mock Exam - 1](#mock-exam---1)<br>
[Day24-Mock Exam - 2](#mock-exam---2)<br>

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
    <summary>We have deployed a POD. Inspect the POD and wait for it to start running. </summary>
  
    ```bash
    k get pods
    ```
  
    </details>

2. <details>
    <summary>The application stores logs at location /log/app.log. View the logs. </summary>
  
    ```bash
    k exec webapp --cat /log/app.log
    ```
  
    </details>

3. <details>
    <summary>If the POD was to get deleted now, would you be able to view these logs. </summary>
  
    ```bash
    k describe webapp 
    ```
  
    </details>

4. <details>
    <summary>Configure a volume to store these logs at /var/log/webapp on the host. </summary>
  
    ```bash
    ls /var/log/webapp 
    k edit pod webapp # name:log-volume, hstPath: path: /var/log/webapp, type: Directory / nmae: loge-volume
    k replace --force -f .yaml    
    cd /var/log/webapp 
    cat app.log
    ```
  
    </details>

5. <details>
    <summary>Create a Persistent Volume with the given specification. </summary>
  
    ```bash
    # https://kubernetes.io/docs/concepts/storage/persistent-volumes/
    cd ~ 
    vi pv.yaml
    k create -f pv.yaml 
    k get pv
    ```
  
    </details>

6. <details>
    <summary>Let us claim some of that storage for our application. Create a Persistent Volume Claim with the given specification. </summary>
  
    ```bash
    # https://kubernetes.io/docs/concepts/storage/persistent-volumes/
    vi pvc.yaml
    k create -f pvc.yaml 
    k get pvc
    ```
  
    </details>

7. <details>
    <summary>What is the state of the Persistent Volume Claim? </summary>
  
    ```bash
    k get pvc
    ```
  
    </details>

8. <details>
    <summary>What is the state of the Persistent Volume? </summary>
  
    ```bash
    k get pv
    ```
  
    </details>

9. <details>
    <summary>Why is the claim not bound to the available Persistent Volume? </summary>
  
    ```bash
    k get pv
    cat pv.yaml 
    cat pvc.yaml 
    ```
  
    </details>

10. <details>
    <summary>Update the Access Mode on the claim to bind it to the PV. </summary>
  
    ```bash
    vi pvc.yaml 
    k replace --force -f pvc.yaml    
    ```
  
    </details>

11. <details>
    <summary>You requested for 50Mi, how much capacity is now available to the PVC?</summary>
  
    ```bash
    k get pv
    k get pvc 
    ```
  
    </details>


12. <details>
    <summary>Update the webapp pod to use the persistent volume claim as its storage. </summary>
  
    ```bash
    # https://kubernetes.io/docs/concepts/storage/persistent-volumes/
    k edit pod webapp 
    k replace --force -f .yaml
    cat /pv/log/app.log
    ```
  
    </details>

13. <details>
    <summary>What is the Reclaim Policy set on the Persistent Volume pv-log? </summary>
  
    ```bash
    k get pv pv-log
    ```
  
    </details>

14. <details>
    <summary>What would happen to the PV if the PVC was destroyed? </summary>
  
    ```bash
    k get pv pv-log
    ```
  
    </details>

15. <details>
    <summary>Try deleting the PVC and notice what happens. </summary>
  
    ```bash
    k get pvc
    k delete pvc claim-log-1
    k get pvc 
    ```
  
    </details>

16. <details>
    <summary>Why is the PVC stuck in Terminating state?</summary>
  
    ```bash
    k describe pvc claim-log-1
    ```
  
    </details>

17. <details>
    <summary>Let us now delete the webapp Pod. </summary>
  
    ```bash
    k delete pod webapp
    ```
  
    </details>

18. <details>
    <summary>What is the state of the PVC now?</summary>
  
    ```bash
    k get pvc 
    ```
  
    </details>

19. <details>
    <summary>What is the state of the Persistent Volume now?</summary>
  
    ```bash
    k get pv 
    ```
  
    </details>

## Practice Test - Storage Class
1. <details>
    <summary>How many StorageClasses exist in the cluster right now? </summary>
  
    ```bash
    k get storageclass
    k get sc 
    ```
  
    </details>

2. <details>
    <summary>How about now? How many Storage Classes exist in the cluster? </summary>
  
    ```bash
    k get sc 
    ```
  
    </details>

6. <details>
    <summary>Let's fix that. Create a new PersistentVolumeClaim by the name of local-pvc that should bind to the volume local-pv. </summary>
  
    ```bash
    k get pv
    k get pvc
    ```
  
    </details>

7. <details>
    <summary>Let's fix that. Create a new PersistentVolumeClaim by the name of local-pvc that should bind to the volume local-pv. </summary>
  
    ```bash
    # https://kubernetes.io/docs/concepts/storage/persistent-volumes/
    vi pvc.yaml 
    k create -f pvc.yaml
    k get pvc 
    ```
  
    </details>

8. <details>
    <summary>What is the status of the newly created Persistent Volume Claim?</summary>
  
    ```bash
    k get pvc 
    ```
  
    </details>

9. <details>
    <summary>Why is the PVC in a pending state despite making a valid request to claim the volume called local-pv?</summary>
  
    ```bash
    k describe pvc local-pvc 
    ```
  
    </details>

11. <details>
    <summary>Create a new pod called nginx with the image nginx:alpine. The Pod should make use of the PVC local-pvc and mount the volume at the path /var/www/html. </summary>
  
    ```bash
    k run nginx --image=ngix:alpine --dry-run=client -o yaml
    k run nginx --image=ngix:alpine --dry-run=client -o yaml > nginx.yaml
    k create -f nginx.yaml
    k get pod
    ```
  
    </details>

12. <details>
    <summary>What is the status of the local-pvc Persistent Volume Claim now? </summary>
  
    ```bash
    k get pvc
    ```
  
    </details>

> N
13. <details>
    <summary>Create a new Storage Class called delayed-volume-sc that makes use of the below specs: </summary>
  
    ```bash
    # https://kubernetes.io/docs/concepts/storage/storage-classes/
    vi delayed-volume-sc.yaml
    k create -f delayed-volume-sc.yaml
    k get sc 
    ```
  
    </details>

# Networking
## Practice Test - Explore Env
1. <details>
    <summary>How many nodes are part of this cluster? </summary>
  
    ```bash
    k get nodes
    ```
  
    </details>

2. <details>
    <summary>What is the Internal IP address of the controlplane node in this cluster? </summary>
  
    ```bash
    ifconfig -a 
    cat /etc/network/interfaces
    ifconfig eth0
    ```
  
4. <details>
    <summary>What is the MAC address of the interface on the controlplane node? </summary>
  
    ```bash
    ip link
    ```

    </details>

5. <details>
    <summary>What is the IP address assigned to node01? </summary>
  
    ```bash
    ssh node01 ifconfig eth0
    ```

    </details>

6. <details>
    <summary>What is the MAC address assigned to node01? </summary>
  
    ```bash
    ssh node01 ifconfig eth0
    ```

    </details>

8. <details>
    <summary>What is the state of the interface cni0? </summary>
  
    ```bash
    ssh node01 ip link
    ```

    </details>

9. <details>
    <summary>If you were to ping google from the controlplane node, which route does it take? </summary>
  
    ```bash
    ip r
    ```

    </details>

10. <details>
    <summary>What is the port the kube-scheduler is listening on in the controlplane node? </summary>
  
    ```bash
    netstat -natulp |grep kube-scheduler
    ```

    </details>

11. <details>
    <summary>Notice that ETCD is listening on two ports. Which of these have more client connections established? </summary>
  
    ```bash
    netstat -natulp |grep etcd | grep LISTEN
    ```

    </details>

## Practice Test - CNI weave
1. <details>
    <summary>Inspect the kubelet service and identify the container runtime endpoint value is set for Kubernetes. </summary>
  
    ```bash
    ps aux | grep kubelet 
    ```

    </details>

2. <details>
    <summary>What is the path configured with all binaries of CNI supported plugins? </summary>
  
    ```bash
    ls /opt/cni/bin/
    ```

    </details>

3. <details>
    <summary>Identify which of the below plugins is not available in the list of available CNI plugins on this host? </summary>
  
    ```bash
    ls /opt/cni/bin/
    ```

    </details>

4. <details>
    <summary>What is the CNI plugin configured to be used on this kubernetes cluster? </summary>
  
    ```bash
    ls /etc/cni/net.d/
    ```

    </details>

5. <details>
    <summary>What is the CNI plugin configured to be used on this kubernetes cluster? </summary>
  
    ```bash
    cat /etc/cni/net.d/10-flannel.conflist
    ```

    </details>

## Practice Test - Deploy Networking Solution
1. <details>
    <summary>In this practice test we will install weave-net POD networking solution to the cluster. Let us first inspect the setup. </summary>
  
    ```bash
    k get pods 
    ```

    </details>

2. <details>
    <summary>Inspect why the POD is not running. </summary>
  
    ```bash
    k describe pod app
    ```

    </details>

> H
3. <details>
    <summary>Deploy weave-net networking solution to the cluster. </summary>
  
    ```bash
    # https://www.weave.works/docs/net/latest/kubernetes/kube-addon/#-installation
    kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
    kubectl apply -f /root/weave/weave-daemonset-k8s.yaml
    k get pods -n kube-system
    ```

    </details>

## Practice Test - Networking Weave
1. <details>
    <summary>How many Nodes are part of this cluster? </summary>
  
    ```bash
    k get nodes
    ```

    </details>

2. <details>
    <summary>What is the Networking Solution used by this cluster? </summary>
  
    ```bash
    ps aux | grep kubelet
    ls /etc/cni/net.d/10-weave.conflist 
    ```

    </details>

3. <details>
    <summary>What is the Networking Solution used by this cluster? </summary>
  
    ```bash
    k get pods -n kube-system
    ```

    </details>

4. <details>
    <summary>On which nodes are the weave peers present? </summary>
  
    ```bash
    k get pods -n kube-system -o wide
    ```

    </details>

5. <details>
    <summary>Identify the name of the bridge network/interface created by weave on each node. </summary>
  
    ```bash
    ip link 
    ssh node01
    ip link 
    ```

6. <details>
    <summary>What is the POD IP address range configured by weave? </summary>
  
    ```bash
    k get pods -n kube-system
    k logs -n kube-system weave-net-mvrw7 weave
    ```

    </details>

> H
7. <details>
    <summary>What is the default gateway configured on the PODs scheduled on node01? </summary>
  
    ```bash
    k run busybox --image=busybox --dry-run=client -o yaml -- sleep 1000
    k run busybox --image=busybox --dry-run=client -o yaml -- sleep 1000 > busybox.yaml
    vi busybox.yaml 
    k create -f busybox.yaml 
    k get pod -o wide 
    k exec busybox -- route -n 
    k exec busybox -- ip route
    ```

    </details>

## Practice Test - Service Networking
1. <details>
    <summary>What network range are the nodes in the cluster part of? </summary>
  
    ```bash
    k get nodes -o wide 
    ip a 
    ```

    </details>

2. <details>
    <summary>What is the range of IP addresses configured for PODs on this cluster? </summary>
  
    ```bash
    k -n kube-system get pods 
    k -n kube-system logs weave-net-9m99f -c weave
    ```

    </details>

3. <details>
    <summary>What is the IP Range configured for the services within the cluster? </summary>
  
    ```bash
    cd /etc/kubernetes/manifests/
    cat kube-apiserver.yaml 
    ```

    </details>

4. <details>
    <summary>How many kube-proxy pods are deployed in this cluster? </summary>
  
    ```bash
    k -n kube-system get pods 
    ```

    </details>

5. <details>
    <summary>What type of proxy is the kube-proxy configured to use? </summary>
  
    ```bash
    k -n kube-system get pods
    k -n kube-system logs kube-proxy-5l84j
    ```

    </details>

> N
6. <details>
    <summary>How does this Kubernetes cluster ensure that a kube-proxy pod runs on all nodes in the cluster? </summary>
  
    ```bash
    k -n kube-system get ds 
    ```

    </details>

## Practice Test - CoreDNS in Kubernetes
1. <details>
    <summary>Identify the DNS solution implemented in this cluster. </summary>
  
    ```bash
    k get pods -n kube-system
    ```
   
    </details>

2. <details>
    <summary>How many pods of the DNS server are deployed? </summary>
  
    ```bash
    k get pods -n kube-system
    ```
   
    </details>

3. <details>
    <summary>What is the name of the service created for accessing CoreDNS? </summary>
  
    ```bash
    k get svc -n kube-system
    ```
   
    </details>

4. <details>
    <summary>What is the IP of the CoreDNS server that should be configured on PODs to resolve services? </summary>
  
    ```bash
    k get svc -n kube-system
    ```
   
    </details>

5. <details>
    <summary>Where is the configuration file located for configuring the CoreDNS service? </summary>
  
    ```bash
    k get pods -n kube-system
    k describe pod coredns-787d4945fb-42xp9 -n kube-system
    ```
   
    </details>

6. <details>
    <summary>How is the Corefile passed into the CoreDNS POD? </summary>
  
    ```bash
    k get pods -n kube-system
    k describe pod coredns-787d4945fb-42xp9 -n kube-system
    k get pod coredns-787d4945fb-42xp9 -n kube-system -o yaml
    ```
   
    </details>

7. <details>
    <summary>What is the name of the ConfigMap object created for Corefile? </summary>
  
    ```bash
    k get pod coredns-787d4945fb-42xp9 -n kube-system -o yaml
    ```
   
    </details>

> N
8. <details>
    <summary>What is the root domain/zone configured for this kubernetes cluster? </summary>
  
    ```bash
    k get configmap -n kube-system 
    k describe configmap coredns -n kube-system
    ```
   
    </details>

9. <details>
    <summary>We have deployed a set of PODs and Services in the default and payroll namespaces. Inspect them and go to the next question. </summary>
  
    ```bash
    k get pods 
    k get pods -n payroll
    ```
   
    </details>

10. <details>
    <summary>What name can be used to access the hr web server from the test Application? </summary>
  
    ```bash
    k get svc 
    k describe svc web-service
    ```
   
    </details>

11. <details>
    <summary>Which of the names CANNOT be used to access the HR service from the test pod? </summary>
  
    ```bash
    k get svc 
    k describe svc web-service
    ```
   
    </details>

12. <details>
    <summary>Which of the below name can be used to access the payroll service from the test application? </summary>
  
    ```bash
    k get pod -n payroll
    k get svc -n payroll
    k describe svc web-service -n payroll
    ```
   
    </details>

13. <details>
    <summary>Which of the below name CANNOT be used to access the payroll service from the test application? </summary>
  
    ```bash
    k get pod -n payroll
    k get svc -n payroll
    k describe svc web-service -n payroll
    ```
   
    </details>

> H
14. <details>
    <summary>We just deployed a web server - webapp - that accesses a database mysql - server. However the web server is failing to connect to the database server. Troubleshoot and fix the issue. </summary>
  
    ```bash
    k get deploy
    k get pods -A 
    k get svc -n payroll
    k describe deploy webapp
    k edit deploy webapp # mysql.payroll
    k get pods 
    ```
   
    </details>

> H
15. <details>
    <summary>From the hr pod nslookup the mysql service and redirect the output to a file /root/CKA/nslookup.out </summary>
  
    ```bash
    k exec hr -- nslookup mysql.payroll
    k exec hr -- nslookup mysql.payroll > /root/CKA/nslookup.out
    ```
   
    </details>

## Practice Test - Ingress Networking 1
1. <details>
    <summary>We have deployed Ingress Controller, resources and applications. Explore the setup. </summary>
  
    ```bash
    k get nodes
    k get deploy 
    k get deploy -A
    k get pods -n kube-system 
    k get pods -n ingress-nginx 
    ```
   
    </details>

2. <details>
    <summary>Which namespace is the Ingress Controller deployed in? </summary>
  
    ```bash
    k get pods -A 
    ```
   
    </details>

3. <details>
    <summary>What is the name of the Ingress Controller Deployment? </summary>
  
    ```bash
    k get pods -A 
    k get deploy -n ingress-nginx
    ```
   
    </details>

4. <details>
    <summary>Which namespace are the applications deployed in? </summary>
  
    ```bash
    k get pods -A 
    ```
   
    </details>

5. <details>
    <summary>How many applications are deployed in the app-space namespace? </summary>
  
    ```bash
    k get pods -A 
    ```
   
    </details>

6. <details>
    <summary>Which namespace is the Ingress Resource deployed in? </summary>
  
    ```bash
    k get ingress -A
    ```
   
    </details>

7. <details>
    <summary>What is the name of the Ingress Resource? </summary>
  
    ```bash
    k get ingress -A
    ```
   
    </details>

8. <details>
    <summary>What is the Host configured on the Ingress Resource? </summary>
  
    ```bash
    k get ingress -A
    ```
   
    </details>

9. <details>
    <summary>What backend is the /wear path on the Ingress configured with? </summary>
  
    ```bash
    k describe ingress ingress-wear-watch -n app-space
    ```
   
    </details>

10. <details>
    <summary>At what path is the video streaming application made available on the Ingress? </summary>
  
    ```bash
    k describe ingress ingress-wear-watch -n app-space
    ```
   
    </details>

11. <details>
    <summary>If the requirement does not match any of the configured paths what service are the requests forwarded to? </summary>
  
    ```bash
    k describe ingress ingress-wear-watch -n app-space
    ```
   
    </details>

12. <details>
    <summary>Now view the Ingress Service using the tab at the top of the terminal. Which page do you see? </summary>
  
    ```bash
    k describe ingress ingress-wear-watch -n app-space
    ```
   
    </details>

14. <details>
    <summary>You are requested to change the URLs at which the applications are made available. </summary>
  
    ```bash
    k edit ingress ingress-wear-watch -n app-space
    ```
   
    </details>

16. <details>
    <summary>A user is trying to view the /eat URL on the Ingress Service. Which page would he see? </summary>
  
    ```bash
    k describe ingress ingress-wear-watch -n app-space
    ```
   
    </details>

17. <details>
    <summary>Due to increased demand, your business decides to take on a new venture. You acquired a food delivery company. Their applications have been migrated over to your cluster. </summary>
  
    ```bash
    k get deploy -n app-space 
    ```
   
    </details>

18. <details>
    <summary>You are requested to add a new path to your ingress to make the food delivery application available to your customers. </summary>
  
    ```bash
    k get svc -n app-space 
    k edit ingress ingress-wear-watch -n app-space
    ```
   
    </details>

20. <details>
    <summary>A new payment service has been introduced. Since it is critical, the new application is deployed in its own namespace. </summary>
  
    ```bash
    k get pods -A 
    k get deploy -n critical-space 
    ```
   
    </details>

21. <details>
    <summary>What is the name of the deployment of the new application? </summary>
  
    ```bash
    k get pods -A 
    k get deploy -n critical-space 
    ```
   
    </details>

> H
22. <details>
    <summary>You are requested to make the new application available at /pay. </summary>
  
    ```bash
    k get svc -n critical-space 
    k create ingress -h
    k create ingress ingress-pay -n critical-space --rule="/pay=pay-service:8282"
    k get ingress -n critical-space
    k describe ingress -n critical-space
    k get pods -n critical-space 
    k logs webapp-pay-58cdc69889-v7mk4 -n critical-space
    k edit ingress ingress-pay -n critical-space 
    # annotations:
    # nginx.ingress.kubernetes.io/rewrite-target: /
    ```
   
    </details>

## Practice Test - Ingress Networking 2
1. <details>
    <summary>We have deployed two applications. Explore the setup. </summary>
  
    ```bash
    k get pod -A 
    ```
   
    </details>

2. <details>
    <summary>Let us now deploy an Ingress Controller. First, create a namespace called ingress-nginx. </summary>
  
    ```bash
    k create namespace ingress-nginx
    ```
   
    </details>

3. <details>
    <summary>The NGINX Ingress Controller requires a ConfigMap object. Create a ConfigMap object with name ingress-nginx-controller in the ingress-nginx namespace. </summary>
  
    ```bash
    k create configmap ingress-nginx-controller -n ingress-nginx
    ```
   
    </details>

4. <details>
    <summary>The NGINX Ingress Controller requires two ServiceAccounts. Create both ServiceAccount with name ingress-nginx and ingress-nginx-admission in the ingress-nginx namespace. </summary>
  
    ```bash
    k create serviceaccount ingress-nginx -n ingress-nginx
    k create serviceaccount ingress-nginx-admission -n ingress-nginx
    ```
   
    </details>

5. <details>
    <summary>We have created the Roles and RoleBindings for the ServiceAccount. Check it out!! </summary>
  
    ```bash
    k get roles -n ingress-nginx
    k get rolebindings -n ingress-nginx
    k describe role ingress-nginx -n ingress-nginx
    ```
   
    </details>

> H
6. <details>
    <summary>Let us now deploy the Ingress Controller. Create the Kubernetes objects using the given file. </summary>
  
    ```bash
    cat ingress-controller.yaml 
    k create -f ingress-controller.yaml 
    vi ingress-controller.yaml 
    k get pods -n ingress-nginx
    k get deploy -n ingress-nginx
    k expose deploy ingress-controller -n ingress-nginx --name ingress --port=80 --target -port=80 --type NodePort 
    k get svc -n ingress-nginx 
    k edit svc ingress -n ingress-nginx # 30080
    ```
   
    </details>

> H
7. <details>
    <summary>Create the ingress resource to make the applications available at /wear and /watch on the Ingress service. </summary>
  
    ```bash
    k create ingress ingress-wear-watch -n app-space --rule="/wear=wear-service:8080" --rule="/watch=video-service:8080"
    k get svc -n app-space
    k get ingress -n app-space 
    k describe ingress -n app-space
    k get pods -n app-space
    k logs webapp-video-57cddcc65-67bzk -n app-space
    k get pods -n ingress-nginx
    k logs ingress-nginx-admission-create-kc9v6 -n ingress-nginx
    k edit ingress ingress-wear-watch -n app-space
    #annotations:
      # nginx.ingress.kubernetes.io/rewrite-target: /
      # nginx.ingress.kubernetes.io/ssl-redirect: "false"
    ```
   
    </details>

# Install
## Practice Test - Install kubernetes cluster using kubeadm tool
> H
1. <details>
    <summary>Install the kubeadm and kubelet packages on the controlplane and node01. </summary>
  
    ```bash
    # https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
    ssh node01
    exit 
    ip addr 
    sudo cat /sys/class/dmi/id/product_uuid
    ssh node01
    ip addr 
    sudo cat /sys/class/dmi/id/product_uuid
    exit
    ping node01 
    
    # Letting iptable see bridged traffic
    cat <<EOF | tee /etc/modules-load.d/k8s.conf
    br_netfilter
    EOF
   
    cat <<EOF | tee /etc/sysctl.d/k8s.conf
    net.bridge.bridge-nf-call-ip6tables = 1
    net.bridge.bridge-nf-call-iptables = 1
    EOF
    sysctl --system
   
    clear
    docker ps 
    service docker status
    
    cat /etc/*release*
    sudo apt-get update 
    sudo apt-get install -y apt-transport-https ca-certificates curl
    sudo curl -fsSLo /etc/apt/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg

    echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
    
    sudo apt-get update
    sudo apt-get install -y kubelet=1.26.0-00 kubeadm=1.26.0-00 kubectl=1.26.0-00 # 버전 지정
    sudo apt-mark hold kubelet kubeadm kubectl
    
    # 노드01 에도 같은 작업 
    ssh node01
    cat <<EOF | tee /etc/modules-load.d/k8s.conf
    br_netfilter
    EOF
   
    cat <<EOF | tee /etc/sysctl.d/k8s.conf
    net.bridge.bridge-nf-call-ip6tables = 1
    net.bridge.bridge-nf-call-iptables = 1
    EOF
    sysctl --system
   
    service docker status
    sudo apt-get update 
    sudo apt-get install -y apt-transport-https ca-certificates curl
    sudo curl -fsSLo /etc/apt/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
    echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
    
    sudo apt-get update
    sudo apt-get install -y kubelet=1.26.0-00 kubeadm=1.26.0-00 kubectl=1.26.0-00 # 버전 지정
    sudo apt-mark hold kubelet kubeadm kubectl
    ```
   
    </details>

2. <details>
    <summary>What is the version of kubelet installed? </summary>
  
    ```bash
    kublet --version
    ```
   
    </details>

3. <details>
    <summary>How many nodes are part of kubernetes cluster currently? </summary>
  
    ```bash
    kubectl get nodes
    ```
   
    </details>

> H
5. <details>
    <summary>Initialize Control Plane Node (Master Node). Use the following options: </summary>
  
    ```bash
    ip addr 
    kubeadm init --apiserver-advertise-address 10.13.26.9 --apiserver-cert-extra-sans controlplane pod-network-cidr 10.244.0.0/16
    mkdir -p $HOME/.kube
    sudo cp-i /etc/kubernetes/amdin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config 
    ```
   
    </details>

> N
6. <details>
    <summary>Generate a kubeadm join token </summary>
  
    ```bash
    kubeadm token create --help 
    kubeadm token create --print-join-command
    ```
   
    </details>

7. <details>
    <summary>Join node01 to the cluster using the join token </summary>
  
    ```bash
    ssh node01
    # kubeadm token create --print-join-command 결과 
    kubeadm join 10.13.26.9:6443 --token cpwmot.ldhadf3cokvyyx60 \
    --discovery-token-ca-cert-hash sha256:ea3a622922315b14b289c6efd7b1a77cbf81d29f6ddaf03472c304b6d3228c06
    ```
   
    </details>

> N
8. <details>
    <summary>Install a Network Plugin. As a default, we will go with flannel </summary>
  
    ```bash
    kubectl get nodes 
    # install addons
    # https://kubernetes.io/docs/concepts/cluster-administration/addons/
    # https://github.com/flannel-io/flannel#deploying-flannel-manually
    kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
    kubectl get pods -n kube-system
    kubectl get pods -n kube-system --watch 
    kubectl get nodes 
    ```
   
    </details>

# Troubleshooting
## Practice Test - Application Failure
1. <details>
    <summary>Troubleshooting Test 1: A simple 2 tier application is deployed in the alpha namespace. It must display a green web page on success. Click on the App tab at the top of your terminal to view your application. It is currently failed. Troubleshoot and fix the issue. </summary>
  
    ```bash
    k get pods -n alpha
    k config --help 
    k config set-context --help
    k config set-context --current --namespace=alpha
    k get pods 
    k get deploy
    k get svc 
    curl http://localhost:30081
    k describe deploy webapp-mysql
    k get svc # 이름 다름
    k edit svc mysql 
    cat /tmp/kubectl-edit-3364085288.yaml
    kubectl delete svc mysql 
    kubectl create -f /tmp/kubectl-edit-3364085288.yaml
    k get svc 
    ```
   
    </details>

2. <details>
    <summary>Troubleshooting Test 2: The same 2 tier application is deployed in the beta namespace. It must display a green web page on success. Click on the App tab at the top of your terminal to view your application. It is currently failed. Troubleshoot and fix the issue. </summary>
  
    ```bash
    k config set-context --current --namespace=beta
    k get pods 
    k get svc 
    k describe deploy webapp-mysql 
    k describe svc mysql-service 
    k get pods -o wide  # 데이터 포트가 8080이 아니라 3306
    k edit svc mysql-service 
    k get svc 
    k describe svc mysql-service 
    ```
   
    </details>

3. <details>
    <summary>Troubleshooting Test 3: The same 2 tier application is deployed in the gamma namespace. It must display a green web page on success. Click on the App tab at the top of your terminal to view your application. It is currently failed or unresponsive. Troubleshoot and fix the issue. </summary>
  
    ```bash
    k config set-context --current --namespace=gamma
    k get pods 
    k get svc 
    k describe svc web-service 
    k get pods -o wide
    k describe deploy webapp-mysql
    k get pods  
    k logs webapp-mysql-7cc9dcdffd-k4qcj
    k get svc 
    k describe svc mysql-service # Endpoints 없음 
    k describe pod mysql 
    k edit svc mysql-service  # mysql
    k describe svc mysql-service 
    ```
   
    </details>

4. <details>
    <summary>Troubleshooting Test 4: The same 2 tier application is deployed in the delta namespace. It must display a green web page on success. Click on the App tab at the top of your terminal to view your application. It is currently failed. Troubleshoot and fix the issue. </summary>
  
    ```bash
    k config set-context --current --namespace=delta 
    k get pods 
    k get svc 
    k describe deploy webapp-mysql # DB 유저 잘못지정 
    k edit deploy webapp-mysql # root
    k get pods 
    ```
   
    </details>

5. <details>
    <summary>Troubleshooting Test 5: The same 2 tier application is deployed in the epsilon namespace. It must display a green web page on success. Click on the App tab at the top of your terminal to view your application. It is currently failed. Troubleshoot and fix the issue. </summary>
  
    ```bash
    k config set-context --current --namespace=epsilon 
    k get pods 
    k get svc 
    k describe deploy webapp-mysql # DB 유저 잘못지정 
    k edit deploy webapp-mysql # root
    k get pods 
    k describe pod mysql
    k edit pod mysql # pwd 수정 
    k replace --force -f /tmp/kubectl-edit-2404243763.yaml
    k get pods 
    ```
   
    </details>

6. <details>
    <summary>Troubleshooting Test 6: The same 2 tier application is deployed in the zeta namespace. It must display a green web page on success. Click on the App tab at the top of your terminal to view your application. It is currently failed. Troubleshoot and fix the issue. </summary>
  
    ```bash
    k config set-context --current --namespace=zeta
    k get svc # 30081이 아닌 30088
    k edit svc web-service 
    k get svc 
    k describe deploy webapp-mysql
    k edit deploy webapp-mysql # root 
    k get pods 
    k desribe mysql  # pwd 이슈
    k edit pod mysql # pwd 수정 
    k replace --force -f /tmp/kubectl-edit-3569412833.yaml
    k get pods 
    ```
   
    </details>

## Practice Test - Control Plane Failure
1. <details>
    <summary>The cluster is broken. We tried deploying an application but it's not working. Troubleshoot and fix the issue. </summary>
  
    ```bash
    # source <(kubectl completion bash) <- 자동완성 기능 
    alias k=kubectl 
    kubectl get n
    k get deploy
    k describe deploy 
    k get rs 
    k describe rs app-865fdf7bbf
    k get pod 
    k describe pod app-865fdf7bbf # pending status , 포드가 할당 안되었음. 노드와 작업에
    k get pods -n kube-system 
    k describe pod -n kube-system kube-scheduler-controlplane
    cat /etc/kubernetes/manifests/kube-scheduler.yaml 
    vi /etc/kubernetes/manifests/kube-scheduler.yaml 
    k get pods -n kube-system --watch 
    k logs kube-scheduler-controlplane -n kube-system
    k get pods 
    k get deploy
    ```
   
    </details>

2. <details>
    <summary>Scale the deployment app to 2 pods. </summary>
  
    ```bash
    k get deploy
    k scale deploy app --replicas=2
    k get deploy
    ```
   
    </details>

3. <details>
    <summary>Even though the deployment was scaled to 2, the number of PODs does not seem to increase. Investigate and fix the issue. </summary>
  
    ```bash
    k get pods 
    k describe deploy app 
    k get pods -n kube-system
    k describe -n kube-system pods kube-controller-manager-controlplane
    k logs kube-controller-manager-controlplane -n kube-system
    cat /etc/kubernetes/manifests/kube-controller-manager-controlplane.yaml 
    cat /etc/kubernetes/controller-manager.conf 
    vi /etc/kubernetes/manifests/kube-controller-manager.yaml 
    k get pods -n kube-system --watch
    k get pods 
    k get deploy 
    ```
   
    </details>

4. <details>
    <summary>Something is wrong with scaling again. We just tried scaling the deployment to 3 replicas. But it's not happening. </summary>
  
    ```bash
    k get pods 
    k get deploy 
    k describe deploy app 
    k get pods -n kube-system
    k logs kube-controller-manager-controlplane -n kube-system
    cat /etc/kubernetes/pki/ca.crt
    vi /etc/kubernetes/manifests/kube-controller-manager.yaml 
    k get pods -n kube-system --watch
    k get pods 
    k get deploy 
    ```
   
    </details>

## Practice Test - Worker Node Failure
1. <details>
    <summary>Fix the broken cluster </summary>
  
    ```bash
    k get nodes
    k describe node node01 
    ssh node01
    service kubelet status 
    service kubelet start 
    service kubelet status 
    exit 
    kubectl get nodes 
    ```
   
    </details>

> H
2. <details>
    <summary>The cluster is broken again. Investigate and fix the issue. </summary>
  
    ```bash
    kubectl get nodes 
    kubectl describe node node01 
    ssh node01 
    service kubelet status 
    service kubelet start 
    service kubelet status 
    journalctl -u kubelet 
    ls /etc/kubernetes/kubelet.conf 
    cat /etc/kubernetes/kubelet.conf 
    ls /var/lib/kuelet/ 
    cat /var/lib/kuelet/config.yaml
    ls /etc/kubernetes/pki/ca.crt
    vi /var/lib/kubelet/config.yaml # /etc/kubernetes/pki/ca.crt
    service kubelet restart 
    service kubelet status 
    exit 
    kubectl get nodes 
    ```
   
    </details>

3. <details>
    <summary>The cluster is broken again. Investigate and fix the issue. </summary>
  
    ```bash
    kubectl get nodes 
    ssh node01 
    service kubelet status 
    journalctl -u kubelet 
    ls /etc/kubernetes/kubelet.conf 
    vi /etc/kubernetes/kubelet.conf # 6443
    vi /var/lib/kubelet/config.yaml 
    service kubelet restart 
    service kubelet status 
    exit 
    kubectl get nodes 
    ```
   
    </details>

## Practice Test - Troubleshoot Network
1. <details>
    <summary>A simple 2 tier application is deployed in the triton namespace. It must display a green web page on success. Click on the app tab at the top of your terminal to view your application. It is currently failed. Troubleshoot and fix the issue. </summary>
  
    ```bash
    kubectl get nodes
    kubectl get pods -A
    kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
    kubectl get pods -n triton
    ```
   
    </details>

2. <details>
    <summary>The same 2 tier application is having issues again. It must display a green web page on success. Click on the app tab at the top of your terminal to view your application. It is currently failed. Troubleshoot and fix the issue. </summary>
  
    ```bash
    kubectl get nodes
    kubectl get pods -A
    kubectl -n kube-system logs kube-proxy-tzrs9
    ls -l /var/lib/kube-proxy
    kubectl get ds -n kube-system kube-proxy -o yaml | less
    kubectl describe cm -n kube-system kube-proxy
    kubectl edit ds -n kube-system kube-proxy # --config=/var/lib/kube-proxy/config.conf
    kubectl get pods -n kube-system
    ```
   
    </details>

# Other Topics   
## Practice Test - Advance Kubectl Commands
1. <details>
    <summary>Get the list of nodes in JSON format and store it in a file at /opt/outputs/nodes.json. </summary>
  
    ```bash
    kubectl get nodes -o json > /opt/outputs/nodes.json
    ```
   
    </details>

2. <details>
    <summary>Get the details of the node node01 in json format and store it in the file /opt/outputs/node01.json. </summary>
  
    ```bash
    kubectl get node node01 -o json > /opt/outputs/node01.json
    ```
   
    </details>

3. <details>
    <summary>Use JSON PATH query to fetch node names and store them in /opt/outputs/node_names.txt. </summary>
  
    ```bash
    kubectl get nodes -o=jsonpath='{.items[*].metadata.name}' > /opt/outputs/node_names.txt
    ```
   
    </details>

4. <details>
    <summary>Use JSON PATH query to retrieve the osImages of all the nodes and store it in a file /opt/outputs/nodes_os.txt. </summary>
  
    ```bash
    kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.osImage}' > /opt/outputs/nodes_os.txt
    ```
   
    </details>

5. <details>
    <summary>A kube-config file is present at /root/my-kube-config. Get the user names from it and store it in a file /opt/outputs/users.txt. </summary>
  
    ```bash
    kubectl config view --kubeconfig=my-kube-config -o jsonpath="{.users[*].name}" > /opt/outputs/users.txt
    ```
   
    </details>

6. <details>
    <summary>A set of Persistent Volumes are available. Sort them based on their capacity and store the result in the file /opt/outputs/storage-capacity-sorted.txt. </summary>
  
    ```bash
    kubectl get pv --sort-by=.spec.capacity.storage > /opt/outputs/storage-capacity-sorted.txt
    ```
   
    </details>

7. <details>
    <summary>That was good, but we don't need all the extra details. Retrieve just the first 2 columns of output and store it in /opt/outputs/pv-and-capacity-sorted.txt. </summary>
  
    ```bash
    kubectl get pv --sort-by=.spec.capacity.storage -o=custom-columns=NAME:.metadata.name,CAPACITY:.spec.capacity.storage > /opt/outputs/pv-and-capacity-sorted.txt
    ```
   
    </details>

8. <details>
    <summary>Use a JSON PATH query to identify the context configured for the aws-user in the my-kube-config context file and store the result in /opt/outputs/aws-context-name. </summary>
  
    ```bash
    kubectl config view --kubeconfig=my-kube-config -o jsonpath="{.contexts[?(@.context.user=='aws-user')].name}" > /opt/outputs/aws-context-name
    ```
   
    </details>

# Lightning Lab
## Practice Test - Lightning Lab1
> H
1. <details>
    <summary>Upgrade the current version of kubernetes from 1.25.0 to 1.26.0 exactly using the kubeadm utility. Make sure that the upgrade is carried out one node at a time starting with the controlplane node. To minimize downtime, the deployment gold-nginx should be rescheduled on an alternate node before upgrading each node. </summary>
  
    ```bash
    kubectl drain controlplane --ignore-daemonsets
   
    apt-get update
    apt-mark unhold kubeadm
    apt-get install -y kubeadm=1.26.0-00
    kubeadm upgrade plan
    kubeadm upgrade apply v1.26.0
    kubectl describe node controlplane | grep -A 3 taint
    kubectl taint node controlplane node-role.kubernetes.io/control-plane:NoSchedule-
    kubectl taint node controlplane node.kubernetes.io/unschedulable:NoSchedule-
    apt-mark unhold kubelet
    apt-get install -y kubelet=1.26.0-00
    systemctl daemon-reload
    systemctl restart kubelet
    kubectl uncordon controlplane
    apt-mark unhold kubectl
    apt-get install -y kubectl=1.26.0-00
    apt-mark hold kubeadm kubelet kubectl
    kubectl drain node01 --ignore-daemonsets
   
    ssh node01
    apt-get update
    apt-mark unhold kubeadm
    apt-get install -y kubeadm=1.26.0-00
    kubeadm upgrade node
    apt-mark unhold kubelet
    apt-get install kubelet=1.26.0-00
    systemctl daemon-reload
    systemctl restart kubelet
    apt-mark hold kubeadm kubelet
    exit
    kubectl uncordon node01
    kubectl get pods -o wide | grep gold-nginx
    ```
   
    </details>

> H
2. <details>
    <summary>Print the names of all deployments in the admin2406 namespace in the following format: </summary>
  
    ```bash
    # custom-columns
    kubectl -n admin2406 get deployment -o custom-columns=DEPLOYMENT:.metadata.name,CONTAINER_IMAGE:.spec.template.spec.containers[].image,READY_REPLICAS:.status.readyReplicas,NAMESPACE:.metadata.namespace --sort-by=.metadata.name > /opt/admin2406_data
    ```
   
    </details>
   
3. <details>
    <summary>A kubeconfig file called admin.kubeconfig has been created in /root/CKA. There is something wrong with the configuration. Troubleshoot and fix it </summary>
  
    ```bash
    kubectl get pods --kubeconfig /root/CKA/admin.kubeconfig
    cat ~/.kube/config
    vi /root/CKA/admin.kubeconfig # 6443
    kubectl get pods --kubeconfig /root/CKA/admin.kubeconfig
    ```
   
    </details>

4. <details>
    <summary>Create a new deployment called nginx-deploy, with image nginx:1.16 and 1 replica. Next upgrade the deployment to version 1.17 using rolling update. </summary>
  
    ```bash
    kubectl create deployment nginx-deploy --image=nginx:1.16
    kubectl set image deployment/nginx-deploy nginx=nginx:1.17 --record
    ```
   
    </details>

> H
5. <details>
    <summary>A new deployment called alpha-mysql has been deployed in the alpha namespace. However, the pods are not running. Troubleshoot and fix the issue. The deployment should make use of the persistent volume alpha-pv to be mounted at /var/lib/mysql and should use the environment variable MYSQL_ALLOW_EMPTY_PASSWORD=1 to make use of an empty root password.</summary>
  
    ```bash
    kubectl get deployment -n alpha alpha-mysql  -o yaml | yq e .spec.template.spec.containers -
    kubectl get pods -n alpha
    kubectl describe pod -n alpha alpha-mysql-6d945ffc78-v6ddg
    kubectl get pv alpha-pv
    ```
   
    </details>

6. <details>
    <summary>Take the backup of ETCD at the location /opt/etcd-backup.db on the controlplane node. </summary>
  
    ```bash
    ETCDCTL_API='3' etcdctl snapshot save \
    --cacert=/etc/kubernetes/pki/etcd/ca.crt \
    --cert=/etc/kubernetes/pki/etcd/server.crt \
    --key=/etc/kubernetes/pki/etcd/server.key \
    /opt/etcd-backup.db
    ```
   
    </details>

> N
7. <details>
    <summary>Create a pod called secret-1401 in the admin1401 namespace using the busybox image. The container within the pod should be called secret-admin and should sleep for 4800 seconds. </summary>
  
    ```bash
    kubectl run secret-1401 -n admin1401 --image busybox --dry-run=client -o yaml --command -- sleep 4800 > admin.yaml
    vi admin.yaml
    kubectl create -f admin.yaml
    ```
   
    </details>

# Mock Exams
## Mock Exam - 1
1. <details>
    <summary>Deploy a pod named nginx-pod using the nginx:alpine image. </summary>
  
    ```bash
    k
    kubectl get + 탭2번
    # kubectl cheat 검색 : https://kubernetes.io/docs/reference/kubectl/cheatsheet/
    source <(kubectl completion bash) # set up autocomplete in bash into the current shell, bash-completion package should be installed first.
    echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell.
    alias k=kubectl
    complete -o default -F __start_kubectl k
    
    k run nginx-pod --image=nginx:alpine
    k get pod 
    k describe pod nginx-pod 
    ```
   
    </details>

2. <details>
    <summary>Deploy a messaging pod using the redis:alpine image with the labels set to tier=msg. </summary>
  
    ```bash
    k run --help 
    kubectl run messaging --image=redis:alpine --labels="tier=msg"
    k get pod 
    k describe pod messaging
    ```
   
    </details>

3. <details>
    <summary>Create a namespace named apx-x9984574. </summary>
  
    ```bash
    k create namespace apx-x9984574
    k get ns 
    ```
   
    </details>

> N 
4. <details>
    <summary>Get the list of nodes in JSON format and store it in a file at /opt/outputs/nodes-z3444kd9.json. </summary>
  
    ```bash
    k get nodes 
    k get nodes -o json > /opt/outputs/nodes-z3444kd9.json
    cat /opt/outputs/nodes-z3444kd9.json
    ```
   
    </details>

5. <details>
    <summary>Create a service messaging-service to expose the messaging application within the cluster on port 6379. Use imperative commands. Service: messaging-servicePort: 6379 Type: ClusterIp Use the right labels </summary>
  
    ```bash
    k get pods 
    k get svc 
    k expose --help # kubectl expose pod valid-pod --port=444 --name=frontend
    kubectl expose pod messaging --port=6379 --name=messaging-service
    k get svc 
    k describe svc messaging-service
    k get pods -o wide
    ```
   
    </details>

6. <details>
    <summary>Create a deployment named hr-web-app using the image kodekloud/webapp-color with 2 replicas. Name: hr-web-app / Image: kodekloud/webapp-color / Replicas: 2 </summary>
  
    ```bash
    k create deployment hr-web-app --image=kodekloud/webapp-color --replicas=2
    k get deploy 
    k describe deploy hr-web-app
    ```
   
    </details>

> H
7. <details>
    <summary>Create a static pod named static-busybox on the controlplane node that uses the busybox image and the command sleep 1000. Name: static-busybox / Image: busybox </summary>
  
    ```bash
    k run static-busybox --image=busybox --dry-run=client -o yaml --command -- sleep 1000 > static-busybox.yaml
    cat static-busybox.yaml    
    mv static-busybox.yaml /etc/kubernetes/manifests/
    kubectl get pods 
    k describe pod static-busybox-controlplane
    ```
   
    </details>

8. <details>
    <summary>Create a POD in the finance namespace named temp-bus with the image redis:alpine. / Name: temp-bus / Image Name: redis:alpine </summary>
  
    ```bash
    k run temp-bus --image=redis:alpine -n finance
    k get pod -n finance
    k describe pod temp-bus -n finance
    ```
   
    </details>

> V
9. <details>
    <summary>A new application orange is deployed. There is something wrong with it. Identify and fix the issue. / Issue fixed </summary>
  
    ```bash
    k get pod # Init 컨테이너 문제 
    k describe pod orange 
    k logs orange init-myservice
    k edit pod orange # sleep
    k replace --force -f /tmp/kubectl-edit-1117791310.yaml
    k get pods --watch 
    ```
   
    </details>

10. <details>
    <summary>Expose the hr-web-app as service hr-web-app-service application on port 30082 on the nodes on the cluster. / The web application listens on port 8080. / Name: hr-web-app-service / Type: NodePort / Endpoints: 2 / Port: 8080 / NodePort: 30082 </summary>
  
    ```bash
    k get deploy
    k expose deploy hr-web-app --name=hr-web-app-service --type NodePort --port 8080 
    k get svc # 노드포트가 다름 
    k describe svc hr-web-app
    k edit svc hr-web-app-service # 30082
    k get svc 
    ```
   
    </details>

11. <details>
    <summary>Use JSON PATH query to retrieve the osImages of all the nodes and store it in a file /opt/outputs/nodes_os_x43kj56.txt. / The osImages are under the nodeInfo section under status of each node. / Task Completed </summary>
  
    ```bash
    k get nodes 
    k get nodes -o json 
    # kubectl cheat 검색 : https://kubernetes.io/docs/reference/kubectl/cheatsheet/
    kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.osImage}'
    kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.osImage}' > /opt/outputs/nodes_os_x43kj56.txt
    cat /opt/outputs/nodes_os_x43kj56.txt
    ```
   
    </details>

> V
12. <details>
    <summary>Create a Persistent Volume with the given specification. / Volume Name: pv-analytics / Storage: 100Mi / Access modes: ReadWriteMany / Host Path: /pv/data-analytics / Task Completed </summary>
  
    ```bash
    # Persistent Volume 검색 : [https://kubernetes.io/docs/reference/kubectl/cheatsheet/](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
    vi pv.yaml 
    k create -f pv.yaml 
    k get pv 
    k describe pv pv-analytics
    ```
   
    </details>

## Mock Exam - 2
1. <details>
    <summary>Take a backup of the etcd cluster and save it to /opt/etcd-backup.db. / Backup Completed </summary>
  
    ```bash
    # kubectl cheat 검색 : https://kubernetes.io/docs/reference/kubectl/cheatsheet/
    source <(kubectl completion bash) # set up autocomplete in bash into the current shell, bash-completion package should be installed first.
    echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell.
    alias k=kubectl
    complete -o default -F __start_kubectl k
    
    # etdc backup 검색 : https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/
    # ETCDCTL_API=3 etcdctl --endpoints $ENDPOINT snapshot save snapshotdb
    ETCDCTL_API=3 etcdctl snapshot save -h
    cat /etc/kubernetes/manifests/etcd.yaml | grep file 
    vi /etc/kubernetes/manifests/etcd.yaml
   
    ETCDCTL_API=3 etcdctl --endpoints 127.0.0.1:2379 snapshot save /opt/etcd-backup.db. \
    --cacert=/etc/kubernetes/pki/etcd/ca.crt \
    --cert=/etc/kubernetes/pki/etcd/server.crt \
    --key=/etc/kubernetes/pki/etcd/server.key
   
    ls /opt/etcd-backup.db. 
    ```
   
    </details>

> V
2. <details>
    <summary> Create a Pod called redis-storage with image: redis:alpine with a Volume of type emptyDir that lasts for the life of the Pod. / Specs on the below. / Pod named 'redis-storage' created / Pod 'redis-storage' uses Volume type of emptyDir / Pod 'redis-storage' uses volumeMount with mountPath = /data/redis </summary>
  
    ```bash
    k run redis-storage --image=redis:alpine --dry-run=client -o yaml
    k run redis-storage --image=redis:alpine --dry-run=client -o yaml > redis-storage.yaml 
    # pod volumn 검색 : https://kubernetes.io/docs/concepts/storage/volumes/#emptydir
    vi redis-storage.yaml 
    k create -f redis-storage.yaml
    k get pods
    k get pods --watch
    k describe pod redis-storage
    ```
   
    </details>

> V
3. <details>
    <summary> Create a new pod called super-user-pod with image busybox:1.28. Allow the pod to be able to set system_time. / The container should sleep for 4800 seconds. / Pod: super-user-pod / Container Image: busybox:1.28 / SYS_TIME capabilities for the conatiner? </summary>
  
    ```bash
    k run --help
    k run super-user-pod --image=busybox:1.28 --dry-run=client -o yaml
    k run super-user-pod --image=busybox:1.28 --dry-run=client -o yaml > super-user-pod.yaml 
    vi super-user-pod.yaml 
    # security capabilities 검색 : https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-capabilities-for-a-container    
    k create -f super-user-pod.yaml
    k get pods
    k get pods --watch
    k describe pod super-user-pod
    ```
   
    </details>

> V
4. <details>
    <summary> A pod definition file is created at /root/CKA/use-pv.yaml. Make use of this manifest file and mount the persistent volume called pv-1. Ensure the pod is running and the PV is bound. / mountPath: /data / persistentVolumeClaim Name: my-pvc / persistentVolume Claim configured correctly / pod using the correct mountPath / pod using the persistent volume claim? </summary>
  
    ```bash
    cat /root/CKA/use-pv.yaml 
    k get pv
    k get pvc 
    # pvc 검색 : https://kubernetes.io/docs/concepts/storage/persistent-volumes/#claims-as-volumes
    vi pvc.yaml 
    k create -f pvc.yaml
    vi /root/CKA/use-pv.yaml
    k create -f /root/CKA/use-pv.yaml
    k get pods 
    cat /root/CKA/use-pv.yaml
    k describe pod use-pv
    ```
   
    </details>

> V
5. <details>
    <summary> Create a new deployment called nginx-deploy, with image nginx:1.16 and 1 replica. Next upgrade the deployment to version 1.17 using rolling update. Deployment : nginx-deploy. Image: nginx:1.16 / Image: nginx:1.16 / Task: Upgrade the version of the deployment to 1:17 / Task: Record the changes for the image upgrade </summary>
  
    ```bash
    k create deploy nginx-deploy --image=nginx:1.16 --replicas=1 
    k get deploy
    k describe deploy nginx-deploy
    k set image --help 
    kubectl set image deployment/nginx-deploy nginx=nginx:1.1.7
    k describe deploy nginx-deploy
    ```
   
    </details>

> VV
6. <details>
    <summary> Create a new user called john. Grant him access to the cluster. John should have permission to create, list, get, update and delete pods in the development namespace . The private key exists in the location: /root/CKA/john.key and csr at /root/CKA/john.csr. / Important Note: As of kubernetes 1.19, the CertificateSigningRequest object expects a signerName. / Please refer the documentation to see an example. The documentation tab is available at the top right of terminal. / CSR: john-developer Status:Approved / Role Name: developer, namespace: development, Resource: Pods / Access: User 'john' has appropriate permissions </summary>

  
    ```bash
    ls /root/CKA/
    cd /root/CKA
    ls 
    cat john.csr 
    # 검색 : role binding : https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/
    vi john-csr.yaml
    cat john.csr | base64 | tr -d "\n"
    vi john-csr.yaml
    k create -f john-csr.yaml
    k get csr 
    k certificate approve john-developer
    k get csr 
    ```
   
    </details>

> V
7. <details>
    <summary> Create a nginx pod called nginx-resolver using image nginx, expose it internally with a service called nginx-resolver-service. Test that you are able to look up the service and pod names from within the cluster. Use the image: busybox:1.28 for dns lookup. Record results in /root/CKA/nginx.svc and /root/CKA/nginx.pod / Pod: nginx-resolver created / Service DNS Resolution recorded correctly / Pod DNS resolution recorded correctly </summary>
  
    ```bash
    k run nginx-resolver --image=nginx
    k get pods 
    k expose pod nginx-resolver --name=nginx-resolver-service --port=80
    k describe svc nginx-resolver-service
    k run busybox --image=busybox:1.28 -- sleep 4000 
    k get pods
    k exec busybox -- nslookup nginx-resolver-service > /root/CKA/nginx.svc
    k get pods -o wide 
    # DNS 검색 : https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/
    k exec busybox -- nslookup 10-244-192-1.default.pod.cluster.local
    k exec busybox -- nslookup 10-244-192-1.default.pod.cluster.local > /root/CKA/nginx.svc 
    ```
   
    </details>

8. <details>
    <summary> Create a static pod on node01 called nginx-critical with image nginx and make sure that it is recreated/restarted automatically in case of a failure. / Use /etc/kubernetes/manifests as the Static Pod path for example. / static pod configured under /etc/kubernetes/manifests ? / Pod nginx-critical-node01 is up and running </summary>
  
    ```bash
    k get nodes -o wide # 10.54.115.6
    ssh 10.54.115.6
    ls /etc/kubernetes/manifests/
    kubectl run --help 
    kubectl run nginx-critical --image=nginx --restart=Always --dry-run=client -o yaml 
    cat > /etc/kubernetes/manifests/nginx-critcal.yaml # node01
    kubectl get pods 
    kubectl describe pods nginx-resolver
    ```
   
    </details>
