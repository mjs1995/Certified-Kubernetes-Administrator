# study
- [Day21](#application-failure)<br>

# Application Failure
- Check Service Status
  - ![image](https://user-images.githubusercontent.com/47103479/215324638-57020c13-83ba-4ae1-866b-0e0d21b2d2d5.png)
  - > curl http://web-service-ip:node-port
  - > kubectl describe service web-service
- Check Pod
  - ![image](https://user-images.githubusercontent.com/47103479/215324667-322c3ff3-edf7-4b53-ade7-eed02474d237.png)
  - 실행 중 상태, 포드 상태 및 재시작 횟수 확인 
  - > kubectl get pod
  - > kubectl describe pod web
  - > kubectl logs web -f --previous

# Control Plane Failure
- Check Node Status
  - > kubectl get nodes
  - > kubectl get pods
- Check Controlplane Pods
  - > kubectl get pods -n kube-system
- Check Controlplane Services
  - > service kube-apiserver status
  - > service kube-controller-manager status
  - > service kube-scheduler status
  - > service kubelet status
  - > service kube-proxy status
- Check Service Logs
  - > kubectl logs kube-apiserver-master -n kube-system
  - > sudo journalctl -u kube-apiserver

# Worker Node Failure 
- Check Node
  - > kubectl get nodes
  - > kubectl describe node worker-1
  - ![image](https://user-images.githubusercontent.com/47103479/215484959-e80a3afb-85ed-45f7-bde4-8f550abce8ee.png)
  - > top : 노드에서 가능한 CPU 메모리 및 디스크 공간을 확인
  - > df - h : 노드에서 가능한 CPU 메모리 및 디스크 공간을 확인
- Check Kubelet Status 
  - ![image](https://user-images.githubusercontent.com/47103479/215485072-4c377ba6-8052-41b2-9588-448d07a25bc8.png)
  - > service kubelet status
  - > sudo journalctl –u kubelet
- Check Certificates
  - ![image](https://user-images.githubusercontent.com/47103479/215485125-b8898c31-2553-41d1-874e-56d1e9c07e1e.png)
  - > openssl x509 -in /var/lib/kubelet/worker-1.crt -text

# Network Plugin in Kubernetes
- cni-bin-dir : Kubelet은 시작 시 이 디렉토리에서 플러그인을 검색합니다.
- network-plugin: cni-bin-dir에서 사용할 네트워크 플러그인입니다. 플러그인 디렉토리에서 검색된 플러그인이 보고한 이름과 일치해야 합니다.
- Weave Net
  - > kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
- Flannel 
  - > kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/2140ac876ef134e0ed5af15c65e414cf26827915/Documentation/kube-flannel.yml
- Calico 
  - > curl https://docs.projectcalico.org/manifests/calico.yaml -O
  - > kubectl apply -f calico.yaml
- coreDNS와 관련된 문제 해결
  - 1. CoreDNS 포드가 보류 상태인 경우 먼저 네트워크 플러그인이 설치되어 있는지 확인하십시오.
  - 2. coredns 포드에 CrashLoopBackOff 또는 오류 상태 가 있습니다.
    - 이전 버전의 Docker와 함께 SELinux를 실행하는 노드가 있는 경우 coredns 포드가 시작되지 않는 시나리오가 발생할 수 있습니다. 이를 해결하기 위해 다음 옵션 중 하나를 시도할 수 있습니다.
    - a) 최신 버전의 Docker로 업그레이드합니다.
    - b) SELinux를 비활성화합니다.
    - c) allowPrivilegeEscalation 을 true 로 설정하도록 coredns 배포를 수정합니다.
      - ```shell
        kubectl -n kube-system get deployment coredns -o yaml | \
        sed 's/allowPrivilegeEscalation: false/allowPrivilegeEscalation: true/g' | \
        kubectl apply -f -
        ```
    - d) CoreDNS가 CrashLoopBackOff 를 갖는 또 다른 원인은 Kubernetes에 배포된 CoreDNS 포드가 루프를 감지하는 경우입니다.
      - kubelet 구성 yaml에 다음을 추가합니다. resolvConf: <path-to-your-real-resolv-conf-file> 이 플래그는 kubelet 이 포드 에 대체 resolv.conf 를 전달하도록 지시합니다. systemd-resolved 를 사용하는 시스템 의 경우 /run/systemd/resolve/resolv.conf 는 일반적으로 "실제" resolv.conf 의 위치 이지만 배포판에 따라 다를 수 있습니다.
      - 호스트 노드에서 로컬 DNS 캐시를 비활성화하고 /etc/resolv.conf 를 원본으로 복원합니다.
      - 빠른 수정은 Corefile 을 편집하여 forward 를 바꾸는 것입니다 . /etc/resolv.conf 를 업스트림 DNS의 IP 주소(예: forward )로 바꿉니다 . 8.8.8.8 . 그러나 이것은 CoreDNS 에 대한 문제만 수정합니다 . kubelet 은 잘못된 resolv.conf 를 모든 기본 dnsPolicy 포드에 계속 전달하여 DNS를 확인할 수 없게 합니다.
  - 3. CoreDNS 포드와 kube-dns 서비스가 제대로 작동하는 경우 kube-dns 서비스에 유효한 엔드포인트 가 있는지 확인합니다 .
    - > kubectl -n kube-system get ep kube-dns
- kube-proxy 
  - kube-proxy 는 클러스터의 각 노드에서 실행되는 네트워크 프록시입니다
  - > kubectl describe ds kube-proxy -n kube-system
  - ![image](https://user-images.githubusercontent.com/47103479/215489658-caaf3c58-0c12-493d-852d-34ff4c6d7d57.png)
  - kube-proxy와 관련된 문제 해결
    - 1. kube-system 네임스페이스 의 kube -proxy 포드 가 실행 중인지 확인합니다.
    - 2. kube-proxy 로그를 확인합니다.
    - 3. configmap 이 올바르게 정의되어 있고 kube-proxy 바이너리를 실행하기 위한 구성 파일이 올바른지 확인합니다.
    - 4. kube-config 는 구성 맵 에 정의되어 있습니다.
    - 5. kube-proxy 가 컨테이너 내부에서 실행 중인지 확인
    - ![image](https://user-images.githubusercontent.com/47103479/215489771-b28091ae-9be6-43c0-b99d-2c2d5173e765.png)
    - > netstat -plan | grep kube-proxy

