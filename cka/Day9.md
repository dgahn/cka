Day 9: 업그레이드/백업(kubeadm, etcd)

1) kubeadm 버전 확인
2) kubeadm upgrade plan 흐름 파악
3) control-plane 업그레이드 시 순서 정리
4) kubelet 버전 확인
5) kubectl get componentstatuses(구버전)
6) etcd 멤버 확인
7) etcd snapshot 저장 경로 확인
8) etcd snapshot 생성 명령 정리
9) snapshot 파일 크기/존재 확인
10) snapshot 목록 확인
11) restore 절차 단계 정리
12) 데이터 디렉터리 권한 확인
13) static pod manifest 위치 확인
14) kube-apiserver manifest 확인
15) etcd 인증서 경로 확인
16) backup/restore 시점 고려
17) 노드 업그레이드 순서 정리
18) drain → upgrade → uncordon 시퀀스
19) addon/CNI 업그레이드 영향 체크
20) cluster-info 덤프 확인
21) kubeadm config view 확인
22) API server readiness 확인
23) upgrade 실패 시 rollback 전략 정리
24) etcd snapshot 무결성 체크
25) snapshot 복구 후 클러스터 확인 항목
26) 클러스터 다운타임 최소화 전략
27) 패치 업그레이드 vs 마이너 차이
28) kubeadm token 관련 확인
29) 업그레이드 문서 요약 작성
30) Day9 정리 체크리스트 만들기
