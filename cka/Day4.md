Day 4(서비스/네트워킹: Service/Ingress/NetworkPolicy, DNS) 실습 예제 30개야.

  1. Deployment 2개 생성(app=web, app=api)
    - k create deploy web --image=nginx:1.25
    - k create deploy api --image=nginx:1.25
    - k label deploy web app=web
    - k label deploy api app=api
  2. ClusterIP Service 생성(웹용)
    - k expose deploy web --name=web-svc --port=80 --target-port=80
  3. Service selector 확인, Endpoints 확인
    - k describe svc web-svc
    - k get endpoints web-svc
  4. Service 포트 매핑 확인(targetPort 변경)
    - k edit svc web-svc
  5. NodePort Service 생성
    - k expose deploy web --name=web-nodeport --type=NodePort --port=80
  6. NodePort로 외부 접근 테스트(클러스터 환경에 따라)
    - k get svc web-nodeport
    - curl http://<node-ip>:<nodeport>
  7. LoadBalancer Service 생성(가능한 환경에서)
    - k expose deploy web --name=web-lb --type=LoadBalancer --port=80
  8. Headless Service 생성(clusterIP: None)
    - k apply -f headless-svc.yaml
  9. Headless + StatefulSet 조합 기본 실습
    - k apply -f sts.yaml
    - k get pods -l app=web
  10. Service에 sessionAffinity: ClientIP 설정
    - k patch svc web-svc -p '{"spec":{"sessionAffinity":"ClientIP"}}'
  11. Service에 다중 포트 설정
    - k edit svc web-svc
  12. kubectl describe svc로 라벨/selector 확인
    - k describe svc web-svc
  13. Endpoints 직접 확인(kubectl get endpoints)
    - k get endpoints
  14. Ingress 리소스 생성(기본 host/path 라우팅)
    - k apply -f ingress.yaml
  15. IngressClass 확인 및 지정
    - k get ingressclass
    - ingress.spec.ingressClassName 설정
  16. Ingress에 여러 path 규칙 추가
    - k edit ingress <ingress-name>
  17. TLS Ingress 설정(Secret 생성 후 연결)
    - k create secret tls web-tls --cert=./tls.crt --key=./tls.key
    - ingress.spec.tls에 secretName 설정
  18. Ingress가 없는 환경에서 왜 동작 안 하는지 파악
    - Ingress Controller 존재 여부 확인
  19. Service 없이 Pod 직접 접근 불가 확인
    - Pod IP로 접근, 재시작 시 IP 변경 확인
  20. DNS 확인: nslookup으로 Service 이름 조회
    - k run dns --image=busybox --restart=Never -- nslookup web-svc
  21. DNS 확인: dig로 FQDN 조회
    - k run dns --image=busybox --restart=Never -- dig web-svc.default.svc.cluster.local
  22. Pod에서 curl로 Service 접근 확인
    - k run curl --image=busybox --restart=Never -- wget -qO- http://web-svc
  23. Pod에서 다른 네임스페이스 서비스 접근(svc.ns.svc.cluster.local)
    - wget -qO- http://web-svc.<ns>.svc.cluster.local
  24. NetworkPolicy 기본 deny 생성
    - k apply -f np-deny-all.yaml
  25. NetworkPolicy로 특정 라벨 Pod만 허용
    - k apply -f np-allow-label.yaml
  26. NetworkPolicy로 특정 네임스페이스만 허용
    - k apply -f np-allow-namespace.yaml
  27. NetworkPolicy로 특정 포트만 허용
    - k apply -f np-allow-port.yaml
  28. egress 차단 테스트
    - k apply -f np-egress-deny.yaml
  29. Policy 적용 전후 통신 비교
    - 적용 전/후 curl 결과 비교
  30. Day4 리소스 정리(Service/Ingress/NetworkPolicy/Deployments)
    - k delete svc,ingress,networkpolicy,deploy --all
