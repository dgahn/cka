# 1. Create a new pod called web-pod with image busybox Allow the pod to be able to set system_time (The container should sleep for 3200 seconds)

```
kubectl run web-pod --image=busybox --command sleep 3200 --dry-run=client -o yaml > busybox.yml
```

k8s 문서에서 sys_time 검색
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo-4
spec:
  containers:
  - name: sec-ctx-4
    image: gcr.io/google-samples/hello-app:2.0
    securityContext:
      capabilities:
        add: ["NET_ADMIN", "SYS_TIME"]
```

```
$ kubectl apply -f busybox.yml -n cka
$ kubectl desribe web-pod -n cka
```

# 2. Create a new deployment called myproject, with image nginx:1.16 and 1 replicas. Next upgrade the deployment to version 1.17 using rolling update Make sure that the version upgrade is recorded in the resourcde annotation.

```
$ kubectl create deployment myproject --image=nginx:1.16 -n cka
$ kubectl get deployment -n cka
$ kubectl set image deploy/myproject nginx=nginx:1.17 --record
$ kubectl rollout history deploy/myproject
```

# 3. Create a new deployment called my-deployment Scale the deployment to 3 replicas. Make sure desired number of pod always running

```
$ kubectl create deployment my-deployment --image=nginx --replicas=3
$ kubectl get deployment
$ kubectl get pod
```

# 4. Deploy a web-nginx pod using the nginx:1.17 image with the labels set to tier=web-app
```
$ kubectl run web-nginx --image:nginx:1.17 -l tier=web-app
$ kubectl get pods --show-labels
```
# 5. Create a static pod on node01 called static-pod with image nginx and you have to make sure that it is recreated/restarted automatically in case of any failure happens
- static pod는 k8s api가 아니라 직접 manifest 파일을 만들어서 만드는 Pod

```
controlplane:~$ kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   30d   v1.34.3
node01         Ready    <none>          30d   v1.34.3
controlplane:~$ ssh node01
Last login: Sun Jan 18 00:07:10 2026 from 10.244.12.198
node01:~$ ps aux | grep kubelet
root        1207  0.6  4.1 1888340 80240 ?       Ssl  Jan17   0:17 /usr/bin/kubelet --bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf --config=/var/lib/kubelet/config.yaml --pod-infra-container-image=registry.k8s.io/pause:3.10.1 --container-runtime-endpoint unix:///run/containerd/containerd.sock --cgroup-driver=systemd --eviction-hard imagefs.available<5%,memory.available<100Mi,nodefs.available<5% --fail-swap-on=false
root       12393  0.0  0.0   3528  1792 pts/0    S+   00:08   0:00 grep --color=auto kubelet
node01:~$ cat /var/lib/kubelet/config.yaml | grep static
staticPodPath: /etc/kubernetes/manifests
node01:~$ cd /etc/kubernetes/manifests/
node01:/etc/kubernetes/manifests$ pwd
/etc/kubernetes/manifests
```

문서 보고 yml 파일 만들고 노드만 나가면 실제로 실행되고 있는 것을 확인할 수 있음

# 6. Create a pod called pod-multi with two containers, as given below: 
## 6-1 : Container 1 - name: container1, image: nginx
## 6-2 : Container 2 - name: container2, image: busybox, command sleep 4800

```
$ kubectl run pod-multi --image=nginx --dry-run=client -o yaml -n cka > multi-pod.yaml 

$ vi multi-pod.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: multi-pod
  name: multi-pod
  namespace: cka
spec:
  containers:
  - image: nginx
    name: container1
    resources: {}
  - name: container2
    image: busybox
    args:
    - sleep
    - "4800"
  dnsPolicy: ClusterFirst
  restartPo
