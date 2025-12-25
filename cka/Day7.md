Day 7: 장애 대응 기초(kubectl describe/logs/exec 등)

1) CrashLoopBackOff 유도(잘못된 cmd)
2) kubectl describe pod로 이벤트 확인
3) kubectl logs 기본
4) kubectl logs -f 실시간
5) 이전 컨테이너 로그 확인(--previous)
6) 멀티컨테이너 로그(-c)
7) kubectl exec로 셸 접속
8) readiness 실패 유도
9) liveness 실패 유도
10) 이미지 풀 실패 유도
11) Pending 원인 확인(자원 부족)
12) kubectl get events 정렬
13) kubectl top 리소스 확인(가능한 환경)
14) kubectl describe node로 상태 확인
15) 노드 NotReady 시 증상 확인
16) DNS 문제 유도(잘못된 svc 이름)
17) 서비스 엔드포인트 확인
18) ConfigMap 오류 유도(키 누락)
19) Secret 오류 유도
20) 볼륨 마운트 오류 유도
21) kubectl rollout status로 장애 확인
22) kubectl get rs로 replica 불일치 확인
23) kubectl get pod -o wide로 노드 확인
24) kubectl get 필드셀렉터 실습
25) kubectl describe에서 QoS 확인
26) OOMKilled 유도(리소스 제한 낮게)
27) kubectl debug(지원 버전)
28) 네임스페이스 전환/컨텍스트 확인
29) kubectl explain로 스펙 확인
30) Day7 리소스 정리
