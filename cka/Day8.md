Day 8: 클러스터 관리(노드/taint/toleration/label/selector, drain/cordon)

1) 노드 라벨 확인
2) 노드 라벨 추가/삭제
3) Pod nodeSelector로 배치
4) affinity vs nodeSelector 비교
5) taint 추가(NoSchedule)
6) toleration으로 우회 배치
7) taint 삭제
8) kubectl cordon 테스트
9) cordon 노드에 스케줄 방지 확인
10) kubectl uncordon
11) kubectl drain 기본
12) drain 시 DaemonSet 제외 확인
13) drain 시 --ignore-daemonsets
14) drain 시 --delete-emptydir-data
15) 노드 상태 NotReady 시 영향 확인
16) kubectl describe node로 allocatable 확인
17) kubectl get pods -o wide로 분산 확인
18) Pod anti-affinity로 분산
19) podAffinity로 모으기
20) 노드 셀렉터 오타로 Pending 유도
21) taint key/value/effect 조합 확인
22) tolerationSeconds 실습
23) Pod에 nodeName 고정 실습
24) static pod 존재 확인(가능한 환경)
25) kube-system 리소스 확인
26) 노드 리소스 압박 상태 확인
27) kubectl top node 확인
28) node label 기준 topologyKey 실습(가능한 경우)
29) 노드 교체 시 리스케줄 확인
30) Day8 리소스 정리
