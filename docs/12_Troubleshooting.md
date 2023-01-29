# study
- [Day21](#application-failure)<br>

# Application Failure
- Check Service Status
  - ![image](https://user-images.githubusercontent.com/47103479/215324638-57020c13-83ba-4ae1-866b-0e0d21b2d2d5.png)
  - > curl http://web-service-ip:node-port
  - > kubectl describe service web-service
- Check Pod
  - ![image](https://user-images.githubusercontent.com/47103479/215324667-322c3ff3-edf7-4b53-ade7-eed02474d237.png)
  - 실행 중 상태, 포드 상태 및 재시작 횟수 확인 
  - > kubectl get pod
  - > kubectl describe pod web
  - > kubectl logs web -f --previous

# Control Plane Failure
- Check Node Status
  - > kubectl get nodes
  - > kubectl get pods
- Check Controlplane Pods
  - > kubectl get pods -n kube-system
- Check Controlplane Services
  - > service kube-apiserver status
  - > service kube-controller-manager status
  - > service kube-scheduler status
  - > service kubelet status
  - > service kube-proxy status
- Check Service Logs
  - > kubectl logs kube-apiserver-master -n kube-system
  - > sudo journalctl -u kube-apiserver
