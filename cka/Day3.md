Day 3(구성관리: ConfigMap/Secret, 환경변수, 볼륨 마운트) 실습 예제 30개야. 모두 kubectl 기준.

  1. ConfigMap 생성: --from-literal
  2. ConfigMap 생성: --from-file
  3. ConfigMap 생성: 디렉터리 전체 --from-file
  4. ConfigMap YAML로 작성 후 적용
  5. ConfigMap 조회: kubectl get cm -o yaml
  6. ConfigMap 키 변경 후 재적용
  7. Pod 환경변수로 ConfigMap 단일 키 주입
  8. Pod 환경변수로 ConfigMap 전체 주입 (envFrom)
  9. ConfigMap을 볼륨으로 마운트, 파일 생성 확인
  10. ConfigMap 마운트 경로에 subPath 사용
  11. ConfigMap 업데이트 후 마운트 파일 반영 확인
  12. ConfigMap 업데이트가 env에 즉시 반영되지 않는 것 확인
  13. Secret 생성: --from-literal
  14. Secret 생성: --from-file
  15. Secret 생성: type=Opaque 명시
  16. Secret 내용 확인(kubectl get secret -o yaml)하고 base64 decode
  17. Pod 환경변수로 Secret 단일 키 주입
  18. Pod 환경변수로 Secret 전체 주입 (envFrom)
  19. Secret을 볼륨으로 마운트, 파일 생성 확인
  20. Secret 마운트에 defaultMode 설정
  21. Secret type=kubernetes.io/dockerconfigjson 생성
  22. imagePullSecret로 private image pull 시도
  23. ConfigMap/Secret을 동시에 env로 주입
  24. ConfigMap/Secret을 동시에 볼륨으로 마운트
  25. 동일 키 충돌 시 우선순위 확인(env vs envFrom)
  26. Pod 재시작 없이 ConfigMap 마운트 업데이트 확인
  27. Secret 업데이트 후 마운트 파일 반영 확인
  28. Secret을 volumeMounts.readOnly: true로 마운트
  29. kubectl describe pod로 env/volumes 확인
  30. Day3 리소스 정리: ConfigMap/Secret/Pod 일괄 삭제