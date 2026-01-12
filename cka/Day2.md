Day 2(워크로드 + 롤링/롤백) 실습용 예제 30개야. 모두 kubectl로 바로 해볼 수 있는 수준으로 구성했어.

  1. Deployment 생성: nginx 1개
    - k create deployment web --image=nginx:1.25
  2. Deployment 생성: nginx 3개 replicas
    - k create deployment web3 --image=nginx:1.25 --replicas=3
  3. Deployment에서 replica 수 5로 스케일
    - k scale deploy web3 --replicas=5
  4. Deployment 이미지 nginx:1.25 → nginx:1.26 롤링 업데이트
    - k set image deploy/web3 nginx=nginx:1.26
  5. --record 옵션으로 업데이트 후 rollout history 확인
    - k rollout history deploy/web3
  6. 롤링 업데이트 도중 kubectl rollout status로 진행 확인
    - k rollout status deploy/web3
  7. 잘못된 이미지로 업데이트해서 실패 유도
    - k set image deploy/web3 nginx=nginx:badtag
  8. 실패한 롤아웃 kubectl rollout undo로 롤백
    - k rollout undo deploy/web3
  9. 특정 리비전으로 롤백
    - k rollout history deploy/web3
    - k rollout undo deploy/web3 --to-revision=2
  10. Deployment에 readinessProbe 추가 후 롤링 업데이트 영향 확인
    - k edit deploy web3
    - readinessProbe 추가 후 k rollout status deploy/web3 확인
  11. Deployment에 livenessProbe 추가 후 재시작 확인
    - k edit deploy web3
    - livenessProbe 추가 후 k get pod 확인
  12. Deployment에 maxUnavailable=0, maxSurge=1 롤링 전략 설정
    - k patch deploy web3 -p '{"spec":{"strategy":{"type":"RollingUpdate","rollingUpdate":{"maxUnavailable":0,"maxSurge":1}}}}'
  13. Deployment에 progressDeadlineSeconds 설정 후 타임아웃 유도
    - k patch deploy web3 -p '{"spec":{"progressDeadlineSeconds":10}}'
  14. Deployment에 labels 추가, kubectl get rs로 RS 매칭 확인
    - k label deploy web3 tier=frontend
    - k get rs -l tier=frontend
  15. ReplicaSet 직접 생성 (label/selector 맞춰보기)
    - k create rs web-rs --image=nginx:1.25 --replicas=2
  16. ReplicaSet replicas 변경 후 Pod 수 변하는지 확인
    - k scale rs web-rs --replicas=4
  17. RS selector 변경 시 어떤 일이 일어나는지 실험
    - k edit rs web-rs
    - selector 변경 후 기존 Pod과 매칭 끊김 확인
  18. DaemonSet 생성 (각 노드에 1개씩 뜨는지 확인)
    - k create daemonset node-agent --image=nginx:1.25
  19. DaemonSet에 노드 셀렉터 추가해 일부 노드만 배포
    - k label node <node-name> disktype=ssd
    - k patch ds node-agent -p '{"spec":{"template":{"spec":{"nodeSelector":{"disktype":"ssd"}}}}}'
  20. Job 생성: busybox로 echo "hello"
    - k create job hello --image=busybox -- /bin/sh -c 'echo hello'
  21. Job에 completions=3 설정
    - k create job hello3 --image=busybox -- /bin/sh -c 'echo hello'
    - k patch job hello3 -p '{"spec":{"completions":3}}'
  22. Job에 parallelism=2 설정
    - k patch job hello3 -p '{"spec":{"parallelism":2}}'
  23. Job에 backoffLimit 설정 후 실패 유도
    - k create job failjob --image=busybox -- /bin/sh -c 'exit 1'
    - k patch job failjob -p '{"spec":{"backoffLimit":1}}'
  24. Job 완료 후 Pod 상태 확인 (Completed)
    - k get pods -l job-name=hello3
  25. CronJob 생성: 1분마다 date 출력
    - k create cronjob cj-date --image=busybox --schedule='*/1 * * * *' -- /bin/sh -c 'date'
  26. CronJob에 startingDeadlineSeconds 설정
    - k patch cronjob cj-date -p '{"spec":{"startingDeadlineSeconds":30}}'
  27. CronJob에 concurrencyPolicy=Forbid 설정 실험
    - k patch cronjob cj-date -p '{"spec":{"concurrencyPolicy":"Forbid"}}'
  28. CronJob에 successfulJobsHistoryLimit=1 설정
    - k patch cronjob cj-date -p '{"spec":{"successfulJobsHistoryLimit":1}}'
  29. Deployment, RS, DaemonSet, Job, CronJob의 차이 요약 표 만들어보기
    - Deployment=RS 관리, DaemonSet=노드당 1개, Job=일회성, CronJob=주기 실행
  30. 실습 리소스 전체 정리/삭제 스크립트 작성
    - k delete deploy,rs,ds,job,cronjob --all

livenessProbe : 컨테이너 잘 살아 있어? -> 죽었으면 pod를 재실행
readinessProbe : 서버 잘 살아있어? -> 죽었으면 트래픽을 차단

maxUnavailable : 롤링 업데이트 중에 동시에 내려도 되는 최대 수
maxSurge : 롤링 업데이트 중에 추가로 더 띄울 수 있는 최대 수
rolling : 점진적 교체를 의미한다.
progressDeadlineSeconds : rolling으로 교체될 때 일정 시간 안에 진전이 없으면 실패 처리
startingDeadlineSeconds:

