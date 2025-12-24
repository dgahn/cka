• Day 1 연습문제 20개 (kubectl 기본기)

  1. 현재 kubeconfig 컨텍스트 목록을 출력하고, 현재 컨텍스트 이름을 확인하라.
	  1. k config get-contexts
	  2. k config current-contexts
  2. 컨텍스트를 kind-cka로 전환하라.
	  1. k config use-context kind-cka
		- use-context를 context를 변경하는 것이고
		- set-context는 context 이름을 변경하는 것이다.
  3. ckaday1 네임스페이스를 생성하라.
	  1. k create namespace ckaday1
		  - 확인은 k get ns
  4. ckaday1 네임스페이스에서 nginx:1.25 이미지로 파드 web을 생성하라.
	  - k run web --image=nginx1.25 -n ckaday1
  5. web 파드 로그를 확인하라.
	  - k logs -f --tail 100 web -n ckaday1
  6. web 파드에 kubectl exec로 들어가서 /usr/share/nginx/html 내용을 확인하라.
	  - k exec web -n ckaday1 -it -- ls /usr/share/nginx/html
  7. web 파드에 라벨 app=web을 추가하라.
	  - k label pod web -n ckaday1 app=web
	  - k describe pod web -n ckaday1
  8. ckaday1 네임스페이스에서 라벨 app=web 파드만 조회하라.
	  - k get pod -n ckaday1 -l app=web
  9. ckaday1 네임스페이스에서 busybox 파드 utils를 생성하고 sleep 3600으로 유지하라.
	  - k run utils --image=busybox -n ckaday1 --command -- sleep 3600
  10. utils 파드 내부에서 web 파드로 curl 시도하라(서비스 없이).
	  - k get pod web -n ckaday1 -o wide
	  - k exec -it utils -n ckaday1 -- wget -qo- http://10.244.3.7
  11. ckaday1 네임스페이스에 web-svc라는 ClusterIP 서비스를 생성하고 web 파드(라벨 기반)로 연결하라.
	- k expose pod web -n ckaday1 --name=web-svc --port=80 --target-port=80
  12. utils 파드에서 web-svc로 curl 하여 응답을 확인하라.
	  - k exec utils -it -n ckaday1 -- wget -qo- http://web-svc
  13. ckaday1 네임스페이스에서 nginx:1.25로 web-deploy Deployment(복제본 2개)를 생성하라.
	  - k create deployment web-deploy -n ckaday1 --image=nginx:1.25 --replicas=2
  14. web-deploy의 파드 상태를 확인하라.
	  - k get deploy web-deploy -n ckaday1
  15. web-deploy를 nginx:1.26으로 업데이트하라.
	  - k set image deployment/web-deploy -n ckday1 nginx=nginx:1.26
  16. web-deploy 롤아웃 상태를 확인하라.
	  - k rollout status deployment/web-deploy -n ckaday1
	  - k rollout history deployment/web-deploy -n ckaday1
  17. ckaday1 네임스페이스의 모든 리소스를 삭제하라.
	  - k delete all --all -n ckaday1
  18. ckaday1 네임스페이스 자체를 삭제하라.
	  - k delete ns ckaday1