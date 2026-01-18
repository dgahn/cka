Day 6: 보안(RBAC/ServiceAccount/Role/ClusterRole/Binding)

1) ServiceAccount 생성
  - k create sa app-sa
2) Pod에 ServiceAccount 지정
  - Pod spec: serviceAccountName: app-sa
3) Role 생성(네임스페이스 리소스 read)
  - k create role pod-reader --verb=get,list --resource=pods
4) RoleBinding 생성
  - k create rolebinding read-pods --role=pod-reader --serviceaccount=default:app-sa
5) RoleBinding으로 권한 부여 확인(can-i)
  - k auth can-i list pods --as=system:serviceaccount:default:app-sa
6) ClusterRole 생성(노드 read)
  - k create clusterrole node-reader --verb=get,list --resource=nodes
7) ClusterRoleBinding 생성
  - k create clusterrolebinding node-read --clusterrole=node-reader --serviceaccount=default:app-sa
8) Role vs ClusterRole 차이 확인
  - Role=네임스페이스, ClusterRole=클러스터 범위
9) 특정 verbs만 허용(get/list)
  - k create role pod-read --verb=get,list --resource=pods
10) 특정 리소스만 허용(pods)
  - Role spec.rules.resources: ["pods"]
11) 특정 apiGroup 허용
  - rules.apiGroups: ["apps"]
12) Role에 resourceNames 지정
  - rules.resourceNames: ["web-pod"]
13) ServiceAccount 토큰 마운트 확인
  - k exec <pod> -- ls /var/run/secrets/kubernetes.io/serviceaccount
14) automountServiceAccountToken 끄기
  - Pod spec: automountServiceAccountToken: false
15) Pod에서 API 호출 테스트(권한 제한 확인)
  - curl -k https://$KUBERNETES_SERVICE_HOST:$KUBERNETES_SERVICE_PORT
16) default SA 권한 확인
  - k auth can-i list pods --as=system:serviceaccount:default:default
17) 여러 Role을 하나의 RoleBinding에 매핑
  - RoleBinding subjects에 여러 SA 추가
18) 하나의 ClusterRole을 여러 SA에 매핑
  - ClusterRoleBinding subjects에 여러 SA 추가
19) kubectl auth can-i 다양한 케이스
  - k auth can-i create deploy
  - k auth can-i create deploy --as=system:serviceaccount:default:app-sa
20) Namespace 범위 권한 제한 실습
  - 다른 네임스페이스에서 can-i 확인
