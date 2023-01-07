# study
[Day5](#manual-scheduling)<br>
[Day6](#node-affinity-vs-tains-and-tolerations)<br>

# Manual Scheduling
- ![image](https://user-images.githubusercontent.com/47103479/210774607-a4c5ef7f-bba5-43cc-969f-e609131549bb.png)
  - nodeName은 일반적으로 설정되어 있지 않음
  - 스케줄러는 모든 파드를 통과하여 속성이 설정되지 않은 항목을 찾음(스케줄링 대상자). 파드에 적합한 노드를 식별한 뒤에 스케줄링 알고리즘을 실행하여 파드를 예약함(바인딩 개체를 생성하여 노드 이름 속성을 노드 이름으로 설정) 
- ![image](https://user-images.githubusercontent.com/47103479/210774651-2fdca2eb-0124-41cc-8f4c-ea2d343e845d.png)
  - 스케줄러 없이 파드를 예약하는 가장 쉬운 방법은 단순히 노드 이름 필드를 노드 이름으로 설정하는 것 
  - ![image](https://user-images.githubusercontent.com/47103479/210774762-a177cbb7-0740-42ff-8ac7-77a897a371d6.png)
    - 기존 파드에 노드를 할당하는 다른 방법은 바인딩 개체를 만들고 POST 요청을 보내는 것. 바인딩 개체에서 노드 이름으로 타겟 노드를 설정함  
      - > curl --header "Content-Type:application/json" --request POST --data http://$SERVER/api/v1/namespaces/default/pods/$PODNAME/binding/

# Labels & Selectors 
- Labels과 Selectors는 함께 그룹화하는 표준 방법 
- ![image](https://user-images.githubusercontent.com/47103479/210777841-f1a73315-fab4-499b-9e0e-6dec84ef2a05.png)
  - Labels은 각 항목에 첨부된 속성, Selecotrs는 필터링 하는데 도움이됨 
- ![image](https://user-images.githubusercontent.com/47103479/210777831-3ac3d578-8cd8-498e-915f-945d9de96b75.png)
- > kubectl get pods --selector app=App1 : 레이블이 있는 파드 선택 
- ![image](https://user-images.githubusercontent.com/47103479/210778699-0437f8d3-646f-419c-9235-c220c6939b3b.png)
  - 상단은 replica 자체의 레이블, 하단의 template는 파드에 구성된 레이블 
  - 서비스 정의 파일에서 파드에 설정된 레이블과 일치하도록 selector 선택함. 

# Taints And Tolerations 
- 버그(파드)가 사람에 착륙할 수 있는 경우 사람(노드)에 대한 오염(Taint)과 특정 오염에 대한 버그의 허용 수준(Tolerations)으로 비유함 
- ![image](https://user-images.githubusercontent.com/47103479/210787919-102ae037-a5e0-487e-a3d4-1a0ae5570702.png)
  - Taint의 경우 허용 오차가 없음(달리 명시되지 않는 한 어떤 파드도 배치할 수 없음) 
  - 스케줄러로 순차적으로 배치되고 명시된 파드만 Taint에 배치할수있음 
- > kubectl taint nodes <node-name> key=value:taint-effect
  - ![image](https://user-images.githubusercontent.com/47103479/210797029-a172be15-3cde-4a58-88e6-75b5239d34c1.png)
  - > kubectl taint nodes node1 app=blue:NoSchedule : NoSchedule / PreferNoSchedule / NoExecute
  - tolerations 안에는 이중 코드로 인코딩 되어야함 
- Taint-NoExecute 
  - Taints And Tolerations는 파드의 특정 노드로 이동하도록 지시하지 않고 특정 허용 오차가 있는 파드만 허용하는걸 노드에 알려줌 
- > kubectl describe node kubemaster | grep Taint

# Node Selectors
- 특정 노드에서만 실행되도록 포드에 제한을 설정할 수 있음 
  - ![image](https://user-images.githubusercontent.com/47103479/210802827-3242d3a0-97a4-4431-ae57-b5d827fd1004.png)
    - 가장 간단한 방법은 Node Selectors를 사용함
  - kubectl label nodes <node-name> <label-key>=<label-value> : 노드에 레이블 지정 
    - kubectl label nodes node-1 size=Large
- 한계
  - 단일 레이블과 selector를 사용함 

# Node Affinity
- 주요 목적은 파드가 특정 노드에서 호스팅되는지 확인하는 것. 특정 노드에서 파드 배치를 제한함 
- ![image](https://user-images.githubusercontent.com/47103479/210804297-c5255913-bf95-4d65-ae70-cd9afacc3810.png)
- ![image](https://user-images.githubusercontent.com/47103479/210804624-32b91b59-643d-4896-8a81-e3decea85632.png)
- ![image](https://user-images.githubusercontent.com/47103479/210804653-56e9dffa-aaca-42e2-aa7d-8d6b7199bae9.png)
- 노드 선호 타입
  - ![image](https://user-images.githubusercontent.com/47103479/210806143-1ae5b7f2-7fef-406c-83dc-d13c5251f17a.png)
    - 스케줄러는 파드가 노드에 배치되도록 요구됨 
    - 사용 가능한 값이 무시됨으로 설정되어 파드가 계속 실행됨. 노드 선호도의 변경 사항이 예약되면 영향을 미치지 않음 
    - 실행단계에서 차이 존재. Required라는 옵션이 도입되면서 선호 규칙을 충족하지 않는 노드에서 실행중인 모든 파드를 제거함 

# Node Affinity vs Tains and Tolerations
- ![image](https://user-images.githubusercontent.com/47103479/211035775-cc99cfbe-bc1d-4a17-bc76-8e5228580eba.png)  
  - 색에 맞춰 배치하고싶음. 먼저 taint 및 tolerations 적용.(색지정)
  - 다른 노드에 배치될수있음 
- ![image](https://user-images.githubusercontent.com/47103479/211035969-ce24c575-a06d-43f2-8926-41cc7df0b77b.png)
  - 선호도는 각각의 색상으로 노드에 레이블을 지정하고 selector를 선택함 
  - 다른 파드 중 하나가 다른 노드에서 끝날 수 있음 
- 다른 파드가 노드에 배치되지 않도록 방지하기 위해 먼저 taint 및 tolerations 적용하고 Node Affinity를 사용하여 노드에 배치되지 않도록 파드를 방지함 

# RESOURCE LIMITS
- 사용 가능한 리소스가 충분하지 않은 경우 쿠버네티스는 파드 예약을 보류함 
- 컨테이너 리소스 요청 : 기본적으로 쿠버네티스 파드 또는 컨테이너는 파드 내에 0.5CPU와 256Mi가 필요함
- ![image](https://user-images.githubusercontent.com/47103479/211132870-e79ba31e-d740-42ca-adb0-ea4155005afc.png)
- 1CPU - 1 AWS vCPU , 1 GCP Core, 1 Azure Core, 1 Hyperthread 
- 기본적으로 쿠버네티스는 1vCPU와 512 Mi로 제한 
  - ![image](https://user-images.githubusercontent.com/47103479/211133000-107aacea-b8b8-47b7-9284-130a1dba93c9.png)
  - 설정으로 한도 제한을 할 수 있음. 이 제한을 초과하면 파드가 종료됨 
- 파드 및 배포 편집
  - > kubectl edit pod <pod name> - 파일의 복사본이 임시 위치에 저장됨
  - > kubectl delete pod webapp - 기존 파일 삭제
  - > kubectl create -f /tmp/kubectl-edit-ccvrq.yaml - 임시 파일을 사용하여 새 파드 생성 
  - > kubectl get pod webapp -o yaml > my-new-pod.yaml - YAML 형식 파드 추출
  - > vi my-new-pod.yaml - 파일 변경
  - > kubectl delete pod webapp - 기존 파드 삭제
  - > kubectl create -f my-new-pod.yaml 새 파드 생성 
  - > kubectl edit deployment my-deployment - 배포 편집 

# Daemon Sets
- ![image](https://user-images.githubusercontent.com/47103479/211133721-3fd1705f-0936-4bdb-acc7-0a5906503f1d.png)
  - ReplicasSet으로 여러 장의 사본을 만들었음. 데몬셋도 레플리카셋과 비슷하며 파드의 여러 인스턴스를 배포하는데 도움이 됨
  - 클러스터 각 노드에서 파드의 복사본 하나를 실행함, 클러스터에 새 노드가 추가될 때마다 파드의 복제본이 해당 노드에 자동으로 추가 됨. 노드가 제거되면 파드도 자동으로 제거됨 
  - 클러스터의 데몬셋으로 kube-proxy 구성 요소를 배포할 수 있음
  - 클러스터 각 노드에서 vivenet과 같은 네트워킹 솔루션 에이전트를 배포할 수 있음 
- ![image](https://user-images.githubusercontent.com/47103479/211133802-548da639-e0e2-4ae2-8274-03786854995e.png)
  - > kubectl create –f daemon-set-definition.yaml
  - > kubectl get daemonsets
  - > kubectl describe daemonsets monitoring-daemon
- v.1.12부터 데몬셋은 노드 선호도 규칙으로 기본 스케줄러를 사용하여 노드에서 파드를 예약함 

# Static PODs
- ![image](https://user-images.githubusercontent.com/47103479/211139023-92838181-a3f9-4a82-91a2-bea14460df2e.png)
  - API 서버 또는 나머지의 개입 없이 kubelet이 자체적으로 생성한 파드는 쿠버네티스 클러스터 구성 요소 중 정적 파드라고 함 
  - ![image](https://user-images.githubusercontent.com/47103479/211139106-6018a81a-7578-4b09-8e5a-03cf0b01762f.png)
- > docker ps 
  - 쿠버네티스 클러스터가 아직 없기 때문에 도커 명령어로 실행하여 볼 수 있음 
- ![image](https://user-images.githubusercontent.com/47103479/211139354-24359851-f5ef-49d9-af58-b639bf4a38b8.png)
  - 바이너리를 다운로드 할 필요가 없고 서비스를 구성하거나 서비스 충돌에 대해 걱정할 필요가 없음. 서비스 중 하나라도 중단되면 정적 포드이므로 다시 시작하면됨 
- 데몬세트와의 차이
  - ![image](https://user-images.githubusercontent.com/47103479/211139362-f228bae5-2755-4428-8bda-4d34b995f98f.png)
  - 데몬세트 - kube api 서버를 통해 데몬 세트 컨트롤러에 의해 클러스터의 모든 노드에서 사용할 수 있음. 응용프로그램이 한 인스턴스를 보장하는데 사용됨   
  - 정적 파드 - kueb API 서버의 간섭없이 kubelet에서 직접 생성. 나머지 쿠버네티스 컨트롤 플레인 구성 요소. 
