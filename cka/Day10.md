Day 10: 스케줄링 고급(Affinity/Anti-Affinity, PriorityClass)

1) nodeAffinity required 실습
  - Pod spec: nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution
2) nodeAffinity preferred 실습
  - Pod spec: nodeAffinity.preferredDuringSchedulingIgnoredDuringExecution
3) podAntiAffinity required 실습
  - Pod spec: podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution
4) podAffinity preferred 실습
  - Pod spec: podAffinity.preferredDuringSchedulingIgnoredDuringExecution
5) topologyKey 변경 효과 확인
  - topologyKey: kubernetes.io/hostname
6) affinity 가중치 실습
  - preferred weight 값 변경
7) 우선순위 없는 Pod 배치 확인
  - 기본 PriorityClass 없음 확인
8) PriorityClass 생성
  - k apply -f priorityclass.yaml
9) high priority Pod 스케줄 확인
  - Pod spec: priorityClassName: high-priority
10) preemption 발생 확인
  - 높은 우선순위 Pod 생성 후 기존 Pod 축출 확인
11) preemptionPolicy=Never 실습
  - Pod spec: preemptionPolicy: Never
12) PodDisruptionBudget 생성
  - k apply -f pdb.yaml
13) PDB로 drain 제한 확인
  - k drain <node> 시 실패 확인
14) taints + tolerations 조합
  - taint 적용 후 tolerations 추가
15) topologySpreadConstraints 실습
  - Pod spec: topologySpreadConstraints 추가
16) maxSkew 조정 실습
  - maxSkew 값 변경
17) whenUnsatisfiable 효과 확인
  - DoNotSchedule vs ScheduleAnyway
18) multiple constraints 조합
  - constraints 2개 이상 추가
19) default scheduler 로그 확인(가능한 환경)
  - scheduler 로그 확인
20) schedulerName 지정(커스텀 스케줄러 있으면)
  - Pod spec: schedulerName: <name>
