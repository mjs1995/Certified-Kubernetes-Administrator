# study 
- [Day20](#setup---kubeadm)<br>

# setup - kubeadm
- Kubernetes 클러스터는 다양한 구성 요소로 구성됩니다.
- 높은 수준에서 큐브 관리 도구를 사용하여 Kubernetes 클러스터를 설정하는 단계
  - 여러 시스템이 있어야 합니다. 또는 프로비저닝된 가상 머신 클러스터를 구성합니다.
  - 호스트에서 컨테이너 런타임을 설치하는 것입니다.(도커 사용) 
  - 모든 노드에서 Cube 관리 도구를 설치하는 것입니다. Cube 관리 도구는 쿠버네티스 솔루션 설치 및 구성을 통해 필요한 모든 구성 요소 올바른 노드에서 올바른 순서로 부트스트랩을 지원합니다.
  - 마스터 서버를 초기화하는 것입니다. 마스터가 초기화되면 작업자 노드를 마스터에 결합하기 전에 네트워크 전제 조건이 충족되었는지 확인해야 합니다.
  - Kubernetes에는 마스터 노드와 작업자 노드 사이 특별한 네트워킹 솔루션이 필요합니다. Pod 네트워크라고 합니다.
- https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

# Deploy with Kubeadm - Provision VMs with Vagrant
- 전제 조건으로, VirtualBox와 Vagrant가 설치되어 있어야 합니다.
- > git clone https://github.com/kodekloudhub/certified-kubernetes-administrator-course.git
- > vi Vagrantfile 
- > vagrabt status
- > vagrant up 
- > vagrant ssh kubemaster 
- > uptime
- > vagrant  ssh kubenode01 / vagrant  ssh kubenode02
- > cat /etc/hostname
