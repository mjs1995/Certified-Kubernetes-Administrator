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
