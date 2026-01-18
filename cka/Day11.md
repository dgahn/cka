Day 11: 트러블슈팅 집중

1) Pod Pending 원인 유형별(taint/요청량)
  - k describe pod로 원인 확인
2) ImagePullBackOff 해결 흐름
  - 이미지 이름/레지스트리/시기 확인
3) CrashLoopBackOff 해결 흐름
  - logs/describe 확인 후 command 수정
4) Readiness 실패 해결 흐름
  - probe 경로/포트 확인
5) Liveness 실패 해결 흐름
  - probe 설정 완화
6) DNS 실패 원인 추적
  - CoreDNS 상태 확인, nslookup 테스트
7) Service selector 불일치 해결
  - svc selector와 pod label 일치 확인
8) Endpoints 비어있을 때 원인
  - selector 오타, pod not ready 확인
9) NetworkPolicy로 통신 차단 확인
  - 정책 적용 여부 확인
10) Ingress 404 문제 확인
  - host/path 규칙 및 service/port 확인
11) Node NotReady 원인 파악
  - k describe node로 조건 확인
12) DiskPressure/MemoryPressure 확인
  - node conditions 확인
13) PVC Pending 원인 추적
  - k describe pvc
14) PV/PVC 바인딩 실패 해결
  - accessModes/storageClass/selector 확인
15) 권한 오류(Forbidden) RBAC 확인
  - k auth can-i로 확인
16) SA 토큰 마운트 문제 확인
  - automountServiceAccountToken 확인
17) ConfigMap 키 누락 문제
  - key 존재 여부 확인
18) Secret decode/키 문제
  - base64 디코드 후 확인
19) 환경변수 충돌 문제
  - env vs envFrom 우선순위 확인
20) 볼륨 마운트 경로 충돌
  - mountPath 중복 확인
