# study 
- [Day7-Rolling Updates and Rollback](#practice-test---rolling-updates-and-rollback)<br>

# Rolling Updates and Rollback
- ![image](https://user-images.githubusercontent.com/47103479/211197869-a9277a32-22ae-4269-9cbc-78446c94de02.png)
  - 배포를 처음 생성하면 롤아웃이 트리거됨. 새 롤아웃은 새 배포 버전을 생성함 -> 변경 사항을 추적하고 필요한 경우 배포의 이전 버전으로 롤백할 수 있음  
- > kubectl rollout status deployment/myapp-deployment 
- > kubectl rollout history deployment/myapp-deployment
- 배포 전략 2가지 
  - ![image](https://user-images.githubusercontent.com/47103479/211197986-ba5e76f4-1da9-49da-a139-594eb3f7f7c0.png)
  - ![image](https://user-images.githubusercontent.com/47103479/211198114-82d6d1d6-eb74-4f18-8552-2407e65e966d.png)
    - Recreate : 모든 것을 파괴하고 새 버전을 만듬 
    - Rolling Update : 한번에 모두 파괴하지 않고 이전 버전을 삭제함(기본 배포 전략) 
- > kubectl apply -f deployment-definition.yaml : .yaml 파일 수정 후 apply실행
- > kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1 : 다른 방식으로 한번에 수행 
- ![image](https://user-images.githubusercontent.com/47103479/211198195-7f2691a7-7606-4323-b3df-6865b58d6b67.png)
  - ReplicaSet을 자동으로 생성하고 복제본 수를 맞추기위해 필요한 파드 수가 생서됨.롤링 업데이트전략으로 새 복제본이 생성되면 이전 버전은 삭제됨 
  - > kubectl get replicasets
  - > kubectl rollout undo deployment/myapp-deployment : 실행 취소 명령(Rollback) 
- Commands
  - create 
    - > kubectl create –f deployment-definition.yml
  - get
    - > kubectl get deployments
  - Update
    - > kubectl apply –f deployment-definition.yml
    - > kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
  - Stauts 
    - > kubectl rollout status deployment/myapp-deployment
    - > kubectl rollout history deployment/myapp-deployment
  - Rollback
    - > kubectl rollout undo deployment/myapp-deployment

# Application Commands & Arguments
- 가상 머신과 달리 컨테이너는 운영 체제를 호스트하기 위한 것이 아니라 특정 작업을 실행하기 위한 것 
- 도커 컨테이너 실행
  - > docker run ubuntu : ubuntu 이미지의 인스턴스를 실행함 
  - > docker ps -a 
  - > docker run ubuntu [COMMAND]
  - > docker run ubuntu sleep 5 : 5초 동안 대기
  - > docker build –t ubuntu-sleeper . : 새 이미지 빌드 
  - > docker run ubuntu-sleeper
- ![image](https://user-images.githubusercontent.com/47103479/211307327-5e139115-0608-4cf0-b1e7-67b06d694983.png)
- ![image](https://user-images.githubusercontent.com/47103479/211307790-7ce9cea2-e827-4dcd-92c5-2fff44601c89.png)
  - 배열 형태로 args 속성에 추가 
  - > docker run --name ubuntu-sleeper ubuntu-sleeper
  - > docker run --name ubuntu-sleeper ubuntu-sleeper 10 
  - > kubectl create -f pod-definition.yml
- ![image](https://user-images.githubusercontent.com/47103479/211308170-e9267564-cb88-4ec1-8ad3-64930607fffc.png)
  - > docker run --name ubuntu-sleeper \ --entrypoint sleep2.0 ubuntu-sleeper 10 

# Configure Environment Variables in Applications
- ![image](https://user-images.githubusercontent.com/47103479/211313515-5a15378a-cf0a-4f70-9786-5b0c2c096937.png)

# Configuring ConfigMaps in Applications
- Configmpa은 쿠버네티스에서 키-값 쌍의 형태로 comfiguration data를 전달하는데 사용됨. 
- > kubectl get configmaps
- > kubectl describe configmaps
- Create ConfigMap
  - ![image](https://user-images.githubusercontent.com/47103479/211318380-d84a9b13-45a0-4d54-a1ee-e7d154d8a935.png)
  - Imperative
    - ![image](https://user-images.githubusercontent.com/47103479/211319168-68b4391d-b92d-49db-bb83-9b619d605201.png)
      - > kubectl create configmap \ app-config --from-literal=APP_COLOR=blue \ --from-literal=APP_MOD=prod
    - ![image](https://user-images.githubusercontent.com/47103479/211319198-ed3426c6-e5df-4eef-9d56-2d9cc4bb563e.png)
      - > kubectl create configmap \ app-config --from-file=app_config.properties
  - Declarative
    - > kubectl create –f 
    - ![image](https://user-images.githubusercontent.com/47103479/211319681-fcc18451-5419-44a8-a07a-7eff88d4180a.png)
    - > kubectl create –f config-map.yaml
- ![image](https://user-images.githubusercontent.com/47103479/211320168-d836e524-e328-4077-aa41-1d0e848d019e.png)
- ![image](https://user-images.githubusercontent.com/47103479/211320359-ba833c26-6f29-40a4-96c0-39d9aee0a6e1.png)

# Secrets
- Secret은 ConfigMap과 유사하지만 인코딩된 형식으로 저장된다는 점만 다름. 암호는 base64 형식으로 데이터를 인코딩함 
- Create screate 
  - Imperative
    - ![image](https://user-images.githubusercontent.com/47103479/211326139-a396da76-58d7-4f5b-ace8-ba9cc9f80ccf.png)
      - > kubectl create secret generic \ app-secret --from-literal=DB_Host=mysql --from-literal=DB_User=root --from-literal=DB_Password=paswrd
    - ![image](https://user-images.githubusercontent.com/47103479/211326283-72337d6f-127e-4118-8403-0dc22c3ef91a.png)
      - > kubectl create secret generic <secret-name> --from-file=<path-to-file>
  - Declarative
    - ![image](https://user-images.githubusercontent.com/47103479/211326817-99d0239e-873c-4056-8034-038dfebcdf20.png)
    - > kubectl create –f secret-data.yaml
- Encode Secrets
  - ![image](https://user-images.githubusercontent.com/47103479/211327044-e73d4807-73da-4a6d-a8fd-5919e4d31a21.png)
    - linux 호스트에서 echo-n 명령어로 실행 
    - > kubectl get secrets
    - > kubectl describe secrets
    - > kubectl get secret app-secret –o yaml
- Decode Secrets
  - ![image](https://user-images.githubusercontent.com/47103479/211327208-6c8ebfef-7df2-4429-b8f5-e6490836d0af.png)
- Inject into pod 
  - ![image](https://user-images.githubusercontent.com/47103479/211327523-aff1227a-ef57-4f61-896b-cbad5e8329d4.png)
  - > kubectl create –f pod-definition.yaml
- ![image](https://user-images.githubusercontent.com/47103479/211327581-69f07ca6-3319-4ee8-9e4a-94b2e94c3dab.png)
  - > ls /opt/app-secret-volumes
  - > cat /opt/app-secret-volumes/DB_Password
- 비밀은 암호화되지 않음. 인코딩만 되어 있으므로 누구나 파일을 조회할수 있음. 따라서 비밀 개체 정의 파일을 소스 코드 리포지토리에 체크인하지 않음
- ETCD 에 암호화되어 저장되도록 비밀에 대한 미사용 암호화를 활성화합니다. 
- 쿠버네티스에서 비밀을 처리하는 방식
  - 비밀은 해당 노드의 포드에 필요한 경우에만 노드로 전송됨
  - Kubelet은 비밀이 디스크 저장소에 기록되지 않도록 비밀을 tmpfs에 저장함
  - 비밀에 의존하는 Pod가 삭제되면 kubelet은 비밀 데이터의 로컬 복사본도 삭제함 
