Day 5(스토리지: PV/PVC/StorageClass, 볼륨 타입) 실습 예제 20개야.

  1. StorageClass 목록 확인
    - k get sc
  2. 기본(StorageClass) 확인
    - k get sc -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.annotations.storageclass\.kubernetes\.io/is-default-class}{"\n"}{end}'
  3. PVC 생성(기본 SC로 동적 프로비저닝)
    - k apply -f pvc.yaml
  4. PVC 상태 확인(Pending → Bound)
    - k get pvc
  5. Pod에서 PVC 마운트 후 파일 쓰기
    - Pod에 PVC mount 후 echo test > /data/test.txt
  6. Pod 재시작 후 데이터 유지 확인
    - Pod 삭제 후 재생성, /data/test.txt 확인
  7. PVC 용량 확장(가능한 SC에서)
    - k edit pvc <pvc-name>
  8. PV 수동 생성(hostPath)
    - k apply -f pv-hostpath.yaml
  9. PVC를 PV에 수동 바인딩
    - PVC spec.volumeName 지정
  10. PV reclaimPolicy 차이 확인(Retain/Delete)
    - k get pv -o wide
  11. PV accessModes 차이 실습(RWO/ROX/RWX)
    - PV/PVC accessModes 변경 후 바인딩 확인
  12. 동일 PVC를 여러 Pod에 마운트(RWO 동작 확인)
    - 두 Pod에서 동일 PVC 마운트 시 스케줄 제약 확인
  13. emptyDir 볼륨 실습(파드 종료 시 데이터 삭제)
    - volumes: emptyDir: {}
  14. emptyDir medium: Memory 실습
    - volumes: emptyDir: {medium: Memory}
  15. hostPath 볼륨 실습(노드 로컬)
    - volumes: hostPath: {path: /data/host}
  16. configMap 볼륨 실습(파일로 마운트)
    - volumes: configMap: name: app-cm
  17. secret 볼륨 실습(파일로 마운트)
    - volumes: secret: secretName: app-secret
  18. downwardAPI 볼륨 실습
    - volumes: downwardAPI: items 설정
  19. projected 볼륨 실습(여러 소스 합치기)
    - volumes: projected: sources: configMap + secret
  20. subPath 마운트 실습
    - volumeMounts: subPath 설정
