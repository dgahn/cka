Day 3(구성관리: ConfigMap/Secret, 환경변수, 볼륨 마운트) 실습 예제 30개야. 모두 kubectl 기준.

  1. ConfigMap 생성: --from-literal
    - k create cm app-cm --from-literal=APP_ENV=prod
  2. ConfigMap 생성: --from-file
    - k create cm app-cm --from-file=app.conf
  3. ConfigMap 생성: 디렉터리 전체 --from-file
    - k create cm app-cm --from-file=conf.d/
  4. ConfigMap YAML로 작성 후 적용
    - k apply -f cm.yaml
  5. ConfigMap 조회: kubectl get cm -o yaml
    - k get cm app-cm -o yaml
  6. ConfigMap 키 변경 후 재적용
    - k edit cm app-cm
  7. Pod 환경변수로 ConfigMap 단일 키 주입
    - env: valueFrom.configMapKeyRef(name=app-cm, key=APP_ENV)
  8. Pod 환경변수로 ConfigMap 전체 주입 (envFrom)
    - envFrom: configMapRef: name: app-cm
  9. ConfigMap을 볼륨으로 마운트, 파일 생성 확인
    - volumes: configMap: name: app-cm
    - volumeMounts: mountPath: /etc/config
  10. ConfigMap 마운트 경로에 subPath 사용
    - volumeMounts: mountPath: /etc/config/app.conf, subPath: app.conf
  11. ConfigMap 업데이트 후 마운트 파일 반영 확인
    - k edit cm app-cm
    - Pod에서 cat /etc/config/app.conf 확인
  12. ConfigMap 업데이트가 env에 즉시 반영되지 않는 것 확인
    - env 값 확인 후 CM 수정, Pod 재시작 전 변화 없음 확인
  13. Secret 생성: --from-literal
    - k create secret generic app-secret --from-literal=DB_PASS=pass123
  14. Secret 생성: --from-file
    - k create secret generic app-secret --from-file=./db.pass
  15. Secret 생성: type=Opaque 명시
    - k create secret generic app-secret --type=Opaque --from-literal=DB_PASS=pass123
  16. Secret 내용 확인(kubectl get secret -o yaml)하고 base64 decode
    - k get secret app-secret -o yaml
    - echo <base64> | base64 -d
  17. Pod 환경변수로 Secret 단일 키 주입
    - env: valueFrom.secretKeyRef(name=app-secret, key=DB_PASS)
  18. Pod 환경변수로 Secret 전체 주입 (envFrom)
    - envFrom: secretRef: name: app-secret
  19. Secret을 볼륨으로 마운트, 파일 생성 확인
    - volumes: secret: secretName: app-secret
    - volumeMounts: mountPath: /etc/secret
  20. Secret 마운트에 defaultMode 설정
    - volumes: secret: secretName: app-secret, defaultMode: 0400
  21. Secret type=kubernetes.io/dockerconfigjson 생성
    - k create secret docker-registry regcred --docker-server=<server> --docker-username=<u> --docker-password=<p> --docker-email=<e>
  22. imagePullSecret로 private image pull 시도
    - Pod spec: imagePullSecrets: - name: regcred
  23. ConfigMap/Secret을 동시에 env로 주입
    - envFrom: configMapRef + secretRef
  24. ConfigMap/Secret을 동시에 볼륨으로 마운트
    - volumes 두 개 추가 후 서로 다른 mountPath
  25. 동일 키 충돌 시 우선순위 확인(env vs envFrom)
    - env가 envFrom보다 우선함 확인
  26. Pod 재시작 없이 ConfigMap 마운트 업데이트 확인
    - CM 수정 후 파일 내용 변경 확인
  27. Secret 업데이트 후 마운트 파일 반영 확인
    - Secret 수정 후 파일 내용 변경 확인
  28. Secret을 volumeMounts.readOnly: true로 마운트
    - volumeMounts: readOnly: true
  29. kubectl describe pod로 env/volumes 확인
    - k describe pod <pod-name>
  30. Day3 리소스 정리: ConfigMap/Secret/Pod 일괄 삭제
    - k delete cm,secret,pod --all
