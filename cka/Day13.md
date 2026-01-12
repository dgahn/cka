Day 13: 약점 재학습

1) 오답 1~3 재실습
  - 오답 문제 다시 풀기
2) 오답 4~6 재실습
  - 오답 문제 다시 풀기
3) 오답 7~9 재실습
  - 오답 문제 다시 풀기
4) 오답 10~12 재실습
  - 오답 문제 다시 풀기
5) 오답 13~15 재실습
  - 오답 문제 다시 풀기
6) 핵심 명령 암기 리스트 작성
  - k get/describe/logs/exec/rollout 정리
7) alias 재정비
  - alias k=kubectl 확인
8) 자주 쓰는 yaml 템플릿 작성
  - pod/deploy/svc 템플릿 저장
9) kubectl explain로 구조 복습
  - k explain deploy.spec
10) 롤아웃/롤백 반복
  - k set image, k rollout undo
11) RBAC 반복
  - role/rolebinding 생성 반복
12) PV/PVC 반복
  - pvc 생성 및 mount 반복
13) NetworkPolicy 반복
  - deny/allow 정책 반복
14) DNS 진단 반복
  - nslookup, dig 반복
15) 스케줄링 반복
  - affinity/taint 반복
16) 문제 풀이 시간 단축 연습
  - 타이머로 연습
17) 실수 방지 체크리스트 업데이트
  - 체크리스트 보완
18) 다중 네임스페이스 연습
  - ns 여러 개에서 실습
19) 템플릿 재사용 연습
  - dry-run -o yaml 활용
20) dry-run 활용 연습
  - k create deploy --dry-run=client -o yaml
21) output 옵션(-o jsonpath) 복습
  - k get pod -o jsonpath='{.items[0].metadata.name}'
22) jsonpath 자주 쓰는 것 정리
  - name/labels/containers 정리
23) kubectl label/annotate 반복
  - k label/annotate 반복
24) patch 활용 복습
  - k patch deploy ...
25) set image/scale/rollout 반복
  - k set image, k scale, k rollout status
26) troubleshooting 시나리오 재현
  - CrashLoopBackOff 재현
27) etcd 백업/복구 개념 복습
  - snapshot 절차 요약
28) 스터디 노트 압축
  - 핵심만 요약
29) mock 재도전 준비
  - 환경 초기화
30) Day13 정리
  - 다음 주 계획 기록
