Day 4(서비스/네트워킹: Service/Ingress/NetworkPolicy, DNS) 실습 예제 30개야.

  1. Deployment 2개 생성(app=web, app=api)
  2. ClusterIP Service 생성(웹용)
  3. Service selector 확인, Endpoints 확인
  4. Service 포트 매핑 확인(targetPort 변경)
  5. NodePort Service 생성
  6. NodePort로 외부 접근 테스트(클러스터 환경에 따라)
  7. LoadBalancer Service 생성(가능한 환경에서)
  8. Headless Service 생성(clusterIP: None)
  9. Headless + StatefulSet 조합 기본 실습
  10. Service에 sessionAffinity: ClientIP 설정
  11. Service에 다중 포트 설정
  12. kubectl describe svc로 라벨/selector 확인
  13. Endpoints 직접 확인(kubectl get endpoints)
  14. Ingress 리소스 생성(기본 host/path 라우팅)
  15. IngressClass 확인 및 지정
  16. Ingress에 여러 path 규칙 추가
  17. TLS Ingress 설정(Secret 생성 후 연결)
  18. Ingress가 없는 환경에서 왜 동작 안 하는지 파악
  19. Service 없이 Pod 직접 접근 불가 확인
  20. DNS 확인: nslookup으로 Service 이름 조회
  21. DNS 확인: dig로 FQDN 조회
  22. Pod에서 curl로 Service 접근 확인
  23. Pod에서 다른 네임스페이스 서비스 접근(svc.ns.svc.cluster.local)
  24. NetworkPolicy 기본 deny 생성
  25. NetworkPolicy로 특정 라벨 Pod만 허용
  26. NetworkPolicy로 특정 네임스페이스만 허용
  27. NetworkPolicy로 특정 포트만 허용
  28. egress 차단 테스트
  29. Policy 적용 전후 통신 비교
  30. Day4 리소스 정리(Service/Ingress/NetworkPolicy/Deployments)