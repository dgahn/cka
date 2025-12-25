Day 5(스토리지: PV/PVC/StorageClass, 볼륨 타입) 실습 예제 30개야.

  1. StorageClass 목록 확인
  2. 기본(StorageClass) 확인
  3. PVC 생성(기본 SC로 동적 프로비저닝)
  4. PVC 상태 확인(Pending → Bound)
  5. Pod에서 PVC 마운트 후 파일 쓰기
  6. Pod 재시작 후 데이터 유지 확인
  7. PVC 용량 확장(가능한 SC에서)
  8. PV 수동 생성(hostPath)
  9. PVC를 PV에 수동 바인딩
  10. PV reclaimPolicy 차이 확인(Retain/Delete)
  11. PV accessModes 차이 실습(RWO/ROX/RWX)
  12. 동일 PVC를 여러 Pod에 마운트(RWO 동작 확인)
  13. emptyDir 볼륨 실습(파드 종료 시 데이터 삭제)
  14. emptyDir medium: Memory 실습
  15. hostPath 볼륨 실습(노드 로컬)
  16. configMap 볼륨 실습(파일로 마운트)
  17. secret 볼륨 실습(파일로 마운트)
  18. downwardAPI 볼륨 실습
  19. projected 볼륨 실습(여러 소스 합치기)
  20. subPath 마운트 실습
  21. volumeMounts.readOnly 확인
  22. PVC에 selector 사용(레이블 PV 매칭)
  23. StatefulSet + PVC 템플릿 실습
  24. StorageClass 파라미터 확인
  25. volumeBindingMode 차이 확인
  26. local PV 사용 시 nodeAffinity 확인
  27. PV finalizers 확인 및 제거 실습
  28. PVC 삭제 후 PV 상태 확인
  29. reclaimPolicy Retain 시 수동 정리 실습
  30. Day5 리소스 정리(PV/PVC/Pod/SC)