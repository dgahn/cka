Day 8: 클러스터 관리(노드/taint/toleration/label/selector, drain/cordon)

1) 노드 라벨 확인
  - k get nodes --show-labels
2) 노드 라벨 추가/삭제
  - k label node <node> disktype=ssd
  - k label node <node> disktype-
3) Pod nodeSelector로 배치
  - Pod spec: nodeSelector: {disktype: ssd}
4) affinity vs nodeSelector 비교
  - nodeAffinity 추가 후 스케줄링 비교
5) taint 추가(NoSchedule)
  - k taint node <node> key=value:NoSchedule
6) toleration으로 우회 배치
  - Pod spec: tolerations 추가
7) taint 삭제
  - k taint node <node> key=value:NoSchedule-
8) kubectl cordon 테스트
  - k cordon <node>
9) cordon 노드에 스케줄 방지 확인
  - 새로운 Pod Pending 확인
10) kubectl uncordon
  - k uncordon <node>
11) kubectl drain 기본
  - k drain <node> --ignore-daemonsets
12) drain 시 DaemonSet 제외 확인
  - DaemonSet Pod 유지 확인
13) drain 시 --ignore-daemonsets
  - k drain <node> --ignore-daemonsets
14) drain 시 --delete-emptydir-data
  - k drain <node> --ignore-daemonsets --delete-emptydir-data
15) 노드 상태 NotReady 시 영향 확인
  - k get nodes
16) kubectl describe node로 allocatable 확인
  - k describe node <node>
17) kubectl get pods -o wide로 분산 확인
  - k get pods -o wide
18) Pod anti-affinity로 분산
  - podAntiAffinity 설정
19) podAffinity로 모으기
  - podAffinity 설정
20) 노드 셀렉터 오타로 Pending 유도
  - nodeSelector 잘못된 라벨 값
