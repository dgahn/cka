Day 7: 장애 대응 기초(kubectl describe/logs/exec 등)

1) CrashLoopBackOff 유도(잘못된 cmd)
  - k run crash --image=busybox --restart=Never -- /bin/sh -c 'exit 1'
2) kubectl describe pod로 이벤트 확인
  - k describe pod crash
3) kubectl logs 기본
  - k logs crash
4) kubectl logs -f 실시간
  - k logs -f crash
5) 이전 컨테이너 로그 확인(--previous)
  - k logs crash --previous
6) 멀티컨테이너 로그(-c)
  - k logs <pod> -c <container>
7) kubectl exec로 셸 접속
  - k exec -it <pod> -- sh
8) readiness 실패 유도
  - readinessProbe에 잘못된 path 설정
9) liveness 실패 유도
  - livenessProbe에 실패하는 명령 설정
10) 이미지 풀 실패 유도
  - image: nginx:badtag
11) Pending 원인 확인(자원 부족)
  - requests를 크게 설정 후 k describe pod
12) kubectl get events 정렬
  - k get events --sort-by=.metadata.creationTimestamp
13) kubectl top 리소스 확인(가능한 환경)
  - k top pod
14) kubectl describe node로 상태 확인
  - k describe node <node>
15) 노드 NotReady 시 증상 확인
  - k get nodes
16) DNS 문제 유도(잘못된 svc 이름)
  - nslookup bad-svc
17) 서비스 엔드포인트 확인
  - k get endpoints <svc>
18) ConfigMap 오류 유도(키 누락)
  - 존재하지 않는 key 참조
19) Secret 오류 유도
  - 존재하지 않는 secret 참조
20) 볼륨 마운트 오류 유도
  - 잘못된 hostPath 지정
21) kubectl rollout status로 장애 확인
  - k rollout status deploy/<name>
22) kubectl get rs로 replica 불일치 확인
  - k get rs
23) kubectl get pod -o wide로 노드 확인
  - k get pod -o wide
24) kubectl get 필드셀렉터 실습
  - k get pod --field-selector status.phase=Pending
25) kubectl describe에서 QoS 확인
  - k describe pod <pod>
26) OOMKilled 유도(리소스 제한 낮게)
  - limits.memory를 작게 설정
27) kubectl debug(지원 버전)
  - k debug pod/<pod> -it --image=busybox
28) 네임스페이스 전환/컨텍스트 확인
  - k config get-contexts
  - k config set-context --current --namespace=<ns>
29) kubectl explain로 스펙 확인
  - k explain pod.spec
30) Day7 리소스 정리
  - k delete pod --all
