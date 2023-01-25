# study
- [Day16](#linux-networking-basics)<br>
- [Day17](#dns)<br>
- [Day18](#cni-in-kubernetes)<br>

# Linux Networking Basics
- Networking Pre-Requisites
  - ![image](https://user-images.githubusercontent.com/47103479/214087391-17a1791e-a2c4-4191-8581-9b0bc1f4ead1.png)
- Switching
  - 스위치는 두 시스템을 포함하는 네트워크를 생성함
  - ![image](https://user-images.githubusercontent.com/47103479/214087663-721b0d17-caa9-4c6c-beab-f292dc6b3914.png)
  - > ip link : 호스트의 수정 인터페이스를 나열함 
  - > ip addr : 할당된 IP 주소를 확인함 
  - > ip addr add 192.168.1.10/24 dev eth0 : 해당 인터페이스에 IP 주소 추가 명령
- Routing
  - 라우터는 두 네트워크를 함께 연결하는 데 도움이 됨
  - 라우터는 네트워크의 또 다른 장치일 뿐
  - ![image](https://user-images.githubusercontent.com/47103479/214088180-fc8770d5-ead9-411e-b9b3-4f859fac1ba2.png)
- Gateway
  - 네트워크가 방이라면,Gateway는 다른 네트워크나 인터넷으로 외부 세계로 통하는 문
  - ![image](https://user-images.githubusercontent.com/47103479/214088868-7c5eb8ad-27e8-46a9-84d3-9246fb95084d.png)
  - > route : IP 경로 또는 단순히 경로 명령 
  - > ip route show # ip route list : 라우팅 테이블을 보는데 사용됨  
  - > ip route add 192.168.1.0/24 via 192.168.2.1 : IP 경로 추가 명령 
- ![image](https://user-images.githubusercontent.com/47103479/214089611-147c1b53-c388-411d-a500-ccc13e3dbbf7.png)
  - 호스트 A에게 문이 또는 네트워크 2의 게이트웨이는 호스트 B를 함.라우팅 테이블 항목을 추가하여 이를 수행함
  - > ip route add 192.168.2.0/24 via 192.168.1.6
  - > ip route add 192.168.1.0/24 via 192.168.2.6
  - > ping 192.168.2.5 # 라우팅 항목이 옳음 
- ![image](https://user-images.githubusercontent.com/47103479/214090383-30ed87f9-f81a-4c09-86ab-eac8634a701f.png)
  - 한 네트워크에서 다른 네트워크로 호스트가 패킷을 전달할 수 있는지 여부는 인터페이스 간은 설정에 의해 관리됨
  - > cat /proc/sys/net/ipv4/ip_forward # 없음 : 호스트에서 IP 전달이 활성화된 경우 확인 명령 
  - > echo 1 > /proc/sys/net/ipv4/ip_forward # 1로 설정하면 핑이 통과하는 것을 볼 수 있음 

# DNS
- ![image](https://user-images.githubusercontent.com/47103479/214216152-8d4fd3d4-36e0-474d-9915-85d1d9a5a9a6.png)
  - > cat >> /etc/hosts
  - > ping db
  - > ssh db
  - > curl http://www.google.com
- name resolution
  - ![image](https://user-images.githubusercontent.com/47103479/214216386-5dfe15ae-872d-44e3-aaf4-bbc2e1ed85ae.png)
  - DNS서버는 중앙에서 관리할 단일 서버 
- DNS
  - ![image](https://user-images.githubusercontent.com/47103479/214216518-16a829af-a499-4b69-8df2-b672dc7f9a15.png)
  - > cat /etc/resolv.conf
  - > cat /etc/nsswitch.conf
- Domain Names
  - ![image](https://user-images.githubusercontent.com/47103479/214216888-97708f2b-9081-4714-bab4-482b6d0b8f23.png)
  - 상업용 또는 일반 용도의 Dot.com,네트워크용 Dot.net,교육 기관을 위한 Dot.edu,비영리 조직의 경우 .org.
  - ![image](https://user-images.githubusercontent.com/47103479/214216997-1cba041e-c930-4327-b17d-d6fbc017ff93.png)
  - ![image](https://user-images.githubusercontent.com/47103479/214217057-e30cbcbf-5142-4912-8548-ad597167f603.png)
- Record Types
  - ![image](https://user-images.githubusercontent.com/47103479/214217491-f42218ad-b7c7-4e12-a39a-a0f869bb69b9.png)
  - A레코드 : 호스트 이름에 IP를 저장한다는 것을 알고 있음. IPv6을 호스트 이름에 저장하는 것을 쿼드 A 레코드
  - CNAME 레코드 : 한 이름을 다른 이름에 매핑하는 것
- nslookup
  - ![image](https://user-images.githubusercontent.com/47103479/214217641-3c68f0b0-0af9-43df-acdb-8021798a795a.png)
  - nslookup을 사용하여 DNS 서버에서 호스트 이름을 쿼리할 수 있음. DNS 서버만 쿼리함
  - > nslookup www.google.com
- dig
  - ![image](https://user-images.githubusercontent.com/47103479/214217599-482ad375-1437-42e2-9e73-7ec747284f44.png)
  - Dig는 DNS 이름 확인을 테스트하는 또 다른 유용한 도구

# CoreDNS
- ![image](https://user-images.githubusercontent.com/47103479/214217825-771e405a-72f2-4b67-820c-e562dce75ac3.png)
  - > wget https://github.com/coredns/coredns/releases/download/v1.7.0/coredns_1.7.0_linux_amd64.tgz : Installation of CoreDNS
  - > tar -xzvf coredns_1.7.0_linux_amd64.tgz : Extract tar file
  - > ./coredns : Run the executable file
- ![image](https://user-images.githubusercontent.com/47103479/214217847-5aa31e7b-7a61-494d-a199-4990eab55b21.png)
  - > cat > /etc/hosts : Configuring the hosts file
  - > cat > Corefile : Adding into the Corefile
  - > ./coredns : Run the executable file

# Network Namespaces
- > ps aux
- 호스트에는 나머지 네트워크에 대한 정보와 함께 자체 라우팅 및 ARP 테이블이 있음 
- create network ns
  - > ip netns add red : Linux 호스트에서 새 네트워크 네임스페이스를 생성
  - > ip nets : 네트워크 네임스페이스를 나열하려면 ip netns 명령을 실행
  - > ip link : 내 호스트의 인터페이스를 나열
- Exec in Network Namespace
  - > ip netns exec red ip link
  - > ip -n red link : 네임스페이스 내에서 ip 명령을 실행하려는 경우
  - 호스트에서 ARP 명령을 실행하면 항목 목록이 표시되고 하지만 컨테이너 내부에서 실행하면 항목이 표시되지 않습니다. 라우팅 테이블도 마찬가지입니다.
  - > arp
  - > route
- Virtual Cable
  - > ip link add veth-red type veth peer name veth-blue : 케이블 만듬 
  - > ip link set veth-red netns red / ip link set veth-blue netns blue : 네임스페이스 연결 
  - > ip -n red addr add 192.168.15.1/24 dev veth-red / ip -n blue addr add 192.168.15.2/24 dev veth-blue : ip 주소 할당 
  - > ip -n red link set veth-red up / ip -n blue link set veth-blue up : ip 링크 설정 명령 사용하여 인터페이스 불러옴
  - > ip netns exec red ping 192.168.15.2
  - > ip netns exec red arp / ip netns exec blue arp : ARP 테이블 나열 
  - > arp : 이것을 호스트의 ARP 테이블과 비교하면,우리가 만든 새 네임스페이스에 대해 호스트 ARP 테이블이 전혀 모른다는 것을 알 수 있음 
  - 호스트 내 가상 스위치 생성
    - LINUX BRIDGE, Open vSwitch
- linux Bridge
  - > ip link add v-net-0 type bridge 
  - > ip link
  - > ip link set dev v-net-0 up
  - > ip -n red link del veth-red
  - > ip link add veth-red type veth peer name veth-red-br / ip link add veth-blue type veth peer name veth-blue-br : 네임스페이스를 연결하는 케이블을 만듬
  - > ip link set veth-red netns red
  - > ip link set veth-red-br master v-net-0
  - > ip link set veth-blue netns blue
  - > ip link set veth-blue-br master v-net-0
  - > ip -n red addr add 192.168.15.1/24 dev veth-red / ip -n blue addr add 192.168.15.2/24 dev veth-blue : 네임스페이스와 브리지 네트워크 연결 
  - > ip -n red link set veth-red up / ip -n blue link set veth-blue up
  - > ip addr add 192.168.15.5/24 dev v-net-0
  - > ip link set dev veth-red-br up / ip link set dev veth-blue-br up
  - on the ns
    - > ip netns exec blue ping 192.168.1.1
    - > ip netns exec blue route
    - > ip netns exec blue ip route add 192.168.1.0/24 via 192.168.15.5
    - 이제 호스트에는 두 개의 IP 주소가 있음. 1925.168.15.5의 브리지 네트워크에 있는 하나, 다른 하나는 192.168.1.2의 외부 네트워크에 있음 
    - > ip a : Check the IP Address of the host
    - > iptables -t nat -A POSTROUTING -s 192.168.15.0/24 -j MASQUERADE : 포스트 라우팅 체인에서 NAT IP 테이블에 새 규칙 추가
    - > ip netns exec blue ping 192.168.1.1
    - > ip netns exec blue ping 8.8.8.8
    - > ip netns exec blue route
    - > ip netns exec blue ip route add default via 192.168.15.5 : 호스트를 지정하는 기본 게이트 웨이를 추가
    - 현재 네임스페이스는 내부 사설망에서 외부 세계의 아무도 그들에 대해 알지 못함
    - > iptables -t nat -A PREROUTING --dport 80 --to-destination 192.168.15.2:80 -j DNAT : 다른 옵션은 포트 전달 역할을 추가하는 것으로 IP 테이블을 사용하여 포트 80으로 들어오는 모든 트래픽을 말함
    - > iptables -nvL -t nat

# Docker Networking
- None Network
  - > docker run --network none nginx
- Host
  - > docker run --network host nginx
- Bridge Network
  - > docker run --network bridge nginx
  - > docker network ls
  - > ip link 
  - > ip link add docker0 type bridge
  - > ip addr 
  - > ip netns : 네임스페이스 나열 
  - > docker inspect <container-id> : 각 컨테이너와 연결된 네임스페이스를 볼 수 있음 
  - > ip -n 04acb487a641 link
  - > ip -n 04acb487a641 addr
- NAT 규칙
  ```shell
  iptables \
           -t nat \
           -A PREROUTING \
           -j DNAT \
           --dport 8080 \
           --to-destination 80

  iptables \
        -t nat \
        -A DOCKER \
        -j DNAT \
        --dport 8080 \
        --to-destination 172.18.0.6:80
  ```
  - > iptables -nvL -t nat : IP 테이블에 규칙을 나열

# CNI
- CNI(컨테이너 네트워크 인터페이스) : 컨테이너 런타임 환경에서 네트워킹 문제를 해결하기 위해 프로그램을 개발하는 방법을 정의하는 일련의 표준
- ![image](https://user-images.githubusercontent.com/47103479/214223959-d9ea4a93-0628-45fd-b2bd-4882b26d5b47.png)
- ![image](https://user-images.githubusercontent.com/47103479/214223922-946fab34-458a-4eed-8a3b-2e80fd5f0564.png)
- > bridge add 2e34dcf34 /var/run/netns/2e34dcf34 : 특정 네트워크 이름 공간에 컨테이너를 추가함 
- > bridge add <id> <namespace>
- CNI은 플러그인 개발 방법을 정의함 
- CNI은 일련의 책임을 정의함 
  - ![image](https://user-images.githubusercontent.com/47103479/214224438-91107beb-c0b2-4d0e-b9d0-1da02c1b1b9b.png)
- CNI는 이미 지원되는 플러그인 세트와 함께 제공됨
  - ![image](https://user-images.githubusercontent.com/47103479/214224604-d566506f-32a3-48b5-8619-f9a7a206b535.png)
  - Docker는 CNI를 구현하지 않습니다.Docker에는 CNM(컨테이너 네트워크 모델)이라는 자체 표준 세트가 있습니다.

# Networking Cluster Nodes 
- ![image](https://user-images.githubusercontent.com/47103479/214224883-6478397e-5407-474b-9437-c655e0e7bf9a.png)
- ![image](https://user-images.githubusercontent.com/47103479/214224917-fd81fd60-ead3-4c1f-8d84-255dcc8bfc30.png)
- ![image](https://user-images.githubusercontent.com/47103479/214224984-6c6432f5-ef6c-4f70-8e10-ecb2a6a9a435.png)
- ![image](https://user-images.githubusercontent.com/47103479/214225042-82e7f300-1c9f-4064-a7dc-69b2ca74fc05.png)
  - https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#check-required-ports
- Commands
  - > ip link
  - > ip addr
  - > ip addr add 192.168.1.10/24 dev eth0
  - > ip route
  - > ip route add 192.168.1.0/24 via 192.168.2.1
  - > cat /proc/sys/net/ipv4/ip_forward
  - > route
  - > arp
  - > netstat -plnt

# POD Networking Concepts 
- ![image](https://user-images.githubusercontent.com/47103479/214294903-83a943ca-4209-44cd-bc7b-df43c50cfb45.png)
  - Pod 네트워킹 요구 사항 : Kubernetes는 고유한 IP 주소를 얻기 위해 모든 Pod를 기대함, 모든 포드는 동일한 노드 내의 다른 모든 포드에 도달하여 해당 IP 주소를 사용함
  - ![image](https://user-images.githubusercontent.com/47103479/214295166-7680403b-2eb7-49d6-b3da-087df3a49616.png)
  - ![image](https://user-images.githubusercontent.com/47103479/214295276-6c78e9dc-418f-4cf3-ae9e-f124cd7326c1.png
  - ![image](https://user-images.githubusercontent.com/47103479/214295541-c5587aaf-6e79-410e-a2b7-b4ce4767a9d7.png)
- ![image](https://user-images.githubusercontent.com/47103479/214296045-aaa82f39-0613-4dbd-bb05-368f2205a80c.png)
  - 모든 호스트가 이를 기본 게이트웨이로 사용하도록 지정합니다. 이렇게 하면 경로를 쉽게 관리할 수 있습니다.
- CNI는 쿠버네티스에게 컨테이너를 생성하자마자 스크립트를 호출하는 방법입니다
  - ![image](https://user-images.githubusercontent.com/47103479/214296463-05cdf505-484e-4cc6-ac21-8829d636376b.png)

# CNI in Kubernetes
- CNI는 CNI 컨테이너 실행 시간에 따른 컨테이너 실행 시간 책임을 정의합니다.
  - Container Runtime must create network namespace
  - Identify network the container must attach to
  - Container Runtime to invoke Network Plugin (bridge) when container is ADDed.
  - Container Runtime to invoke Network Plugin (bridge) when container is DELeted.
  - JSON format of the Network Configuration  
- ![image](https://user-images.githubusercontent.com/47103479/214322348-d0f3b7ce-0a8e-41d8-9d1f-98214c4d1f6d.png)
  - ![image](https://user-images.githubusercontent.com/47103479/214322397-2879859b-3a43-42df-ba3c-9390d0704bac.png)
  - > ps -aux | grep kubelet
  - > ls /opt/cni/bin : CNI bin 디렉터리에는 지원되는 모든 CNA 플러그인이 있음 
  - > ls /etc/cni/net.d : CNI 충돌 디렉토리에는 구성 파일 세트가 있음 
  - > cat /etc/cni/net.d/10-bridge.conf
    - ![image](https://user-images.githubusercontent.com/47103479/214322851-5d35e3a2-f6b3-4030-844e-521fdaa5ec23.png)

# WeaveWorks 
- ![image](https://user-images.githubusercontent.com/47103479/214323468-184fe142-283d-4766-816d-16ea09b428f4.png)
  - 회사의 각 사이트에 에이전트를 배치하여 사이트 간 모든 운송활동 관리를 담당함
  - ![image](https://user-images.githubusercontent.com/47103479/214324131-9b3942ab-ed15-4b2b-a19d-761c26750940.png)
- Deploy Weave
  - > kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
  - > kubectl get pods –n kube-system
  - > kubectl logs weave-net-5gcmb weave –n kube-system

# IPAM
- IP 주소 관리 
- ![image](https://user-images.githubusercontent.com/47103479/214561785-62b61fb7-2e8a-4622-87fd-889d4fcb2cd1.png)
  - CNI는 컨테이너에 IP 할당하고 관리할 네트워크 솔루션 공급자인 CNI 플러그인의 책임이라고 말합니다. 표준을 정의하는 사람들입니다. 
  - ![image](https://user-images.githubusercontent.com/47103479/214562064-ac822484-f9d0-4066-ae0b-533988183b11.png)
  - ![image](https://user-images.githubusercontent.com/47103479/214562111-ea283ef8-cfe1-440a-848a-946df2817f7c.png)
  - > cat /etc/cni/net.d/net-script.conf : ipam  섹션 확인(사용할 플러그인 유형 지정)  
- Weave는 기본적으로 IP 범위 10.32.0.0/12를 할당합니다.

# Service Networking 
- 클러스터 IP : 클러스터 내에서만 액세스할 수 있습니다
- ![image](https://user-images.githubusercontent.com/47103479/214565732-6df4f9d2-33d4-495d-a6e4-41b964a6c606.png)
- 서비스 객체를 생성할 때 쿠버네티스에서 미리 정의된 범위에서 IP 주소가 할당됩니다.
- > kube-proxy --proxy-mode [userspace | iptablkes | ipvs ] …
- > kubelet get pods -o wide
- > kubelet get service
- > kube-api-server --service-cluster-ip-range ipNet (Default: 10.0.0.0/24) : 클러스터 IP 범위 
- > ps aux | grep kube-api-server
- > iptables –L –t net | grep db-service
- > cat /var/log/kube-proxy.log

# Cluster DNS
- Objectives
  - What names are assigned to what objects?
  - Service DNS records
  - POD DNS Recrods
- ![image](https://user-images.githubusercontent.com/47103479/214570780-edecb350-2149-4eba-8ce7-1a8bc32021a8.png)
  - 서비스가 생성될 때마다 Kubernetes DNS 서비스는 서비스에 대한 레코드를 만듭니다. 서비스 이름을 IP 주소에 매핑합니다.
- ![image](https://user-images.githubusercontent.com/47103479/214571414-1b8dff10-31a8-4fde-8b53-ffcd54fc0d95.png)
  - 모든 서비스는 SVC라는 다른 하위 도메인으로 함께 그룹화됩니다.
  - 모든 서비스와 포드가 클러스터의 경로 도메인으로 함께 그룹화됩니다.

# How Kubernetes Implements DNS 
- ![image](https://user-images.githubusercontent.com/47103479/214571838-a1e80178-9acd-46a5-8fd3-d6d24aa50c09.png)
  - 서로 해결하는 쉬운 방법 각각의 etc 호스트 파일에 항목을 추가하는 것입니다. 수천 개의 포드가 있는 경우 적합하지 않음 
  - 다른 포드가 새 포드에 액세스할 수 있도록 포드에서 etc resolv.conf 파일을 구성하여 DNS 서버를 가리키도록 합니다.
- CoreDNS
  - ![image](https://user-images.githubusercontent.com/47103479/214572788-82e8336e-1a89-4985-8593-1f9131f462d0.png)   
  - coreDNS 서버는 Kubernetes 클러스터의 Kube 시스템 네임스페이스에서 포드로 배포됩니다.  
  - 복제 세트의 일부로 중복성을 위해 두 개의 팟(Pod)으로 배포됩니다.
  - CoreDNS에는 구성 파일이 필요합니다. 플러그인은 상태 보고, 지표 모니터링, 현금 등 오류를 처리하도록 구성되어 있습니다.
  - > kubectl get configmap –n kube-system
  - ![image](https://user-images.githubusercontent.com/47103479/214573025-fd70fcd0-3164-47d2-9add-41dd855db98d.png)
  - > kubectl get service –n kube-sytem
  - > cat /var/lib/kubelet/config.yaml
  - ![image](https://user-images.githubusercontent.com/47103479/214573309-357e3361-0c72-48a5-9abc-c5ab8da695f8.png)
  - ![image](https://user-images.githubusercontent.com/47103479/214594944-32f14d11-e6c8-4847-b9e0-bc0b6949b443.png)

# Ingress
- ![image](https://user-images.githubusercontent.com/47103479/214595618-332e6b76-a9d6-4cb2-84b9-227f983c787a.png)
  - 각 로드 밸런서에 대해 비용을 지불해야 합니다. 이러한 로드 밸런서를 많이 보유하면 역으로 클라우드 청구서에 영향을 미칩니다.
- ![image](https://user-images.githubusercontent.com/47103479/214595938-a60e95c5-bb79-42a3-9513-d6ca6922c5de.png)
  - Ingress는 다른 서비스로 라우팅하도록 구성할 수 있는 외부에서 액세스할 수 있는 단일 URL 사용하여 사용자가 애플리케이션에 액세스하도록 돕습니다.
- 배포하는 솔루션을 Ingress 컨트롤러, 세트를 구성하는 규칙 중 인그레스 리소스라고 함.인그레스 리소스는 정의 파일을 사용하여 생성됩니다.
- Ingress Controller
  - ![image](https://user-images.githubusercontent.com/47103479/214596367-8daf9b4e-6702-435b-8749-5a459b055461.png)
  - NGINX, Contour, HAProxy, Traefik, Astel 
  - ![image](https://user-images.githubusercontent.com/47103479/214597200-14b2f91b-b69d-4d69-99df-83bf4a7897d5.png)
