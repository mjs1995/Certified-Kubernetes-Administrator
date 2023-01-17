# study

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
