- ![image](https://github.com/mjs1995/Certified-Kubernetes-Administrator/assets/47103479/5be3e9f1-2d3d-428b-b4b7-87e81651711b)
- 쿠버네티스로 실무를 할 수 있을 거 같아서 미리 연초에 CKA를 준비하였고 쿠버네티스 관련된 책을 읽으면서 기본적인 지식은 있었습니다.
- 현재 내부사정으로 쿠버네티스 실무를 하고 있지는 않지만 gke 상에서 쿠버네티스를 활용해서 데이터 파이프라인 환경을 구성하면서 CKAD를 병행하면서 개념을 다시 잡으면 좋을 거 같아 시험을 보게 되었습니다. 11월 말에 사이버먼데이를 활용해 시험 50% 할인을 받았습니다.
- CKAD 시험과 관련된 후기를 남기고자 합니다.

# 시험 준비
- 시험 준비 기간은 3주 정도 소요되었으며 쿠버네티스 실무 경험은 없지만 CKA 자격증이 있었고 쿠버네티스 관련된 서적을 읽어서 기본적인 지식이 있는 상태였습니다. 또한 쿠버네티스 기반 사이드 프로젝트를 하고 있어서 시험을 준비하는데 많은 시간은 소요되지 않았습니다.
- 이번에도 시험은 udemy에서 Mumshad Mannambeth의 [Certified Application Developer (CKAD) with Tests](https://www.udemy.com/course/certified-kubernetes-application-developer/)를 보면서 진행하였습니다. 
- 개념에 대한 부분은 정리가 되어있어서 해당 강의의 Practice Test 실습 부분만 진행하였습니다.
- 시험환경에 대해서 어떻게 나올지에 대해서 알고 있어 killer.sh도 패스하고 github [CKAD Exercises](https://github.com/dgkanatsios/CKAD-exercises?tab=readme-ov-file)와 [ckad-crash-course](https://github.com/bmuschko/ckad-crash-course) 한 번씩 풀어보고 시험을 봤습니다.

# 시험 유형 
- 시험은 총 120분 동안 16문제를 풀면 되고 시험 합격 커트는 66점입니다. 
- [시험 커리큘럼](https://www.cncf.io/training/certification/ckad/)은 아래와 같습니다.
- ![image](https://github.com/mjs1995/Certified-Kubernetes-Administrator/assets/47103479/fb175c9b-fb7b-4c61-aa88-a861a407f441)

# 시험 팁 
- ![image](https://github.com/mjs1995/Certified-Kubernetes-Administrator/assets/47103479/878e7f3b-41d1-40a6-9359-91f4583c4161)
- 올해 초 CKA시험과 다르게 휴식 요청이 가능하며 자유롭게 사용이 가능한 거 같습니다. 저는 중간중간 머리가 안 돌아가거나 스트레칭을 하고 싶을 때 위에 휴식요청을 누르고 1분 정도 쉬고 다시 보았던 거 같습니다.(한 4번은 쉬었던 거 같습니다.)
- 메모장과 계산기 사용이 가능하였지만 시험이 시작되면 txt 폴더를 하나 만들어서 거기를 많이 활용하였던 거 같습니다.
- 왼쪽에 Quick Reference 부분을 보면 Cluster에 대한 정보가 있어서 잘 전환되었는지 확인했고 Documentation 링크도 바로 줘서 확인할 수 있었습니다.
- kubectl -> k처럼 이제는 단축기에 대한 따로 설정을 안 해도 되어있습니다.
- 보통 kubectl edit deployments를 하긴 했지만 ckad의 경우 manifest 파일을 제공해주고 있어서 cp 1번_deployment.yaml 1번 deployment_백업. yaml로 백업본을 저장해 두고 풀었습니다.
- 시험을 준비하면서 참고한 공식 문서 링크입니다.
  - [CronJob](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/#example)
  - [jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/#running-an-example-job)
  - [Resource Management](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#example-1)
  - [Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#creating-a-deployment)
  - [Cheat Sheet - Updating resources](https://kubernetes.io/docs/reference/kubectl/quick-reference/#updating-resources)
  - [Security Context](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-the-security-context-for-a-pod)
  - [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/#using-configmaps)
  - [Secrets](https://kubernetes.io/docs/concepts/configuration/secret/#restriction-secret-must-exist)
  - [Liveness, Readiness](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-a-liveness-http-request)
  - [Deployments - Max Surge](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#max-surge)
  - [PersistentVolume](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolume)
  - [Resource Quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/#resource-quota-per-priorityclass)
 - 시험 결과는 등록된 메일로 24시간 이내에 발송되며 뱃지와 같이 시험 결과에 대한 확인 링크를 줍니다.
   - ![image](https://github.com/mjs1995/Certified-Kubernetes-Administrator/assets/47103479/747007ed-3650-4829-b715-d07017b537b4)
   - ![image](https://github.com/mjs1995/Certified-Kubernetes-Administrator/assets/47103479/0867a8c8-d5d4-47f4-a3b3-010eb964c428)
