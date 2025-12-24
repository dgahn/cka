# kind
docker 이미지 중에 클러스터를 구성할 수 있는 이미지

config를 아래와 같이 구성했다.

```
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
  - role: worker
  - role: worker
  - role: worker
  - role: worker
  - role: worker
  - role: worker
```

그리고 명령어는 아래와 같다.

```
kind create cluster --name cka --config kind-config.yaml
```

확인은 아래와 같이 할 수 있다.
```
k get nodes
```
```
NAME                STATUS   ROLES           AGE     VERSION
cka-control-plane   Ready    control-plane   2m27s   v1.35.0
cka-worker          Ready    <none>          2m17s   v1.35.0
cka-worker2         Ready    <none>          2m17s   v1.35.0
cka-worker3         Ready    <none>          2m17s   v1.35.0
cka-worker4         Ready    <none>          2m17s   v1.35.0
cka-worker5         Ready    <none>          2m17s   v1.35.0
cka-worker6         Ready    <none>          2m17s   v1.35.0
cka-worker7         Ready    <none>          2m17s   v1.35.0
cka-worker8         Ready    <none>          2m17s   v1.35.0
```
