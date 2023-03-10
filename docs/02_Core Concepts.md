# study 
[Day1](#cluster-architecture)<br>
[Day2](#kubelet)<br>
[Day3](#recap---replicasets)<br>
[Day4](#services)<br>

# Cluster Architecture 
- 쿠버네티스 
  - 쿠버네티스의 목적은 애플리케이션을 호스팅 하는 것
  - 컨테이너 형태의 자동화된 방식으로 애플리케이션 내의 다른 서비스 간에 응용 프로그램의 많은 인스턴스를 쉽게 배포할 수 있도록 함.
- 쿠버네트스 클러스터
  - ![image](https://user-images.githubusercontent.com/47103479/210134083-9556a259-d427-43ac-8aed-b8d3c0ead379.png)
  - 일련의 노드로 구성되어 컨테이너 형태로 애플리케이션을 호스팅함 
  - 작업자 노드는 선박 
  - 마스터 노드 : 클러트서 관리를 위해 다른 노드에 관한 정보를 저장하고, 계획하고, 노드와 컨테이너 등을 모니터링함 
  - ETCD 크러스터 : 고가용성 키-값 저장소, 정보를 저장하는 데이터베이스 
  - 스케줄러 : 컨테이너를 배치할 올바른 노드를 식별함. 
  - 컨트롤러
    - Controller-Manager
    - Node-Controller : 노드를 관리함. 새 노드를 클러스터에 온보딩하는 일을 담당함 
    - Replication-Controller  
  - Kube-apiserver : 쿠버네티스의 기본 관리 구성 요소로 클러스터 내의 모든 작업을 오케스트레이션함  
  - 런타임 엔진 : 컨테이너를 실행할 수 있는 소프트웨어(Docker, ContainerD,Rock et) 
  - Kubelet : 클러스터의 각 노드에서 실행되는 에이전트, Kube API 서버의 지시를 수신함. 필요에 따라 노드에 컨테이너트를 배포하거나 제거함 
  - Kube-proxy : 클러스터 내의 서비스간 의사 소통을 가능하게 도와줌. 컨테이너가 실행될 수 있도록 작업자 노드에 배치 

# ETCD 
- 분산 키-값 저장소 
  - key-value store
  - ![image](https://user-images.githubusercontent.com/47103479/210163366-1dd0fa72-8fb1-4441-92f3-dc6cbcbc4b54.png)
    - 새로운 정보를 추가할 때 마다 테이블 전체가 영향을 받음 
  - ![image](https://user-images.githubusercontent.com/47103479/210163373-8b4148b5-ab6b-47ff-98e4-7490f29dc865.png)
    - 키-값 저장소는 문서 또는 페이지 형태로 정보를 저장함, 한 파일을 변경해도 다른 파일에는 영향을 미치지 않음 
    - 데이터가 복잡해지면 JSON 또는 YANO와 같은 데이터 형식으로 저장할 수 있음 
- ETCD 설치 및 작동 
  - ```shell
    # Download Binaries 
    curl -L https://github.com/etcd-io/etcd/releases/download/v3.3.11/etcdv3.3.11-linux-amd64.tar.gz -o etcd-v3.3.11-linux-amd64.tar.gz
    
    # Extract 
    tar xzvf etcd-v3.3.11-linux-amd64.tar.gz
    
    # Run ETCD Service 
    ./etcd
    
    # 키-값 쌍 저장 
    ./etcdctl set key1 value1
    
    # 저장된 데이터 검색 
    ./etcdctl get key1
    
    # 옵션 검색 
    ./etcdctl
    
    # 버전 검색 
    ./etcdctl --version 
    
    # API version 3에서 작동 
    ETCDCTL_API=3 ./etcdctl version
    export ETCDCTL_API=3 ./etcdctl version 
    
    # ETCDCTL v3 
    export ETCDCTL_API = 3 ./etcdctl version
    ./etcdctl put key1 value1 # 값 설정
    ./etcdctl get key1 # 값 가져옴
    
    # ETCDCTL API버전과 인증서 파일 경로 지정
    kubectl exec etcd - master - n kube - system -- sh - c "ETCDCTL_API=3 etcdctl get / --prefix --keys-only --limit=10 --cacert /etc/kubernetes/pki/etcd/ca.crt --cert /etc/kubernetes/pki/etcd/server.crt --key /etc/kubernetes/pki/etcd/server.key" 
    ```
  
- 역할
  - 클러스터에 관한 정보를 저장함 (Nodes, PODs, Configs, Secrets, Accounts, Roles, Bindings, Others) 
  - 배포 방식
    - Manual
      - wget -q --https-only \
        "https://github.com/coreos/etcd/releases/download/v3.3.9/etcd-v3.3.9-linux-amd64.tar.gz"
      - ![image](https://user-images.githubusercontent.com/47103479/210163930-b972185b-5870-475d-ae44-5c8744d4ed74.png)
    - kubeadm
      - kubectl get pods -n kube-system 
        - ![image](https://user-images.githubusercontent.com/47103479/210163971-9e1307b7-c701-4d5e-9e8f-9ca98bdf469d.png)
      - kubectl exec etcd-master –n kube-system etcdctl get / --prefix –keys-only : 쿠버네티스에 저장된 모든키를 검색
        - ![image](https://user-images.githubusercontent.com/47103479/210163980-2f6c9c9a-032e-4f95-bcd1-7ac2d32ed04f.png)
      - Registry - minions, pods, replicasets, deployments, roles, secrets

# Kube-api server 
- ![image](https://user-images.githubusercontent.com/47103479/210164103-7a6b5646-f3a8-4595-a31a-40c14d1f6381.png)
- 설치
  - wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-apiserver
    - ![image](https://user-images.githubusercontent.com/47103479/210164194-c6d8cd85-359d-457d-8aba-bf9c43822fc3.png)
  - kubectl get pods -n kube-system : kubeadmin은 kubeadmin-apiserver를 배포함 
    - ![image](https://user-images.githubusercontent.com/47103479/210164199-b0af2c72-faf7-4b22-ba0f-f5916383867b.png)
  - cat /etc/kubernetes/manifests/kube-apiserver.yaml
    - ![image](https://user-images.githubusercontent.com/47103479/210164203-026793d2-1752-43a0-9f06-c7f5fb8e9673.png)
  - cat /etc/systemd/system/kube-apiserver.service : 옵션 검사 
    - ![image](https://user-images.githubusercontent.com/47103479/210164244-e978f70f-e6f0-4310-8034-135392ab9588.png)
  - ps -aux | grep kube-apiserver : 실행 중인 프로세스 확인
    - ![image](https://user-images.githubusercontent.com/47103479/210164255-a6d26353-6993-4262-a040-d656f2792bcc.png)

# Kube-Controller Manager 
- 쿠버네티스의 다양한 컨트롤러를 관리함 
- 컨트롤러는 지속적으로 시스템 내 다양한 구성 요소의 상태를 모니터링함, 전체 시스템을 원하는 기능 상태로 가져오기 위해 노력함 
- ![image](https://user-images.githubusercontent.com/47103479/210164860-ae16d6a5-1f23-4adf-b2c3-8d99cef35819.png)
  - 노드 컨트롤러는 상태를 모니터링 하기 위해 Kube API서버를 통해서 메모를 작성하고 필요한 조치를 취함. 상태를 테스트함 
- ![image](https://user-images.githubusercontent.com/47103479/210164874-f1eeea49-9647-4c67-8d6a-b29b2b3633db.png)
  - 복제 컨트롤러는 상태 모니터링을 담당함, 복제 세트의 수를 확인하고 원하는 수를 보장함. Pod가 죽으면 재생성함  
- 쿠버네티스의 다양한 컨트롤러
  - ![image](https://user-images.githubusercontent.com/47103479/210164918-abd69d1f-5109-42bd-a4b2-d2ae76ef17ea.png)
- 설치 
  - wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-controller-manager
    - ![image](https://user-images.githubusercontent.com/47103479/210164966-83287181-6445-402d-a63e-aefcd784f17b.png)
  - kubectl get pods -n kube-system
    - ![image](https://user-images.githubusercontent.com/47103479/210164989-6f0d0214-4b02-4c1e-a3eb-c6c5df523905.png)
  - cat /etc/kubernetes/manifests/kube-controller-manager.yaml
    - ![image](https://user-images.githubusercontent.com/47103479/210164991-ea05395f-2f04-4c42-a58f-faa483e95345.png)
  - cat /etc/systemd/system/kube-controller-manager.service
    - ![image](https://user-images.githubusercontent.com/47103479/210164994-31d152bf-e3f6-4fc7-bfda-971c680ed38d.png)
  - ps -aux | grep kube-controller-manager
    - ![image](https://user-images.githubusercontent.com/47103479/210164997-3a812839-e619-4290-8f99-3b4107442462.png)

# Kube Scheduler
- 노드에서 Pod 예약을 담당함. 어떤 파드가 어디로 가는지 결정함 
- ![image](https://user-images.githubusercontent.com/47103479/210165067-8c058b0b-2f54-4d28-8763-3006816ddf6f.png)
  - 포드에 가장 적합한 노드를 식별함
  - 포드의 프로필에 맞지 않는 노드를 필터링함(CPU가 충분하지 않는 노드, 파드에 요청한 메모리 리소스)
  - 스케줄러는 노드의 순위를 매김(우선 순위 기능을 사용하여 점수를 할당함 - 무료로 사용할 수 있는 리소스의 양.)
  - 더 고려해야할 부분
    - Resource Requirements and Limits
    - Taints and Tolerations
    - Node Selectors/Affinity
- 설치
  - wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-scheduler
    - ![image](https://user-images.githubusercontent.com/47103479/210165166-4a249136-49ee-4caa-8ff4-8968eb65f424.png)
  - cat /etc/kubernetes/manifests/kube-scheduler.yaml
    - ![image](https://user-images.githubusercontent.com/47103479/210165174-6b551e21-d20a-4b6c-9944-ea2f2a7533cb.png)
  - ps -aux | grep kube-scheduler
    - ![image](https://user-images.githubusercontent.com/47103479/210165185-df1bc342-2623-4e53-b0e5-7e3402e81978.png)

# Kubelet
- ![image](https://user-images.githubusercontent.com/47103479/210170369-631403e9-9ec8-44ab-ac99-63a1052e5bb6.png)
- 노드의 컨테이너 또는 파드, 컨테이너 런타임 엔진을 요청함. 파드를 계속 모니터링함 
- 설치 
  - kubeadm 사용해서 클러스터를 배포하는 경우 kubelet을 자동으로 배포하지 않음. 항상 수동으로 설치해야함 
  - wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kubelet
    - ![image](https://user-images.githubusercontent.com/47103479/210170382-03b7506a-c971-4598-9df6-c9542e1b3fbf.png)
  - ps -aux | grep kubelet
    - ![image](https://user-images.githubusercontent.com/47103479/210170386-1315e520-1e7d-4b54-9beb-9f0ad33ec1d5.png)

# Kube-proxy
- 파드 네트워크는 클러스터의 모든 노드에 걸친 내부 가상 네트워크 
- Kube-proxy는 각 노드에서 실행되는 프로세스로 새로운 서비스를 찾고, 새로운 서비스가 생성될 때마다 각 노드에 적절한 규칙을 생성함. 해당 서비스에 대한 트랙픽을 백엔드 파드로 전달함 
- ![image](https://user-images.githubusercontent.com/47103479/210170535-6df57780-66b0-40c9-a34a-864c113c6be2.png)
  - 10.96.0.12의 서비스 IP로 이동하여 실제 파드의 IP인 10.32.0.15로 변경함 
- 설치
  - wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-proxy
    - ![image](https://user-images.githubusercontent.com/47103479/210170550-6eada300-0446-4409-8c0a-d608d791dae5.png)
  - kubectl get pods -n kube-system
    - ![image](https://user-images.githubusercontent.com/47103479/210170576-4803846b-a7b1-43f3-878e-a71d70c79a9f.png)
  - kubectl get daemonset -n kube-system
    - ![image](https://user-images.githubusercontent.com/47103479/210170587-d7b0414a-2e8c-4977-8d3c-d50d13b97c22.png)

# Recap - PODs
- 목표 : 쿠버네티스와 함께 애플리케이션을 배포하는 것, 쿠버네티스는 컨테이너를 직접 배포하지 않음 
- 파드는 애플리케이션의 단일 인스턴스로 가장 작은 개체 
- ![image](https://user-images.githubusercontent.com/47103479/210170760-1b9cc516-8659-4c29-8fd1-5a2271246b37.png)
  - 애플리케이션을 액세스하는 사용자 수가 증가하면 인스턴스를 추가해야함 -> 새 인스턴스와 함께 동일한 응용 프로그램의 새 파드를 만듬 -> 사용자 기반이 더 늘어나고 현재 논드에 충분한 용량이 없다면? -> 언제든지 클러스터의 새 노드에서 추가 파드를 배포할 수 있음. 새 노드가 추가됨(클러스터의 물리적 용량을 확장함)   
    - 파드는 애플리케이션을 실행하는 컨테이너로 1대1 관계를 갖음
    - 파드는 확장하려면 새 파드를 만들고 축소하려면 기존 파드를 삭제함 
- Multi-Container PODs 
  - ![image](https://user-images.githubusercontent.com/47103479/210170844-9da93552-b3d5-4978-aeef-c7e6c2f949ab.png)
  - 하나의 파드는 여러 컨테이너를 가질 수 있음. Helper Containers를 통해 일종의 지원 작업을 수행할 수 있음(사용자 처리, 업로드된 파일 데이터 처리 등). 두 컨테이너는 동일한 네트워크 공간을 공유하기 때문에 서로 localhost를 참조하여 통신할 수 있고 동일한 저장 공간을 쉽게 공유할 수도 있음 
- ![image](https://user-images.githubusercontent.com/47103479/210170938-5368cbfe-de72-4e2b-91f4-fd674f33bde2.png)
  - 파드를 사용하면 쿠버네티스가 아래의 모든 작업을 자동으로 수행함. 파드는 어떤 컨테이너로 구성되는지 정의하기만 하면 됨  
    - links, custom networks를 사용해서 공유 가능한 볼륨을 생성하고 컨테이너 간에 공유해야 함. 
    - 애플리케이션 컨테이너가 죽으면 helper 컨테이너도 수동으로 죽기 때문에 상태를 모니터링 해야함. 
- 파드 배포 
  - kubectl run nginx --image nginx - 파드를 생성하여 Docker 컨테이너를 배포함 
    - 파드를 자동으로 생성함 - NGINX 도커 이미지의 인스턴스를 배포함 - 이미지 parameter를 사용하여 이미지 이름을 지정함 
    - Docker Hub : 최신 도커 이미지가 있는 공용 저장소로 다양한 응용 프로그램이 저장됨  
  - kubectl get pods
    - ![image](https://user-images.githubusercontent.com/47103479/210171058-36272936-4895-4b08-927d-2edd0cd03d57.png)
    - ![image](https://user-images.githubusercontent.com/47103479/210171063-453542be-d07d-4b08-a79f-a48071829bf3.png)
    - 클러스터 파드의 수 및 상태를 볼 수 있음 
- YAML 
  - apiVersion, kind, metadata, spec - 최상위 수준, 루트 수준 속성으로 필수 입력란
  - ![image](https://user-images.githubusercontent.com/47103479/210172035-23e7af82-806c-43ca-9b29-45db540d945e.png)
  - apiVersion
    - 개체를 생성하는 데 사용하는 쿠버네티스 API
      - POD - v1
      - Service - v1
      - ReplicaSet - apps/v1
      - Deployment - apps/v1 
  - kind : 만들고자 하는 객체의 종류 
  - metadata : name(문자열), labels(dict) 등의 데이터 
  - spec : 만들려는 객체에 따라 추가정보를 제공하는 곳 
    - Spec은 dict형, containers는 List/Array(파드는 그 안에 여러 컨테이너를 가질 수 있기 때문에) 
    - Containers의 아래 -는 1st Item in List(도커 리포지토리의 도커 이미지) 
  - > kubectl create -f pod-definition.yml : pod 생성 (kubectl apply -f pod.yaml / -f 옵션을 사용하여 파일 이름을 전달함)
  - > kubectl get pods : 사용 가능한 파드 목록 확인
  - > kubectl describe pod myapp-pd : 파드에 대한 자세한 정보 확인 

# Recap - ReplicaSets 
- Replication Controller 
  - 컨트롤러는 쿠버네티스의 두뇌. 쿠버네티스 개체를 모니터링하는 프로세스 
  - ![image](https://user-images.githubusercontent.com/47103479/210241406-e7972d60-208d-43c1-b3e3-4a52f3a21b6c.png)
    - 복제 컨트롤러가 있으면 기존 것이 실패했을 때 새 파드를 자동으로 불러옴 
  - ![image](https://user-images.githubusercontent.com/47103479/210242242-cf309a86-ffa7-4ca6-9855-eacf1a1e1979.png)
    - load를 공유하기 위해 여러 파드를 생성하는 것 
  - Replication Controller - 이전 기술로 Replica Set으로 대체됨 
  - ![image](https://user-images.githubusercontent.com/47103479/210242594-e82f5103-5e5c-4f58-b112-f8747a1c1766.png)
    - > kubectl create f replicaset definition.yml : 복제 세트 생성 
    - > kubectl get replicaset : 생성된 복제 세트 목록 보기 
    - > kubectl get pods
- Replica Set
  - ![image](https://user-images.githubusercontent.com/47103479/210243689-9dd1a34c-d1d5-4242-873c-18b20aeeb1f8.png)
    - apps/V1으로 apiVersion이 다름  / kind : ReplicaSet
    - Replica Set에는 선택 정의가 필요함 (선택 섹션은 어떤 파드가 아래에 있는지 식별함) - 속성에 대해 사용자 입력이 필요함 
    - 3개의 복제본으로 시작해서 6개의 복제본으로 확장하기
      - > kubectl replace f replicaset definition.yml : 복제본 수를 업데이트 하기
      - > kubectl scale replicas=6 f replicaset definition.yml : kube control scale command 실행
      - > kubectl scale replicas=6 replicaset myapp replicaset 
- Commands
  - > kubectl delete replicaset myapp replicaset : 복제 세트 삭제
  - > kubectl replace f replicaset definition.yml : 복제 세트 교체 또는 업데이트 

# Deployments 
- 롤링업데이트 : 인스턴스 업그레이드를 할 때 하나씩 업그레이드를 하는 것 
- ![image](https://user-images.githubusercontent.com/47103479/210245780-23677266-c91e-4d5f-afc0-5ab5692699e7.png)
  - 각 컨테이너는 파드에 캡슐화되고 파드는 복제 컨트롤러 또는 Replica Set을 사용해 여러 개 배포됨 - 기본 인스턴스를 원활하게 업그레이드 하기 위해 롤링 업데이트 사용, 변경 사항 실행 취소 필요에 따라 변경 사항을 일시 중지하고 다시 시작함 
- Definition
  - ![image](https://user-images.githubusercontent.com/47103479/210245999-aef07f8d-7dfb-4365-824b-5d0586678d3e.png)
  - > kubectl create f deployment definition.yml
  - > kubectl get deployments : 배포시 자동으로 replicaset 생성 
  - > kubectl get replicaset 
  - > kubectl get pods
- ReplicaSet과 배포의 차이는 배포라고 하는 새로운 쿠버네티스 개체 
- Commands
  - > kubectl get all : 생성된 모든 개체를 한 번에 보기 

# Tip
- https://kubernetes.io/docs/reference/kubectl/conventions/
- ``` bash
  # NGINX 포드 생성
  kubectl run nginx --image=nginx
  
  # POD 매니페스트 YAML 파일(-o yaml)을 생성합니다. 만들지 마세요(--드라이런)
  kubectl run nginx --image=nginx --dry-run=client -o yaml

  # 배포 만들기
  kubectl create deployment --image=nginx nginx

  # 배포 YAML 파일(-o yaml)을 생성합니다. 만들지 마세요(--드라이런)
  kubectl create deployment --image=nginx nginx --dry-run=client -o yaml
  
  # 배포 YAML 파일(-o yaml)을 생성합니다. 복제본 4개(--replicas=4)로 생성하지 마세요(--dry-run).
  kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml

  # 파일에 저장하고 필요에 따라 파일을 변경(예: 복제본 추가)한 다음 배포를 생성합니다.
  kubectl create -f nginx-deployment.yaml

  # k8s 버전 1.19+에서는 --replicas 옵션을 지정하여 4개의 복제본으로 배포를 생성할 수 있습니다.
  kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml
  
  Kubectl expose deployment nginx --port 80
  kubectl edit deployment nginx
  kubectl scale deployment nginx --replicas=5
  kubectl set image deployment nginx nginx=nginx:1.18
  ```

# Services
- 내부의 다양한 구성 요소 사이와 응용 프로그램 외부의 통신을 가능하게함. 애플리케이션을 함께 연결하는데 도움이됨 
- Pods,ReplicaSet,Deployments와 같은 object로 
- NodePort 서비스 : 노드에서 포트를 수신하는것, 웹 애플리케이션을 실행하는 파드의 포트로 요청 전달하는 것, 서비스가 노드의 포트를 수신하기 때문에 파드에 요청을 전달함 
- Services Types
  - NodePort : 노드의 포트에서 액세스할 수 있음 
    - ![image](https://user-images.githubusercontent.com/47103479/210375988-7c0a5430-5eb5-4aa2-8fb7-f85f996b3478.png)
    - 노드 포트는 30,000 에서 32,767 사이의 유효한 범위에만 있을 수 있음 
    - ![image](https://user-images.githubusercontent.com/47103479/210376241-e69a3d70-b2e3-48e6-96cb-53fcddaeb514.png)
      - selector를 이용해서 파드를 연결함 
    - > kubectl create -f service-definition.yml
    - > kubectl get services
    - > curl http://192.168.1.2:30008
    - ![image](https://user-images.githubusercontent.com/47103479/210377285-e6c5752c-765c-4169-823e-4bbc0cb9ca82.png)
      - 단일 파드, 단일 노드, 단일 노드의 여러 파드에서 서비스는 동일하게 생성됨. 파드가 제거되거나 추가되면 서비스가 자동으로 업데이트되고 매우 유연하고 적응력있음  
  - ClusterIP : 서로 다른 서비스간에 소통을 가능하게 하는 가상 IP를 생성함 
    - IP는 정적이 아님. 파드는 언제든지 다운될 수 있고 항상 새로운 파드가 생성됨 -> 응용 프로그램 간에 내부 통신을 위해 IP주소에 의존할 수 없음 
    - ![image](https://user-images.githubusercontent.com/47103479/210381936-00337001-ca88-4fd8-8c14-d87149cac1bd.png)
      - 쿠버네티스 클러스터에서 쉽게 마이크로 서비스 기반 애플리케이션을 효과적으로 포할 수 있음. 각 레이어의 크기를 조정할 수 있고 커뮤니케이션에 영향을 주지 않고 다양한 서비스 사이를 필요에 따라 이동가느함. 
      - 각 서비스에는 IP와 이름이 할당됨(클러스터 내부에서 사용해야 하는 이름). 다른 파드에서 서비스에 액세스하는데 이를 클러스터 IP라 칭함 
    - ![image](https://user-images.githubusercontent.com/47103479/210382648-47a042f3-53c8-4602-b19a-96fde5aa3d77.png)
      - > kubectl create -f service-definition.yml
      - > kubectl get services
  - LoadBalancer : 클라우드 공급자에서 애플리케이션을 위한 로드 밸런서를 지원함. 부하를 분산시킴 
    - 작업자 노드 포트에서 외부 응용 프로그램을 사용할 수 있도록 도움
    - 로드밸러서용 새 VM을 설치함, AJ/Proxy 또는 nginx등과 같은 적합한 로드밸런서를 설치 및 구성, 트래픽을 라우팅하도록 기본 노드에 로드 밸런서를 구성함 

# NameSpace
- ![image](https://user-images.githubusercontent.com/47103479/210569294-87074577-81d2-4dc0-9935-c0abc966a6b5.png)
  - 파드와 같은 객체 생성, 클러스터의 배포 및 서비스 등을 namespace 공간에서 해옴. 클러스터가 처음 설정될 때 쿠버네티스에 의해 자동으로 생성됨 
  - Kube-system은 내부 목적으로 네트워킹 솔루션에 필요한 DNS 서비스 등 사용자로부터 격리하고 실수로 삭제하는것을 방지하기 위해 다른 namespace 공간에 생성함 
  - kube-public은 모든 사용자가 자원을 사용할 수 있어야 함
- ![image](https://user-images.githubusercontent.com/47103479/210570671-cf50e500-e89c-4399-8558-7b49cf8c0c42.png)
- > kubectl get pods --namespace=kube-system : 다른 네임스페이스에 있는 파드들도 나열 
- > kubectl create -f pod-definition.yml --namespace=dev : 다른 네임스페이스 파드 생성 
- > kubectl create namespace dev : 네임스페이스 생성 
- ![image](https://user-images.githubusercontent.com/47103479/210570713-350b6d7a-01d7-4925-a84c-7487b9bb316b.png)
  - > kubectl config set-context $(kubectl config current-context) --namespace=dev : 현재 컨텍스트의 네임스페이스를 dev로 설정 
  - > kubectl get pods --all-namespace
- ![image](https://user-images.githubusercontent.com/47103479/210570969-c58461f3-a619-4f5d-b46d-8e1ad1aa875b.png)

# Imperative vs Declarative
- Infrastructure as Code
  - Imperative
    - 1. VM이 필요함
    - 2. NGINX 소프트웨어를 설치해야함 
    - 3. 포트를 8080으로 설정
    - 4. 웹 파일 경로를 정의함
    - 5. 애플리케이션 소스 코드가 저장되는 위치 지정 
    - 6. NGINX 서버 실행 
  - Declarative
    - VM Name : web-server
    - Package : nginx
    - Port : 8080
    - Path : /var/www/nginx
    - Code : GIT Repo -X
- Kubernetes
  - Imperative
    - Create Objects
      - kbectl run --image=nginx nginx
      - kubectl create deployment --image=nginx nginx
      - kubectl expose deployment nginx --port 80
    - Update Objects
      - kubectl edit deployment nginx
      - kubectl scale deployment nginx --replicas=5
      - kubectl set image deployment nginx nginx=nginx:1.18
    - kubectl create -f nginx.yaml
    - kubectl replace -f nginx.yaml
    - kubectl delete -f nginx.yaml
  - Declarative 
    - Create Objects
      - kubectl apply -f nginx.yaml
    - Update Objects
      - kubectl apply -f /path/to/config-files
      - kubectl apply -f nginx.yaml
- Declarative의 경우 단계별 지침을 제공하지 않음. 최종 목적지만 선언함. 목적지에 도달하기 위해 어떻게 할 것이 아니라 무엇을 할 것인지 지정하는 것 
  - 오케스트레이션 툴 : Ansible, Puppet,Chef, Terraform
- 명령형(Imperative) 접근 방식 항상 현재 구성을 알고 있어야 하므로 관리자에게 매우 부담스러움 
- kubectl apply -f nginx.yaml
  - Local file, Kubernets, JSON 세 개의 섹션을 비교하게됨
  - 쿠버네티스 클러스터 자체에 annotations: kubectl.kubernetes.io/last-applied-configuration:{JSON} 형태로 저장됨.

# tips
- --dry-run: 기본적으로 명령이 실행되는 즉시 리소스가 생성됨
  - 단순히 명령을 테스트하려는 경우 --dry-run=client옵션을 사용. 리소스를 생성하는 것이 아니라 리소스를 생성할 수 있는지 여부와 명령이 올바른지 여부를 알려줌
- -o yaml: 리소스 정의를 YAML 형식으로 화면에 출력함 
- ```bash
  # NGINX 포드 생성
  kubectl run nginx --image=nginx
  
  # POD 매니페스트 YAML 파일(-o yaml)을 생성합니다. 만들지 마세요(--드라이런)
  kubectl run nginx --image=nginx --dry-run=client -o yaml

  # 배포 만들기
  kubectl create deployment --image=nginx nginx

  # 배포 YAML 파일(-o yaml)을 생성합니다. 만들지 마세요(--드라이런)
  kubectl create deployment --image=nginx nginx --dry-run=client -o yaml

  # 4개의 복제본으로 배포 생성
  kubectl create deployment nginx --image=nginx --replicas=4
  kubectl scale deployment nginx --replicas=4
  kubectl create deployment nginx --image=nginx --dry-run=client -o yaml > nginx-deployment.yaml

  # 포트 6379에서 포드 redis를 노출하기 위해 ClusterIP 유형의 redis-service라는 서비스를 만듭니다.
  kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
  kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml
  
  # NodePort 유형의 nginx라는 서비스를 만들어 노드의 포트 30080에서 포드 nginx의 포트 80을 노출합니다.
  kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml
  kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml
  ```
