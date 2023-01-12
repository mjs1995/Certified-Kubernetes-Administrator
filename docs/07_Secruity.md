# Security Primitives 
- 비밀번호 기반 인증 비활성화, 경로 액세스 비활성화, SSH 키 기반 인증만 사용할 수 있음 
- API 서버 자체에 대한 액세스 제어 
  - 누가 클러스터에 액세스 할 수 있는지?
    - Files – Username and Passwords
    - Files – Username and Tokens
    - Certificates
    - External Authentication providers - LDAP
    - Service Accounts
  - 그들이 무엇을 할 수 있는지? 
    - RBAC Authorization
    - ABAC Authorization
    - Node Authorization
    - Webhook Mode
- ![image](https://user-images.githubusercontent.com/47103479/212088719-9eb7b334-1d9c-4be3-946d-4df7053ff7b0.png)
  - 클러스터와 모든 통신은 ECTD 클러스터와 같은 다양한 구성 요소, kube-controller-manager,스케줄러,API 서버, 작업자 노드에서 실행되는 것 뿐만 아니라 Kubelet 및 kube-proxy와 같은 TLS 암호화를 사용하여 보호됨 

# Authentication
- ![image](https://user-images.githubusercontent.com/47103479/212089553-11aa1b4c-f47c-44ec-be42-86ba4c369f8e.png)
  - 쿠버네티스 클러스터에서 인증 시 쿠버네티스 클러스터는 여러 노드, 물리적 또는 가상, 함께 작동하는 다양한 구성 요소, 관리자와 같은 사용자가 있음 
  - 관리 작업을 수행하기 위해 클러스터에 액세스하는 개발자, 응용 프로그램을 테스트 하거나 배포하는 클러스터에 액세스하는 개발자, 배포된 애플리케이션에 액세스하는 최종 사용자가 있음 
  - 내부 구성 요소 간의 통신과 클러스터에 대한 관리 액세스 보안, 인증 및 권한 부여 매커니즘을 통해 클러스터를 보호하는 방법에 중점을 둠 
- 두 가지 유형의 사용자
  - 관리자와 같은 사람 개발자
  - 다른 프로세스 및 서비스 또는 애플리케이션 클러스터에 액세스해야 하는 로봇 
- ![image](https://user-images.githubusercontent.com/47103479/212090205-af363383-a114-4ae4-9104-6ebc48dada8b.png)
  - 쿠버네티스는 기본적으로 사용자 계정을 관리하지 않음. 외부 소스에 의존하며 사용자 세부 정보 또는 인증서가 있는 파일과 같이 LDAT와 같은 타사 ID서비스를 통해 사용자를 관리함 
  - > kubectl create serviceaccount sa1 
  - > kubectl list serviceaccount
- ![image](https://user-images.githubusercontent.com/47103479/212090430-78b29b7e-ca3a-4526-8675-e55820d7df71.png)
- Kube API 서버에 인증하는 다양한 인증 메커니즘 
  - Static Password File 
    - ![image](https://user-images.githubusercontent.com/47103479/212091093-71acd11a-b951-4896-b892-521568c3a72f.png)
    - ![image](https://user-images.githubusercontent.com/47103479/212091175-cf12fcf9-4ad4-4a11-aeb4-d5d161d0d2dc.png)
    - > curl -v -k http://master-node-ip:6443/api/v1/pods -u "user1:password123"
  - Static Token File
    - ![image](https://user-images.githubusercontent.com/47103479/212091501-a2ec6269-c19b-4d5b-a499-f836dd270ada.png)
    - > curl -v -k https://master k https://master-node-ip:6443/api/v1/pods ip:6443/api/v1/pods --header "Authorization: Bearer KpjCVbI7rCFAHYPkBzRb7gu1cUc4B" 
  - Certificates
  - Identity Services(LDAT, Kerberos 등) 

# Article on Setting up Basic Authentication
- 세부정보가 있는 로컬 파일 생성 /tmp/users/user-details.csv
  - ![image](https://user-images.githubusercontent.com/47103479/212092509-8ace6ebf-1b0e-47f0-b851-379ebdfb1499.png)
- kubeadm이 구성한 kube-apiserver 정적 포드를 편집하여 사용자 세부 정보를 전달
  - > /etc/kubernetes/manifests/kube-apiserver.yaml
  - ![image](https://user-images.githubusercontent.com/47103479/212092632-faef09cb-e9fd-45b4-92da-41a0db671539.png)
- basic-auth 파일을 포함하도록 kube-apiserver 시작 옵션 수정
  - ![image](https://user-images.githubusercontent.com/47103479/212092766-a67892a7-de5d-4528-95a0-68baebe756be.png)
- 사용자에게 필요한 역할 및 역할 바인딩을 만듬
  - ![image](https://user-images.githubusercontent.com/47103479/212093065-f8635079-980a-4d88-a629-a6d4fc4b9489.png)
- 사용자 자격 증명을 사용하여 kube-api 서버에 인증할
  - > curl -v -k https://localhost:6443/api/v1/pods -u "user1:password123"


