Day 6: 보안(RBAC/ServiceAccount/Role/ClusterRole/Binding)

1) ServiceAccount 생성
2) Pod에 ServiceAccount 지정
3) Role 생성(네임스페이스 리소스 read)
4) RoleBinding 생성
5) RoleBinding으로 권한 부여 확인(can-i)
6) ClusterRole 생성(노드 read)
7) ClusterRoleBinding 생성
8) Role vs ClusterRole 차이 확인
9) 특정 verbs만 허용(get/list)
10) 특정 리소스만 허용(pods)
11) 특정 apiGroup 허용
12) Role에 resourceNames 지정
13) ServiceAccount 토큰 마운트 확인
14) automountServiceAccountToken 끄기
15) Pod에서 API 호출 테스트(권한 제한 확인)
16) default SA 권한 확인
17) 여러 Role을 하나의 RoleBinding에 매핑
18) 하나의 ClusterRole을 여러 SA에 매핑
19) kubectl auth can-i 다양한 케이스
20) Namespace 범위 권한 제한 실습
21) ClusterRoleBinding 잘못 연결 후 권한 과다 확인
22) RBAC 오타로 Forbidden 발생 유도
23) RoleBinding 삭제 후 권한 회수 확인
24) ServiceAccount 삭제 시 영향 확인
25) API groups 목록 확인(kubectl api-resources)
26) --as로 impersonation 테스트
27) --as-group 테스트
28) TokenRequest 생성(가능한 버전)
29) RBAC 리소스 정리
30) Day6 리소스 전체 삭제
