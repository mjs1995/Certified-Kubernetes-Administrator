# study

# Design a kubernetes cluter
- 목적
  - ![image](https://user-images.githubusercontent.com/47103479/214866985-7169b3c1-5a00-410e-a379-0936d5019ed8.png)
  - 학습 목적으로 클러스터를 배포하려는 경우
  - 개발 및 테스트 목적으로 클러스터를 배포하려는 경우 
  - 프로덕션 애플리케이션을 호스팅하려는 경우 
    - ![image](https://user-images.githubusercontent.com/47103479/214867342-c294f137-1755-4e84-8bdd-ed641c934760.png)
    - 고가용성 다중 노드 클러스터와 여러 마스터 노드를 사용하는 것이 좋습니다.
- ![image](https://user-images.githubusercontent.com/47103479/214867812-883dd4e6-f105-4a5c-b47a-3a13577cf9ba.png)
  - 온프레미스의 경우 kube admin은 매우 유용한 도구입니다.
  - Google 컨테이너 엔진이 프로비저닝 GCP의 Kubernetes 클러스터는 클릭 한 번으로 클러스터 업그레이드 기능 제공하여 매우 쉽습니다.따라서 클러스터를 매우 쉽게 유지 관리할 수 있습니다.
  - koPs는 AWS에 Kubernetes 클러스터를 배포하는 좋은 도구입니다.
  - Azure Kubernetes 서비스 또는 AKS가 Azure에서 호스팅된 Kubernetes 환경 관리에 도움이 됩니다.
- Storage
  - ![image](https://user-images.githubusercontent.com/47103479/214867964-1e113334-91a3-4639-ab8a-8d5ea2fa731d.png)
- Nodes
  - ![image](https://user-images.githubusercontent.com/47103479/214868040-74e88629-ee9a-47f7-a3ec-8d2fc7b9c292.png)
  - 가상 머신 또는 클라우드 환경에서 마스터 노드 1개와 작업자 노드 2개인 3개의 노드가 있는 클러스터를 구축할 것입니다.
  - 마스터 노드가 제어 구성요소 호스팅용으로 CD 서버 및 기타의 QAP 서버와 같습니다.마스터 노드도 노드로 간주되어 워크로드를 호스팅할 수 있습니다.
    - ![image](https://user-images.githubusercontent.com/47103479/214868725-059d9c4b-a609-4630-8554-bd32de909c60.png)
  - 작업자 노드는 워크로드를 호스팅하기 위한 것입니다.
