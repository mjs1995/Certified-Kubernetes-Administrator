# Monitor Cluster Components 
- 클러스터의 노드 수와 같은 노드 수준 메트릭, CPU와 같은 성능 메트릭, 메모리, 네트워크 및 디스크 활용도, 파드 수준 및 성능 지표 등을 모니터링하고 싶음 
- 오픈 소스 솔루션으로 Metrics Server, Prometheus, Elastic Stack, Datadog, Dynatrace 
- Metrics Server
  - Metrics Server는 각 쿠버네티스 노드 및 파드에서 집계해서 메모리에 저장함. 인메모링 모니터링 솔루션 
  - cAdvisor는 kubelect API를 통해 Metrics Server에서 매트릭을 사용할 수 있도록 하고 파드에서 성능 지표 검색
  - > minikube addons enable metrics-server : 메트릭 서버 활성화(Minikube에서) 
  - > git clone https://github.com/kubernetes-incubator/metrics-server.git
  - > kubectl create –f deploy/1.8+/
  - > kubectl top node : CPU와 각 노드의 메모리 소비 조회 

# Application Logs
- > docker run kodekloud/event-simulator : event-simulator 라는 Docker 컨테이너 실행 
- > docker run -d kodekloud/event-simulator : -d 옵션으로 로그 안보이게함
- > docker logs -f ecf : -f 옵션은 라이브 로그 트레일을 보는데 도움이 됨  
- ![image](https://user-images.githubusercontent.com/47103479/211194693-8fcf7a9d-8b4d-49eb-b446-e96882234654.png)
  - > kubectl create –f event-simulator.yaml
  - > kubectl logs –f event-simulator-pod
  - > kubectl logs –f event-simulator-pod event-simulator : 파드 내 여러 컨테이너가 있는 경우 이름 지정 
