# study
- [Day15](#docker-storage)<br>
- [Day16](#persistent-volumes)<br>

# Docker Storage
- 도커 스토리지의 두 가지 개념
  - Storage Drivers
  - Volume Drivers
- File system
  - ![image](https://user-images.githubusercontent.com/47103479/212905794-bf6a4089-3a30-4520-a866-1fe23b9f0414.png)
- Layered Architecture
  - ![image](https://user-images.githubusercontent.com/47103479/212906081-8c88a7d1-6bae-401b-9d00-ad8d0a967943.png)
  - ![image](https://user-images.githubusercontent.com/47103479/212906730-0a139380-4bbe-4275-bc16-f783e182d87f.png) 
    - 최종 도커 이미지를 형성하는 docker build 명령, 빌드가 완료되면 레이어의 내용은 수정할 수 없음. 읽기 전용. 
    - docker run 명령을 사용하여 컨테이너를 기반으로 생성함 
- Copy-on-write
  - ![image](https://user-images.githubusercontent.com/47103479/212907081-f3e639bf-9f77-4c7a-b71b-eef555e20fc6.png)
  - docker build 명령을 사용하여 이미지를 다시 빌드할 때까지 이미지는 항상 동일하게 유지됨 
- Volumes
  - ![image](https://user-images.githubusercontent.com/47103479/212907297-5d3b8eca-0ffa-4e3c-af47-6d68f8c6c7e0.png)
    - > docker volume create data_volume
    - > ls -l /var/lib/docker/volumes/
    - > docker volume ls  
    - > docker run -v data_volume:/var/lib/mysql mysql
    - > docker run -v data_volume2:/var/lib/mysql mysql
    - > docker run -v /data/mysql:/var/lib/mysql mysql : -v 사용은 예전 스타일
    - > docker run --mount type=bind,source=/data/mysql,target=/var/lib/mysql mysql : --mount가 선호되는 방법.
  - 도커는 Storage drivers를 사용하여 계층화된 아키텍처를 활성화함
    - AUFS
    - ZFS
    - BTRFS
    - Device Mapper
    - Overlay
    - Overlay2
- ![image](https://user-images.githubusercontent.com/47103479/212908286-b4d7062d-d25d-47fe-a168-5f184fdd1b2d.png)
  - 볼륨은 스토리지 드라이버에 의해 처리되지 않고 볼륨 드라이버 플러그인에 처리됨(기본은 Local) 
  - > docker run -it --name mysql --volume-driver rexray/ebs --mount src=ebs-vol,target=/var/lib/mysql mysql

# Container Storage Interface
- ![image](https://user-images.githubusercontent.com/47103479/212908706-bad45ab8-a00c-401c-b2f6-9a459a9b0215.png)
  - CRI : 컨테이너 런타임 인터페이스 
  - CNI : 컨테이너 네트워킹 인터페이스
  - CSI : 컨테이너 솔루션 인터페이스 
    - RPC, CreateVolume, DeleteVolume, ControllerPublishVolume

# Volumes
- ![image](https://user-images.githubusercontent.com/47103479/212909879-0e252543-5c11-4a95-a228-cd8202eca0dd.png)
  - 컨테이너에서 처리한 데이터를 유지하려면 컨테이너가 생성될 때 컨테이너에 볼륨을 연결합니다.컨테이너에서 처리한 데이터가 배치되고 볼륨에서 영구적으로 유지됨. 컨테이너가 삭제되더라도 생성되거나 처리된 데이터는 그대로 유지됨 
- ![image](https://user-images.githubusercontent.com/47103479/212909925-f665551e-8447-4ed6-8564-1f302da33f22.png)
  - 파드에서 생성된 데이터는 볼륨에 저장되며 파드가 삭제된 후에도 데이터는 남아있음 
  - 볼륨을 만들때 스토리지가 필요하여 다양한 방식으로 스토리지를 구성하도록 선택할 수 있음 
  - 볼륨이 생성되면 컨테이너에서 액세스하려면 컨테이너 내부의 디렉터리에 볼륨을 마운트합니다.이때 볼륨 마운트 필드를 사용함 
- ![image](https://user-images.githubusercontent.com/47103479/212910446-75fabe9d-774b-43c8-8b00-1542ffa17548.png)
  - 다중 노드 클러스터에서 포드가 슬래시 데이터 디렉토리를 사용하기 때문입니다. 사용을 권장하지 않음
  - Kubernetes는 여러 유형의 클러스터 스토리지 솔루션을 지원함 

# Persistent Volumes
- ![image](https://user-images.githubusercontent.com/47103479/214075755-a58f9284-fa35-43c7-acb6-15c178fb33c8.png)
  - 영구 볼륨은 관리자가 구성한 스토리지 볼룸으로 클러스터에 애플레케이션을 배포하는 사용자가 사용하는 클러스터 전체 풀
  - ![image](https://user-images.githubusercontent.com/47103479/214076070-d025fa3a-0f5d-4200-b908-ab4e503748d5.png)
  - > kubectl create –f pv-definition.yaml
  - > kubectl get persistentvolume

# Persistnet Volume Claims
- 저장소를 사용하기 위해 관리자는 영구 볼륨 세트를 생성하고 사용자가 영구 볼륨 클레임을 생성합니다.
- 영구 볼륨 클레임이 생성되면 요청 및 볼륨에 설정된 속성에 대해 Kubernetes는 영구 볼륨을 클레임 기반으로 바인딩합니다.
- ![image](https://user-images.githubusercontent.com/47103479/214076923-a510f1b5-df46-4f1e-b88d-768fc3b02b46.png)
- ![image](https://user-images.githubusercontent.com/47103479/214077757-ff675902-d142-4ac0-a930-0a062da6eb33.png)
  - > kubectl create –f pvc-definition.yaml
  - > kubectl get persistentvolumeclaim
  - > kubectl delete persistentvolumeclaim myclaim
- ![image](https://user-images.githubusercontent.com/47103479/214077882-aa67ab83-6117-40ec-b9b8-00c244d3797d.png)

# Storage Classes
- ![image](https://user-images.githubusercontent.com/47103479/214083798-ce775988-b18c-44c5-899b-18e96393480c.png)
  - Google Cloud 영구 디스크에서 PV가 생성되기 전에 Google Cloud에서 디스크를 만들었어야 합니다.
  - 볼륨의 동적 프로비저닝 : Google 스토리지와 같은 Google Cloud에서 스토리지를 자동으로 프로비저닝할 수 있는 요청이 있을 때 포드에 연결함
    - ![image](https://user-images.githubusercontent.com/47103479/214084337-afcd97a4-add3-4f80-b8c2-9326f4fa495f.png)
- storage class
  - ![image](https://user-images.githubusercontent.com/47103479/214084535-073c65bc-b229-43ae-949f-babf8d66d8b9.png)
