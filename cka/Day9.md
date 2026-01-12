Day 9: 업그레이드/백업(kubeadm, etcd)

1) kubeadm 버전 확인
  - kubeadm version
2) kubeadm upgrade plan 흐름 파악
  - sudo kubeadm upgrade plan
3) control-plane 업그레이드 시 순서 정리
  - kubeadm upgrade apply -> kubelet/ctl 업그레이드
4) kubelet 버전 확인
  - kubelet --version
5) kubectl get componentstatuses(구버전)
  - k get componentstatuses
6) etcd 멤버 확인
  - ETCDCTL_API=3 etcdctl member list --endpoints=<ep>
7) etcd snapshot 저장 경로 확인
  - /var/lib/etcd 확인
8) etcd snapshot 생성 명령 정리
  - ETCDCTL_API=3 etcdctl snapshot save /tmp/etcd.db --endpoints=<ep> --cacert=<ca> --cert=<cert> --key=<key>
9) snapshot 파일 크기/존재 확인
  - ls -lh /tmp/etcd.db
10) snapshot 목록 확인
  - ETCDCTL_API=3 etcdctl snapshot status /tmp/etcd.db
11) restore 절차 단계 정리
  - etcdctl snapshot restore ... -> data-dir 변경 -> manifest 수정
12) 데이터 디렉터리 권한 확인
  - ls -ld /var/lib/etcd
13) static pod manifest 위치 확인
  - ls /etc/kubernetes/manifests
14) kube-apiserver manifest 확인
  - cat /etc/kubernetes/manifests/kube-apiserver.yaml
15) etcd 인증서 경로 확인
  - /etc/kubernetes/pki/etcd/*
16) backup/restore 시점 고려
  - 컨트롤플레인 정지 후 스냅샷
17) 노드 업그레이드 순서 정리
  - control-plane 먼저, worker 다음
18) drain → upgrade → uncordon 시퀀스
  - k drain <node> --ignore-daemonsets
  - 업그레이드 후 k uncordon <node>
19) addon/CNI 업그레이드 영향 체크
  - CNI 호환 버전 확인
20) cluster-info 덤프 확인
  - k cluster-info dump > /tmp/cluster-dump.txt
21) kubeadm config view 확인
  - kubeadm config view
22) API server readiness 확인
  - k get --raw /readyz
23) upgrade 실패 시 rollback 전략 정리
  - 스냅샷 복구 플로우 확인
24) etcd snapshot 무결성 체크
  - etcdctl snapshot status /tmp/etcd.db
25) snapshot 복구 후 클러스터 확인 항목
  - k get nodes/pods 확인
26) 클러스터 다운타임 최소화 전략
  - 노드 롤링 업그레이드
27) 패치 업그레이드 vs 마이너 차이
  - 패치=호환, 마이너=호환성 점검 필요
28) kubeadm token 관련 확인
  - kubeadm token list
29) 업그레이드 문서 요약 작성
  - kubeadm upgrade 문서 핵심 정리
30) Day9 정리 체크리스트 만들기
  - 사전 체크/백업/복구 항목 정리
