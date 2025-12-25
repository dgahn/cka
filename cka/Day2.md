Day 2(워크로드 + 롤링/롤백) 실습용 예제 30개야. 모두 kubectl로 바로 해볼 수 있는 수준으로 구성했어.

  1. Deployment 생성: nginx 1개
  2. Deployment 생성: nginx 3개 replicas
  3. Deployment에서 replica 수 5로 스케일
  4. Deployment 이미지 nginx:1.25 → nginx:1.26 롤링 업데이트
  5. --record 옵션으로 업데이트 후 rollout history 확인
  6. 롤링 업데이트 도중 kubectl rollout status로 진행 확인
  7. 잘못된 이미지로 업데이트해서 실패 유도
  8. 실패한 롤아웃 kubectl rollout undo로 롤백
  9. 특정 리비전으로 롤백
  10. Deployment에 readinessProbe 추가 후 롤링 업데이트 영향 확인
  11. Deployment에 livenessProbe 추가 후 재시작 확인
  12. Deployment에 maxUnavailable=0, maxSurge=1 롤링 전략 설정
  13. Deployment에 progressDeadlineSeconds 설정 후 타임아웃 유도
  14. Deployment에 labels 추가, kubectl get rs로 RS 매칭 확인
  15. ReplicaSet 직접 생성 (label/selector 맞춰보기)
  16. ReplicaSet replicas 변경 후 Pod 수 변하는지 확인
  17. RS selector 변경 시 어떤 일이 일어나는지 실험
  18. DaemonSet 생성 (각 노드에 1개씩 뜨는지 확인)
  19. DaemonSet에 노드 셀렉터 추가해 일부 노드만 배포
  20. Job 생성: busybox로 echo "hello"
  21. Job에 completions=3 설정
  22. Job에 parallelism=2 설정
  23. Job에 backoffLimit 설정 후 실패 유도
  24. Job 완료 후 Pod 상태 확인 (Completed)
  25. CronJob 생성: 1분마다 date 출력
  26. CronJob에 startingDeadlineSeconds 설정
  27. CronJob에 concurrencyPolicy=Forbid 설정 실험
  28. CronJob에 successfulJobsHistoryLimit=1 설정
  29. Deployment, RS, DaemonSet, Job, CronJob의 차이 요약 표 만들어보기
  30. 실습 리소스 전체 정리/삭제 스크립트 작성