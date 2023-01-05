# study
[Day5](#manual-scheduling)<br>

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