```
```
$ kubectl apply -f multi-pod.yaml
$ kubectl get pods
```

# 7. Create a pod called test-pod in "custom" namesapce belonging to the test environment (env=test) and backend tier (tier=backend). image:nginx:1.17
```
$ kubectl create namespace custom
$ kubectl run test-pod --image=nginx:1.17 -n custom -l env=test --dry-run=client -o test-pod.yaml
$ kubectl get pod -n custom --show-labels
```

# 8. Get the node node01 in Json format and store it in a file at ./node-info.json
```
$ kubectl get node node01 -o json > ./node-info.json
```
# 9. Use JSON PATH query to retrieve the osImages of all the nodes and store it in a file "all-nodes-os-info.txt" at root location. (Note: The osImage are under the nodeInfo section under status of each node.)
```
$ kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.osImage}' > "./all-nodes-os-info.txt"
$ cat ./all-nodes-os-info.txt
```
# 10. Upgrade the Cluster (Master and worker Node) from 1.18.0 to 1.19.0. Make sure to first drain both Node and make it available after upgrade.
문서 보고 그대로 하면 됨. (주의. 업그레이드할 버전 정보를 찾고 drain 관련 문서로 봐야함.)

controlplane
1. drain
2. 업그레이드
3. uncorndon

node
1. drain
2. 업그레이드
3. uncorndon

# 11.  Take a backup of the ETCD database and save it to "opt/etcd-backup.db" Also restore the ETCD database from the backup

# 12. Create a new user "ajeet". Grant him access to the cluster. User "ajeet" should have permission to create, list get, update and delete pods. The private key at location: /root/ajeet/.key and csr at /root/ajeet.csr
- 버전이 바뀌면서 달라진듯
# 13. Create a nginx pod called dns-resolver using image nginx, expose it internally with a service called dns-resolver-service.
## check if pod and service name are resolvable fro within the cluster.
## Use the image: busybox:1.28 for dns lookup
## Save the result in /root/nginx.svc

```
$ k run dns-resolver-service --image=nginx
$ k get pod
$ k expose pod dns-resolver --name=dns-resolver-service --port=80 --target-port=80 --type=ClusterIP
$ k run test-nslookup --image=busybox:1.28 --rm -it --restart=Never -- nslookup dns-resolver-service > /root/nginx.svc
```
# 14. A pod "appychip" (image=nginx) in default namespace is not running. Find the probel and fix it and make it running
```
$ k describe pod appychip
// 이벤트 확인

```

# 15. Create a ReplicaSet (Name: appychip, image: nginx:1.18, replicas: 4) There is already a pod running in a cluster. Make sure that the total count of pods running in the cluster is not more than 4

# 16. Create a Network Policy named "appychip" in default namespace There should be two types, ingress and egress. The ingress should block traffic from an IP range of your choice except some other IP range. should also have namespace and pod selector. Port for ingress policy should be 6379 For Egress, it should allow traffic to an IP range of your choice on 5978 port.
문서보고 진행하면 됨.

# 17. You have access to multiple clusters from your main terminal throush kubectl contexts. Write all those context names into /opt/course/1/contexts. Next write a command to display the current context into /opt/course/1/context_default_kubectl.sh, the command should use kubectl. Finally write a second command doing the same thing into /opt/course/1/context_default_no_kubectl.sh, but without the use of kubectl.

```
$ kubectl config get-contexts -o name > /opt/course/1/contexts
$ vi /opt/course/1/context_default_kubectl.sh
kubectl config get-contexts
$ chomod +x context_default_kubectl.sh
$ ./context_default_kubectl.sh

$ vi /opt/course/1/context_default_no_kubectl.sh
cat ~/.kube/config | grep current
$ chmod +x context_default_no_kubectl.sh
```

# 18.  There are various Pods in all namespaces. Write a command into /opt/course/5/find_pods.sh which list all Pods sorted by their AGE (metadata.creationTimestamp). Write a second command into /opt/course/5/find_pods_uid.sh which lists all Pods sorted by field metadata.uid. Use kubectl sorting for both commands
```
$ kubectl get pod -A --sort-by=.metadata.creationTimestamp
$ mkdir -p /opt/course/5
```

# 19. ssh into the controlplane node with ssh cluster1-controlplane1. Check how the controlplane compoenets kubelet, kube-apiserver, kubescheduler, kube-controller-manager and etcd are started/installed on the controlplane node. Also find out the DNS application and how it's started/installed on the controlplane node. Write your findings into file /opt/course/8/controlplane-components.txt. The file should be structed like:
## /opt/course/8/controlplane-compoenets.txt
## kubelet: [TYPE]
## kube-apiserver: [TYPE]
## kube-schduler: [TYPE]
## kube-controller-manager: [TYPE]
## etcd: [TYPE]
## dns: [TYPE] [NAME]
## choices of [TYPE] are: not installed, process, static-pod, pod


```
## kubelet: process
## kube-apiserver: static-pod
## kube-scheduler: static-pod
## kube-controller-manager: static-pod
## etcd: static-pod
## dns: pod coredns
```

# 20. There are two deployments. frontend and backend deployment. frontend will be in fronted NS and backend will be backend NS. Apply the leat permissive policy to have interaction between frontend and backend deployment. Below are the 3 YAML file to apply network policy. Choose either of them with least permission.
## 1 YAML - pod selector of all. type is ingress and pod selector with all
## 2 YAML - pod slelector as well as namespace selector are present
## 3 YAML - pod selector, NS selector, POD CIDR

# 21. An nginx deployment configured via a ConfigMap containing the Nginx config file. The task is to ensure that TLS 1.2 should not be supported or permitted. And it should only work with TLS1.3 Do the required steps and verify that it work with TLS 1.3
# 22. 
## Namespace : sound-repeater
## Exposing Service echoserver-serivce on http://example.org/echo using Service port 8080
### Expose the service echo-server service in the given namespace Create an nginx ingress for above deployment and service for the host https://www.example.org/echo over port 80 curl -o /dev/null -s -w "%{http_code}\n" http://example.org/echo