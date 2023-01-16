# study
- [Day11](#security-primitives)<br>
- [Day12](#tls-in-kubernetes)<br>

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

# TLS Certificates
- Symmetric Encryption
  -  ![image](https://user-images.githubusercontent.com/47103479/212463495-4bf0ab2d-615e-4f96-9aa3-19f83c2582e4.png)
  - 안전한 암호화 방식 
  - 단일 키를 사용하여 데이터를 암호화하고 해독하는 대신 비대칭 암호화는 한 쌍의 키를 사용함 
    - Private key, Public Lock
  - 트릭은 데이터를 암호화거나 자물쇠로 잠그는 경우로 관련 키로만 열 수 있음 
- ![image](https://user-images.githubusercontent.com/47103479/212463742-e0e33cfb-4644-475c-8c87-237054970d86.png) 
  - > ssh-keygen : id_rsa(Private key), id_rsa.pub(Public lock) 생성 
  - > cat ~/.ssh/authorized_keys 
  - > ssh -i id_rsa_user@server1
  - > openssl genrsa -out my-bank.key 1024 : 개인 키와 공개 키 쌍을 생성함 
  - > openssl rsa -in my-bank.key -pubout > mybank.pem 
- > openssl req -new -key my-bank.key -out my-bank.csr -subj "/c=US/ST=CA/O=MyOrg.Inc./CN=my-bank.com"
- 네트워크를 통해 전송되고 있는 메시지를 암호화하려는 이유 
  - 메시지를 암호화하기 위해 한 쌍의 공개 키와 개인 키로 비대칭 암호화를 사용함 
  - 관리자는 한 쌍의 키를 사용하여 서버에 대한 SSH 연결을 보호함 
  - 서버는 한 쌍의 키를 사용하여 STPS 트래픽을 보호함 
    - 서버는 CA에 대한 인증서 서명 요청, 개인 키를 사용하여 CSR에 서명함(모든 사용자는 CA의 공개 키 사본을 가지고 있음) 
    - 서명 된 인증서가 서버로 다시 전송되고 서버는 서명된 인증서와 함께 웹 애플리케이션을 구성함  
  - 대칭 키는 서버의 공개키를 사용하여 암호화되고 다시 서버에 보내짐. 서버는 개인 키를 사용하여 메시지를 해독함  
- ![image](https://user-images.githubusercontent.com/47103479/212464243-87d5feb9-902c-403c-84ae-1a8eb4304d31.png)
- ![image](https://user-images.githubusercontent.com/47103479/212464220-2852c0d6-95f9-4e06-b29a-eeff28e9895e.png)

# TLS in Kubernetes
- 서비스 인증서 : 서버가 공개 및 개인 키를 사용하여 연결을 보호하는 방법 
- ![image](https://user-images.githubusercontent.com/47103479/212471366-40ab88cc-f6c6-4b59-8b70-3b328a5a0455.png)
  - 세 가지 유형의 인증서
    - 서버에 구성된 서버 인증서
    - CA 서버에 구성된 루트 인증서 
    - 클라이언트에 구성된 클라이언트 인증서 
  - 개인 키는 일반적으로 extension.key와 같이 있음. 파일 이름에 -키가 있음. server.key 또는 server-key.epm 
- ![image](https://user-images.githubusercontent.com/47103479/212471375-0f54963f-1016-44a5-9ac4-e95903d60b72.png)
  - 쿠버네티스 클러스터는 마스터 및 작업자 노드 세트로 구성됨 
  - 노드 간의 모든 통신은 보안이 필요하고 암호화되어야 함 
  - kubectl 유틸리티를 통한 Kubernetes 클러스터 또는 Kubernetes API에 직접 액세스하는 동안 보안 TLS 연결을 설정해야함 
  - 클러스터 내에서 모든 다양한 서비스를 갖기 위해 두 가지 주요 요구 사항 
    - 그들이 말하는 사람인지 확인하기 위해 서버 인증서 사용 및 모든 클라이언트가 클라이언트 인증서를 사용
- Server Certificates for Servers
  - ![image](https://user-images.githubusercontent.com/47103479/212471442-065b2b51-81a8-4dd6-a4aa-d0e78722c9c8.png)
  - etcd 서버는 클러스터에 대한 모든 정보를 저장함. 따라서 한 쌍의 인증서와 키가 필요함
  - 작업자 노드에 있는 kubelet 서비스는 HTTPS API 끝점을 노출함 
- Client Certificates for Clients
  - ![image](https://user-images.githubusercontent.com/47103479/212471591-7781a741-6ed9-42d2-b8f4-d73837cec222.png)
  - kube-apiserver에 접속하는 클라이언트는 우리로 kubectl Arrest API를 통해 관리자
  - 관리 사용자는 kube-API 서버에 인증하기 위한 키 쌍인 admin.crt 및 admin.key라고 하는 인증서가 필요함 
- ![image](https://user-images.githubusercontent.com/47103479/212471642-1f2a70a3-5c27-4d30-88d3-e8cb0d6e0be7.png)
- ![image](https://user-images.githubusercontent.com/47103479/212471630-c44b2dd5-f060-4dc2-bacd-00e76e00259e.png)

# TLS in Kubernetes - Certificate Creation
- 인증서를 생성하려면 Easy-RSA, OPENSSL, CFSSL와 같은 다양한 도구를 사용할 수 있음 
- OPENSSL
  - 개인 키 생성
    - ![image](https://user-images.githubusercontent.com/47103479/212471738-bfa70d31-175d-4d82-8f2e-6dc54b517921.png)
      - > openssl genrsa -out ca.key 2048 : Generate Keys
      - > openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr : Generate CSR
      - > openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt : Sign certificates
  - 클라이언트 인증서 생성 
    - ![image](https://user-images.githubusercontent.com/47103479/212471875-2bde0949-580f-4797-9caa-7ffd48624f12.png)
      - > openssl genrsa -out admin.key 2048
      - > openssl req -new -key admin.key -subj "/CN=kube-admin" -out admin.csr
      - > openssl x509 -req -in admin.csr -CA ca.crt -CAkey ca.key -out admin.crt
  - 생성 된 인증서를 통해서 관리자 인증서를 가져와서 클러스터를 관리할 수 있음 
    - ![image](https://user-images.githubusercontent.com/47103479/212472032-55e1b6a0-2939-43e2-8907-3fdc289b82b3.png)
    - > curl https://kube-apiserver:6443/api/v1/pods \ --key admin.key --cert admin.crt \ --cacert ca.crt
- Generating Server Certificates
  - ETCD Server certificate
    - ![image](https://user-images.githubusercontent.com/47103479/212472123-3d80ba86-db49-42e5-a864-23a2412a0acd.png)
    - ![image](https://user-images.githubusercontent.com/47103479/212472115-54e849f2-6310-417f-b650-48b75df6c94a.png)
  - KUBE API SERVER
    - ![image](https://user-images.githubusercontent.com/47103479/212472240-68ed13f8-cddb-4295-a0d1-fefe98f2a9be.png)
    - > openssl genrsa -out apiserver.key 2048
    - > openssl req -new -key apiserrver.key -subj \ "/CN=kube-apiserver" -out apiserver.csr
    - > openssl req -new -key apiserver.key -subj \ "/CN=kube-apiserver" -out apiserver.csr –config openssl.cnf
    - > openssl x509 -req -in apiserver.csr \ -CA ca.crt -CAkey ca.key -out apiserver.crt
    - ![image](https://user-images.githubusercontent.com/47103479/212472269-d5ed205a-1a2f-4585-acd7-a3a3e33c591f.png)
  - KUBECTL NODES (SERVER CERT)
    - kubelets 서버는 각 노드에서 실행되는 노드 관리를 담당하는 ACTPS API 서버입니다.
    - ![image](https://user-images.githubusercontent.com/47103479/212472321-6dd0eea0-c772-4913-b30c-c2ef6ff99218.png)
  
# View Certificate Details
- ![image](https://user-images.githubusercontent.com/47103479/212474150-73db94f2-f193-46bc-ad07-3fa6c9dcb148.png)
  - kubeadm에 의한 클러스터 프로비저닝에서 건강검진을 하기 위해서는 모든 인증서를 식별하여야 함 
  - ![image](https://user-images.githubusercontent.com/47103479/212474211-0a559016-3db7-479f-bedf-b33454de73f2.png)
  - > cat /etc/kubernetes/manifests/kube-apiserver.yaml
    - ![image](https://user-images.githubusercontent.com/47103479/212474261-5fb0cfd3-8982-419f-a533-0aaec0d958e6.png)
  - > openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
    - ![image](https://user-images.githubusercontent.com/47103479/212474278-bb31e767-eb9f-4ec6-8d96-61c34311b629.png)
  - ![image](https://user-images.githubusercontent.com/47103479/212474319-e8a3a256-1201-4144-991f-10f48604d1ff.png)
  - ![image](https://user-images.githubusercontent.com/47103479/212474340-68328e6c-ca89-45e4-812d-ef32987d8a01.png)
- > journalctl -u etcd.service -l
  - ![image](https://user-images.githubusercontent.com/47103479/212474356-f1b211b2-188e-4c79-9b7d-4af4f6dc7fff.png)
- > kubectl logs etcd-master
  - ![image](https://user-images.githubusercontent.com/47103479/212474387-80464bc2-eb74-4671-97da-5687ddb263d2.png)
- > docker ps -a
  - ![image](https://user-images.githubusercontent.com/47103479/212474400-37232e8e-8017-42d7-8073-38488cc391ac.png)
  - > docker logs 87fc
    - ![image](https://user-images.githubusercontent.com/47103479/212474422-02731c80-1a4b-4055-980d-774f16013661.png)

# Certificates API
- ![image](https://user-images.githubusercontent.com/47103479/212541766-afd3c6b4-3610-445b-8f16-6e56371b7ebd.png)
  - 사용자가 증가하고 팀이 성장함에 따라 인증서를 관리하는 자동화 방법 필요
  - API 호출을 통해 쿠버네티스에 직접 서명 요청. 쿠버네티스 API 객체 생성. 
  - > openssl genrsa -out jane.key 2048 : 사용자 키 생성 
  - > openssl req -new -key jane.key -subj "/CN=jane" -out jane.csr : 관리자에게 요청을 보냄 
  - ![image](https://user-images.githubusercontent.com/47103479/212541844-823ab708-10dd-4158-8a6c-1810753bb7c8.png)
    - > cat jane.csr | base64 
  - > kubectl get csr : 모든 인증서 서명 요청을 볼 수 있음 
  - > kubectl certificate approve jane : 인증 승인 명령 실행
  - ![image](https://user-images.githubusercontent.com/47103479/212541980-19ec6f2d-5da1-4dab-8200-6901834402af.png)
    - > kubectl get csr jane -o yaml : 인증서 보기
    - > echo "<certificate>" |base64 --decode : 인증서 해독 
- ![image](https://user-images.githubusercontent.com/47103479/212542033-4acc1cc4-3cde-4017-9189-fbdcf6722fb2.png)  
  - > cat /etc/kubernetes/manifests/kube-controller-manager.yaml : 인증서에 서명해야 하는 경우 CA서버 경로 인증서와 개인 키가 필요함 

# Security Kubeconfig 
- kube playground
  - ![image](https://user-images.githubusercontent.com/47103479/212543709-7fa7a84f-9b3a-40e3-a6ad-a76725e021e4.png)
  - > curl https://my-kube-playground:6443/api/v1/pods \ --key admin.key --cert admin.crt --cacert ca.crt
  - > kubectl get pods --server my-kube-playground:6443 --client-key admin.key --client-certificate admin.crt --certificate-authority ca.crt
- ![image](https://user-images.githubusercontent.com/47103479/212543867-61d29b2b-182e-4eee-a0fa-29d60cdd4714.png)
  - kubeconfig라는 구성 파일에 옵션으로 저장함 
- KubeConfig File
  - ![image](https://user-images.githubusercontent.com/47103479/212544000-edad9e22-b371-4940-b7e4-a60cc92b7bbc.png)
    - ![image](https://user-images.githubusercontent.com/47103479/212544084-34870c5e-692d-4b63-a6a8-385bf20ebc09.png)
    - ![image](https://user-images.githubusercontent.com/47103479/212544101-9350ec99-0afd-4936-ab17-f19854c8fb7a.png)
  - ![image](https://user-images.githubusercontent.com/47103479/212544163-720bffaa-098b-4cb3-beac-41e273646d3d.png)
    - > kubectl config view : 현재 사용중인 파일 보기
    - > kubectl config view –kubeconfig=my-custom-config : kubeconfig 옵션을 사용하여 파일 지정할 수 있음 
  - ![image](https://user-images.githubusercontent.com/47103479/212544198-229d308d-2649-4217-83d8-bac926d55650.png)
    - > kubectl config use-context prod-user@production : 현재 컨텍스트 변경    
    - ![image](https://user-images.githubusercontent.com/47103479/212544246-4c4b8ba7-a77d-43d0-8107-ed03b0c08f16.png)  
      - > kubectl config -h
- Namespaces
  - ![image](https://user-images.githubusercontent.com/47103479/212544280-619121ac-f87b-4ce1-861f-871f45bd8d61.png)
- Certificates in KubeConfig
  - ![image](https://user-images.githubusercontent.com/47103479/212544301-2ebbb140-c7bd-4e38-b9a5-034124e4cc2b.png)
  - ![image](https://user-images.githubusercontent.com/47103479/212544426-07fe7dd0-9c39-435e-95ef-e3afa900f4e4.png)

# API Groups 
- ![image](https://user-images.githubusercontent.com/47103479/212545231-b3a5595a-e9dc-42be-be99-d622897c97ae.png)
  - 쿠버네티스 API 버전 확인 / 파드 목록 가져오기 
- ![image](https://user-images.githubusercontent.com/47103479/212545261-437798cb-c38c-4624-8513-e7a5b563fe54.png)
  - /metrics, /healthz는 클러스터의 상태를 모니터링함 
  - /logs는 타사 로깅 응용프로ㅡ램과 함께 통합에 사용됨 
  - /api 
    - ![image](https://user-images.githubusercontent.com/47103479/212545497-524c0030-f1a7-4950-8fdf-2879abac970a.png)
    - core그룹으로 모든 핵심 기능이 존재하는 곳. 
  - /apis
    - ![image](https://user-images.githubusercontent.com/47103479/212545503-0c4bc5fc-4465-49dd-96cb-f679236fd4ee.png)
    - named 그룹 API는 더 체계적임. 모든 최신 기능이 이 그룹을 통해 사용할 수 있음 
- ![image](https://user-images.githubusercontent.com/47103479/212545513-bb795c38-415a-4d5d-879f-85fbcb8afc3b.png)
  - > curl http://localhost:6443 -k : 사용가능한 API 그룹 나열
  - > curl http://localhost:6443/apis -k | grep “name” : 지원되는 모든 리소스 그룹을 반환함 
- ![image](https://user-images.githubusercontent.com/47103479/212545564-25bacede-933f-4060-b516-fd9c624c5098.png)
- kubectl proxy
  - ![image](https://user-images.githubusercontent.com/47103479/212545574-95420275-9c79-4f55-ace0-4d3ee2de82f5.png)
  - > kubectl proxy : 파드와 서비스 간 클러스터의 다른 노드와 연결을 활성화하는데 사용함 
- kubectl proxy는 kube control utility에서 만든 ACTP 프록시 서비스로 Kube API 서버에 액세스함 

# Authorization
- ![image](https://user-images.githubusercontent.com/47103479/212546566-128edb08-cbe4-48a1-9a17-2d48ccbe117c.png)
  - 클러스터 인증이 필요한 이유는 클러스터 관리자로서 모든 종류의 작업을 수행할 수 있음 
- 권한 부여 매커니즘 
  - ![image](https://user-images.githubusercontent.com/47103479/212546589-01666923-c92b-467f-bd68-db3993188bd9.png)
  - Node
    - ![image](https://user-images.githubusercontent.com/47103479/212546666-558dd825-8765-41c5-b009-7cf58a5b7a66.png)
    - 특별 권한 부여자인 노드 권한 부여자가 이러한 욫어을 처리함 
  - ABAC
    - ![image](https://user-images.githubusercontent.com/47103479/212546725-2e0ecc1e-f17b-4ab6-b38d-ef74ae378ab4.png)
  - RBAC
    - ![image](https://user-images.githubusercontent.com/47103479/212546784-1fdb6823-921c-451a-be58-2005d2b5ac5f.png)
    - 사용자를 직접 연결하는 대신 일련의 권한이 있는 그룹이 역할을 정의함 
  - Webhook
    - ![image](https://user-images.githubusercontent.com/47103479/212546838-6faa22c0-4fb9-45f6-b94e-ddb747529c05.png)
  - AlwaysAllow : 수행하지 않고 모든 요청을 허용함 
  - AlwaysDeny : 모든 요청을 거부함 
    - ![image](https://user-images.githubusercontent.com/47103479/212546909-08890eca-5e71-4925-bcd9-38b33768fc80.png)

# RBAC
- ![image](https://user-images.githubusercontent.com/47103479/212547032-c8ee87bd-ea83-44ac-a086-42e8c3a7cfeb.png) 
  - kubectl create -f developer-role.yaml  
- ![image](https://user-images.githubusercontent.com/47103479/212547120-773954f6-95c9-4bf3-b45d-259a92c8456c.png)  
  - 사용자를 해당 역할에 역할 하는 것. 이를 위해 롤 바인딩이라는 개체를 만듬. 롤 바인딩 개체는 사용자 개체를 역할에 연결함 
  - > kubectl create -f devuser-developer-binding.yaml
- > kubectl get roles : 생성된 역할 보기 
- > kubectl get rolebindings : 롤 바인딩 보기 
- > kubectl describe role developer : 자세하게 보기
- > kubectl describe rolebinding devuser-developer-binding : 큐브 컨트롤을 실행하고 롤 바인딩 명령을 설명함. 기존 롤 바인디엥 대한 세부 정보 확인할 수 있음 
- ![image](https://user-images.githubusercontent.com/47103479/212547368-f758f22d-0b9a-4b53-a305-6ec72006e5a7.png)
  - > kubectl auth can-i create deployments
  - > kubectl auth can-i delete nodes
  - > kubectl auth can-i create deployments --as dev-user
  - > kubectl auth can-i create pods --as dev-user
  - > kubectl auth can-i create pods --as dev-user --namespace test
- Resource Names
  - ![image](https://user-images.githubusercontent.com/47103479/212547425-95092408-6590-4652-a5d6-84d4a1d3d1ac.png)

# Cluster Roles 
- ![image](https://user-images.githubusercontent.com/47103479/212674295-e1a29a56-adb7-40f2-9c93-4887788f5287.png)
  - > kubectl api-resources --namespaced=true
  - > kubectl api-resources --namespaced=false
- ![image](https://user-images.githubusercontent.com/47103479/212674515-16aeb6fb-5a5c-4a57-9119-5b2307c0f5ff.png)
- clusterrolebinding
  - ![image](https://user-images.githubusercontent.com/47103479/212674675-c20f1de3-963f-4016-b7c6-4a13f6571191.png)
  - > kubectl create –f cluster-admin-role-binding.yaml

# Service Accounts
- > kubectl create serviceaccount dashboard-sa
- > kubectl get serviceaccount : 해당 서비스 계정에는 비밀 개체가 있음 
- > kubectl describe serviceaccount dashboard-sa
- > kubectl describe secret dashboard-sa-token-kbbdm
- > kubectl exec -it my-kubernetes-dashboard ls /var/run/sevrets/kubernetes.io/serviceaccount : 파드 내부의 디렉토리의 내용 나열 
  - > kubectl exec -it my-kubernetes-dashboard cat /var/run/sevrets/kubernetes.io/serviceaccount/token : 해당 파일의 내용 나열하면 사용할 토큰이 표시됨 
- > jq -R 'split(".") | select(length > 0) | .[0],.[1] | @base64d | fromjson' <<< eyJhbGcioiJ... : 토큰 디코딩(jwt.io에서 복사 붙여넣기 가능) 
- > kubectl create token dashboard-sa

# Image Security
- ![image](https://user-images.githubusercontent.com/47103479/212689193-ade978e4-e74c-4a17-9160-4758522f138a.png)
  - library는 사용자 계정 이름을 나타내는 위치인데 제공하지 않으면 library로 가정함 
  - 이미지를 가져올 위치를 지정하지 않았기 때문에 도커의 기본 레지스트리인 도커 허브로 간주됨 
- Private Repository
  - > docker login private-registry.io
  - > docker run private-registry.io/apps/internal-app
  - ![image](https://user-images.githubusercontent.com/47103479/212689911-582103c0-c429-4651-825d-eb61af3d1b23.png)
    - 이미지 이름을 개인 레지스트리에 있는 전체 경로로 바꿈 
  - > kubectl create secret docker-registry regcred \ --docker-server= private-registry.io  \ --docker-username= registry-user \ --docker-password= registry-password \ --docker-email= registry-user@org.com

# Docker Security
- > docker run ubuntu sleep 3600 
- > ps aux : 프로세스를 나열
- Docker 이미지 자체에 사용자 보안을 강화하기 위해 정의를 함 
- > docker build -t my-ubuntu-image
- > docker run my-ubuntu-image sleep 3600
- 루트 사용자 시스템에 제한 없이 액세스 할 수 있음. 
  - /usr/include/linux/capability.h
  - 파일 수정 및 파일에 대한 권한, 액세스 제어, 프로세스 생성 또는 종료, 그룹 ID 또는 사용자 ID 설정, 네트워크 관련 작업 수행, 네트워크 파트 제어 등
- > docker run --cap-drop KILL ubuntu : 권한 삭제 
- > docker run --privileged ubuntu : 모든 권한이 활성화된 상태에서 컨테이너 실행 

# Security Contexts
- > docker run --user=1001 ubuntu sleep 3600
- > docker run -cap-add MAC_ADMIN ubuntu
- Kubernetes Security
  - 컨테이너는 파드에 캡슐화됨. 보안 설정을 컨테이너 수준 또는 파드 수준에서 구성하도록 선택할 수 있음 
  - Security Context
    - ![image](https://user-images.githubusercontent.com/47103479/212695248-354363ac-ae4a-4c42-a8fc-24475dcb6762.png)
