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
