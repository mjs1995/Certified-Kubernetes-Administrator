# Pre-Requisites - JSON PATH
- https://kodekloud.com/p/json-path-quiz
- https://mmumshad.github.io/json-path-quiz/index.html#!/?questions=questionskub1
- https://mmumshad.github.io/json-path-quiz/index.html#!/?questions=questionskub2

# JSON PATH in Kubernetes
- Kubectl에서 JSONpath를 시작
  - Identify the kubectl command
    - 예를 들어 노드에 대한 정보가 필요한 경우, Kubectl get nodes 명령을 사용해야 합니다.
  - Familiarzie with JSON output
    - > kubectl get nodes -o json
    - > kubectl get pods -o json 
    - ![image](https://user-images.githubusercontent.com/47103479/215493057-8f71e3d2-236b-413d-b6cd-1570677665db.png)
  - From the JSON PATH query 
    - .items[0].spec.containers[0].image
  - Use the JSON PATH query with kubectl command
    - > kubectl get pods -o=jsonpath='{.items[0].spec.containers[0].image}'
- Examples
  - > kubectl get pods -o=jsonpath='{.items[*].metadata.name}'
  - ![image](https://user-images.githubusercontent.com/47103479/215493743-32ca2c6c-607a-4023-8f8f-622aa7069a4d.png)
  - > kubectl get pods -o=jsonpath='{.items[*].status.nodeInfo.architecture}'
  - > kubectl get pods -o=jsonpath='{.items[*].status.status.capacity.cpu}'
- > kubectl get nodes -o=custom-columns=NODE:.metadata.name ,CPU:.status.capacity.cpu
- > kubectl get nodes --sort-by=.metadata.name
- > kubectl get nodes --sort-by=..status.capacity.cpu
