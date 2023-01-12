# study
- [Day10](#operating-system-upgrade)<br>
- [Day11](#backup-and-restore)<br>

# Operating System Upgrade 
- ![image](https://user-images.githubusercontent.com/47103479/211800058-b6e88906-62aa-4643-a3a6-82aba9f6c281.png)
  - 노드 중 하나가 다운 되면 그들에 있는 파드에 액세스 할 수 없음. 파드를 배포한 방법에 따라 사용자가 영향을 받을 수 있음 
  - 노드가 5분 이상 다운된 경우 파드는 해당 노드에서 종료됨. 쿠버네티스는 죽은 것으로 간주함 
  - pod-eviction-timeout은 파드가 다시 온라인 상태가 될 때까지 기다리는 시간. 노드가 죽은 것으로 간주하기 전에 최대 5분 동안 노드가 오프라인이 될 때마다 마스터 노드는 대기함  
  - 클러스터의 다른 노드에 워크로드가 이동되도록 모든 워크로드의 노드를 의도적으로 비울 수 있음 . 노드를 비우면 Pod가 정상적으로 종료됨.(노드를 재부팅 할 수 있음) 
- > kubectl drain node-1
- > kubectl cordon node-2
- > kubectl uncordon node-1
  - cordon은 단순히 노드를 예약 불가로 표시하며 drain과 달리 종료되지 않고 기존 노드에서 파드를 이동함  

# Kubernetes Software Versions 
- ![image](https://user-images.githubusercontent.com/47103479/211804179-81070d02-1b00-4955-9886-a20b50d1ab04.png)
  - 마이너 버전은 새로운 특징과 기능으로 몇 달마다 릴리스됨 
  - 패치는 중요한 버그 수정과 함께 더 자주 릴리스됨 
- ![image](https://user-images.githubusercontent.com/47103479/211804507-4275f382-9cb9-45d6-b540-2db426569a6e.png)
  - 알파는 태그가 지정된 알파 릴리스로 이동하여 기능이 기본적으로 비활성화 되어 있어 버그가 있을 수 있음 
  - 베타 릴리스는 코드가 잘 테스트되는 곳으로 새 기능은 기본적으로 활성화 되어 있음 
  - 메인 안정 릴리스는 릴리스 페이지에서 모든 릴리스를 찾을 수 있음 
- ![image](https://user-images.githubusercontent.com/47103479/211805772-196e6e76-ef19-4a8a-b994-aeb7dc11cdf0.png)

# Cluster Upgrade Process 
- ![image](https://user-images.githubusercontent.com/47103479/211806413-3c64c0b2-5302-424b-bb0a-928ca3b21d22.png)
  - 구성 요소는 다를 릴리스 버전에 있을 수 있음. kube API 서버가 컨트롤 플레인에서 기본 구성 요소이고 다른 모든 구성 요소가 통신함. kube API 서버보다 높은 버전에서 다른 구성 요소 중 어느 것도 없어야 합니다. 
- 하나의 버전으로 업그레이드 하는것을 권장함 
- ![image](https://user-images.githubusercontent.com/47103479/211806867-2176bed0-d8ee-419a-8078-f661a8dcd793.png)
  - 업그레이드 프로세스는 클러스터 설정 방법에 따라 다름 
  - Google Kubernets 엔진을 사용하면 클러스터를 몇 번의 클릭만으로 쉽게 업그레이드 할 수 있음. 혹은 kubeadm을 사용하거나 클러스터를 처음부터 배포한 경우 다른 구성 요소를 수동으로 업그레이드 
- ![image](https://user-images.githubusercontent.com/47103479/211807549-290fbfd5-1fdf-4ecb-a241-590693d14348.png)
  - 마스터 노드를 업그레이드 한 다음 작업자 노드를 업그레이드 함 
  - 마스터가 업그레이드 되는 동안, API 서버와 같은 컨트롤 플레인 구성 요소, 스케줄러 및 컨트롤러는 잠시 다운됨 
  - 마스터가 다운되었기 때문에 사용자에게 정상적으로 서비스를 제공하기 위해 작업자 노드에서 호스팅되는 모든 워크로드는 계속됨 
- 전략
  - 한 번에 모두 업그레이드 함. 파드가 다운되고 사용자는 더 이상 응용 프로그램에 액세스할 수 없음 
  - 한 번에 하나의 노드를 업그레이드 하는것. 
  - 클러스터에 새 노드(최신 소프트웨어 버전의 노드) 를 추가하는 것. 클라우드 환경이라면 편리함 
- ![image](https://user-images.githubusercontent.com/47103479/211808422-bff29e6e-d31e-45af-b1dd-acd34811c914.png)
  - > kubeadm upgrade plan
- 1.11ver에서 1.13ver으로 업그레이드
  - > apt-get upgrade -y kubeadm=1.12.0-00
  - > kubeadm upgrade apply v1.12.0
  - > kubectl get nodes
  - > apt-get upgrade -y kubelet=1.12.0-00 
  - > systemctl restart kubelet
  - > kubectl get nodes
  - ![image](https://user-images.githubusercontent.com/47103479/211809442-a070deb3-94fc-4782-aa5b-b57c4cfe048a.png)
  - ![image](https://user-images.githubusercontent.com/47103479/211809660-2f841f75-b0ec-4954-a768-3fc14efc85b3.png)
    - > kubectl drain node-1
    - > apt-get upgrade -y kubeadm=1.12.0-00
    - > apt-get upgrade -y kubeadm=1.12.0-00
    - > kubeadm upgrade node cofig --kubelet-version v1.12.0
    - > systemctl restart kubelet 
  - ![image](https://user-images.githubusercontent.com/47103479/211809911-49dbaaa6-4cc4-48b4-b23e-41624d32e321.png)
    - > kubectl uncordon node-1
    - > kubectl drain node-2
    - > kubectl uncordon node-2
    - > kubectl drain node-3
    - > kubectl uncordon node-3
- https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/
- 실습환경 : katacoda.com/courses/kubernetes/playground

# Backup and Restore 
- Resource Configs
  - 클러스터에서 생성한 리소스와 관련해서 때때로 객체를 생성하는 명령형 방법을 사용함
    - > kubectl create namespace new-namespace
    - > kubectl create secret
    - > kubectl create configmap 
    - > kubectl apply –f pod-definition.yaml 
    - > kubectl get all --all-namespaces -o yaml > all-deploy-services.yaml : 백업스크립트에서 사용할 수 있는 모든 파드 및 배포를 가져오는 것 
- ETCD
  - etcd 클러스터는 클러스터의 상태에 대해 정보를 저장함 . 클러스터 내에서 생성되는 노드 및 기타 모든 리소스는 저장됨 
  - ![image](https://user-images.githubusercontent.com/47103479/212066033-5d77cbcd-6b8b-49ac-be2a-ea25e062d174.png)
  - ETCD에는 내장 스냅샷 솔루션도 함께 제공되어 데이터베이스의 스냅샷을 만들 수 있음 
  - ![image](https://user-images.githubusercontent.com/47103479/212066105-b3505a42-4a41-4dbf-8b18-657fb3c72313.png)
    - > ETCDCTL_API=3 etcdctl \ snapshot save snapshot.db
    - > ETCDCTL_API=3 etcdctl \ snapshot status snapshot.db
    - > service kube-apiserver stop : 백업하려면 먼저 종료
    - > ETCDCTL_API=3 etcdctl \
        snapshot restore snapshot.db \
        --data-dir /var/lib/etcd-from-backup \
        --initial-cluster master-1=https://192.168.5.11:2380,master-2=https://192.168.5.12:2380 \
        --initial-cluster-token etcd-cluster-1 \
        --initial-advertise-peer-urls https://${INTERNAL_IP}:2380
    - > systemctl daemon-reload
    - > service etcd restart
    - > service kube-apiserver start
- etcdctl snapshot save -h필수 글로벌 옵션을 기록, etcdctl snapshot restore -h 스냅샷 복원에 대한 옵션 
  - --cacert 이 CA 번들을 사용하여 TLS 지원 보안 서버의 인증서를 확인합니다.
  - --cert이 TLS 인증서 파일을 사용하여 보안 클라이언트 식별
  - --endpoints=[127.0.0.1:2379] ETCD가 마스터 노드에서 실행되고 localhost 2379에 노출되기 때문에 이것이 기본값
  - --key이 TLS 키 파일을 사용하여 보안 클라이언트 식별
      - > ETCDCTL_API=3 etcdctl \
          snapshot save snapshot.db \
          --endpoints=https://127.0.0.1:2379 \
          --cacert=/etc/etcd/ca.crt \
          --cert=/etc/etcd/etcd-server.crt \
          --key=/etc/etcd/etcd-server.key
- 관리형 쿠버네티스 환경에서는 etcd 클러스터에 액세스 하지 못할 수 있어서 Kube API 서버에 쿼리하여 백업하기 
