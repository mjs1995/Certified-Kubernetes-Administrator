# Certified-Kubernetes-Administrator
- ![image](https://user-images.githubusercontent.com/47103479/219952420-63607529-13da-4266-a203-d0c5fdb9ff2d.png)
- 최근 데이터 엔지니어가 다루는 대부분의 데이터 플랫폼이 Kubernetes를 기반으로 하는 곳이 많아지면서 데이터 파이프라인의 배포, 관리, 확장 등에 대한 전반적인 이해와 클러스터 자원의 효율적인 사용 및 장애 대응 능력을 기르고자 공부를 진행하였습니다. 
- CKA를 공부하면서 Kubernetes 클러스터에서 쿠버네티스 애플리케이션을 설치, 구성, 유지 관리 및 모니터링 스킬을 배웠으며 Kubernetes 클러스터에서 데이터 파이프라인을 운영을 할 때 도움이 될 거 같습니다.
- 2023년에 1월부터 CKA 스터디를 참여하고 2월에 CKA 자격증 시험을 보았습니다. 시험 관련해서 후기 및 팁을 남기고자 합니다.
- 시험은 온라인 원격 시험으로 총 120분 동안 17 문제를 풀어야 합니다. 100점 만점(100%) 중 66점(66%) 이상을 얻어야 하며 시험 등록 시 1년 이내에 2번의 기회가 주어집니다. 1차 시험에 불합격해도 재시험 가능하고 자격증의 유효기간은 3년입니다.
- 시험 유형 
  - [Kubernetes Certified Administrator(CKA)](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/)는 Kubernetes 관리 및 운영에 대한 기술 능력을 검증하기 위한 시험으로 시험유형은 다음과 같습니다. 
    - 클러스터 구성: Kubernetes 클러스터의 구성과 관련된 문제로 Kubernetes API 서버, etcd, Kubelet, Kube-proxy 등과 같은 주요 구성 요소를 물어봅니다.
    - 애플리케이션 배포: Kubernetes에서 애플리케이션을 배포하는 방법과 관련된 문제로 Pod, ReplicaSet, Deployment, Service, ConfigMap 및 Secret과 같은 Kubernetes 리소스를 사용하여 애플리케이션을 배포하는 방법에 대해 나옵니다.
    - 애플리케이션 유지 보수: Kubernetes에서 애플리케이션을 유지 보수하는 방법과 관련된 문제로 Pod 및 노드의 문제를 해결하고, 로그 및 이벤트를 분석하며, 애플리케이션 업그레이드 및 롤백과 같은 방법에 대해 나옵니다.
    - 클러스터 보안: Kubernetes 클러스터 보안과 관련된 문제로 네트워크 보안, RBAC 및 서비스 계정, TLS 인증서 및 Kubernetes 보안 기능과 클러스터 보안을 강화하는 방법에 대해 나옵니다. 
- 시험 UI
  - ![image](https://user-images.githubusercontent.com/47103479/219952534-7a483a12-f19b-46bd-a245-f787be08ea7d.png)(https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-user-interface/examui-performance-based-exams)
  - 시험 UI의 경우 왼쪽상단에 kubectl config use-context {클러스터}가 주어져 있습니다. 또한 대부분의 문제의 경우 ssh {노드}, sudo -i에 대해 설명이 주어져 있습니다.
  - 우측에는 터미널과 safari를 제공하고 있으며 시험 문제 안에서 연관된 kubernetes doc를 제공하지만 직접 search 하는 것을 추천드립니다. 또한 cheet sheet 사용도 가능 합니다.
  - 복사, 붙여넣기는 ctrl+shift+c / ctrl+shift+v이지만 잘 안되실 경우 마우스 우클릭 후에 복사, 붙여넣기를 하시면 됩니다.
  - notepad나 메모장을 사용하여 공식 문서의 코드를 복사해서 터미널에 입력하면서 풀었습니다.
- 시험 준비 
  - 시험공부는 udemy에서 [Mumshad Mannambeth의 Certified Kubernetes Administrator (CKA) with Practice Tests](https://www.udemy.com/course/certified-kubernetes-administrator-with-practice-tests/)를 보면서 공부를 진행하였습니다. 쿠버네티스의 전반적인 내용에 대해 세세하게 배울 수 있었고 수강 시 [CodeCloud](https://kodekloud.com/) 에서 실습환경도 주어집니다. 강의 마지막 부분에 Lightning Labs와 Mock Exams을 푸실정도면 시험에 합격하실 수 있을 것입니다.
  - Mumshad Mannambeth의 Certified Kubernetes Administrator (CKA) with Practice Tests의 [강의 내용 정리](https://github.com/mjs1995/Certified-Kubernetes-Administrator/tree/main/docs)는 해당 링크에서 확인할 수 있습니다.
  - Mumshad Mannambeth의 Certified Kubernetes Administrator (CKA) with Practice Tests의 [문제 및 정답](https://github.com/mjs1995/Certified-Kubernetes-Administrator/blob/main/docs/Pr_test.md)은 해당 링크에서 확인할 수 있습니다. 
  - ![image](https://user-images.githubusercontent.com/47103479/219952720-1ab6e39c-5e23-45ad-9fdc-e915d9a5e516.png)(https://killer.sh/ckad)
  - CKA 시험을 등록하면 [killer.sh](https://killer.sh/) 시뮬레이터 2회 이용권을 부여받습니다. 문제 난이도는 매우 높으며 결과에 상관없이 CKA 시험 보기 전 시험환경에 익숙해지기 위해 풀어보실 것을 권장드립니다.
- 시험 팁  
  - 시험에 자주 나오는 문제 유형 및 공식 문서 링크입니다. 
    - [클러스터 업그레이드](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/#determine-which-version-to-upgrade-to)
    - [클러스터 백업](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#volume-snapshot)
    - [사이드카](https://kubernetes.io/docs/concepts/cluster-administration/logging/#streaming-sidecar-container)
    - [노드포트](https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service)
    - [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/#the-ingress-resource)
    - [Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/#networkpolicy-resource)
    - [PV,PVC](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volumes)
    - [HostPath](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath)
    - [Role](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#kubectl-create-role)
    - [Rolling Update](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#updating-resources)
    - [Sort](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#viewing-and-finding-resources)
- 시험 결과 
  - 시험 결과는 등록된 메일로 24시간 이내에 발송됩니다. 
