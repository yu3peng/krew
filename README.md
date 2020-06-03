<img src="assets/logo/horizontal/color/krew-horizontal-color.png" width="480"
  alt="Krew logo"/>

## 1. 选择 Kubernetes 集群
如果没有现成的 Kubernetes 集群，可以选择网上免费的 Kubernetes 集群资源：

### 1.1 在 kata 中利用 Ubuntu 安装指定版本的 Kubernetes 集群
具体方式可以见：[ubuntu-Kubernetes](https://github.com/yu3peng/ubuntu-Kubernetes)

### 1.2 在 kata 中直接使用 Kubernetes Playgroud
登录 [Kubernetes Playgroud](https://katacoda.com/courses/kubernetes/playground) 使用，本实践采用此种方式进行。

## 2. 安装 krew

### 2.1 在终端上运行以下命令安装 krew
```shell
set -x; cd "$(mktemp -d)" &&
curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/krew.{tar.gz,yaml}" &&
tar zxvf krew.tar.gz &&
KREW=./krew-"$(uname | tr '[:upper:]' '[:lower:]')_amd64" &&
"$KREW" install --manifest=krew.yaml --archive=krew.tar.gz &&
"$KREW" update
```

### 2.2 将 $HOME/.krew/bin 加入到环境变量
```shell
export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
```

### 2.3 查询可以安装的 kubectl 插件
```shell
master $ kubectl krew search
+ kubectl krew search
NAME                            DESCRIPTION                                         INSTALLED
access-matrix                   Show an RBAC access matrix for server resources     no
advise-psp                      Suggests PodSecurityPolicies for cluster.           no
apparmor-manager                Manage AppArmor profiles for cluster.               no
auth-proxy                      Authentication proxy to a pod or service            no
bulk-action                     Do bulk actions on Kubernetes resources.            no
ca-cert                         Print the PEM CA certificate of the current clu...  no
capture                         Triggers a Sysdig capture to troubleshoot the r...  no
change-ns                       View or change the current namespace via kubectl.   no
cilium                          Easily interact with Cilium agents.                 no
cluster-group                   Exec commands across a group of contexts.           no
config-cleanup                  Automatically clean up your kubeconfig              no
cssh                            SSH into Kubernetes nodes                           no
ctx                             Switch between contexts in your kubeconfig          no
custom-cols                     A "kubectl get" replacement with customizable c...  no
debug                           Attach ephemeral debug container to running pod     no
debug-shell                     Create pod with interactive kube-shell.             no
deprecations                    Checks for deprecated objects in a cluster          no
df-pv                           Show disk usage (like unix df) for persistent v...  no
doctor                          Scans your cluster and reports anomalies.           no
duck                            List custom resources with ducktype support         no
eksporter                       Export resources and removes a pre-defined set ...  no
evict-pod                       Evicts the given pod                                no
exec-as                         Like kubectl exec, but offers a `user` flag to ...  no
exec-cronjob                    Run a CronJob immediately as Job                    no
fields                          Grep resources hierarchy by field name              no
fleet                           Shows config and resources of a fleet of clusters   no
gadget                          Gadgets for debugging and introspecting apps        no
get-all                         Like `kubectl get all` but _really_ everything      no
gke-credentials                 Fetch credentials for GKE clusters                  no
gopass                          Imports secrets from gopass                         no
grep                            Filter Kubernetes resources by matching their n...  no
iexec                           Interactive selection tool for `kubectl exec`       no
images                          Show container images used in the cluster.          no
ingress-nginx                   Interact with ingress-nginx                         no
konfig                          Merge, split or import kubeconfig files             no
krew                            Package manager for kubectl plugins.                yes
kubesec-scan                    Scan Kubernetes resources with kubesec.io.          no
kudo                            Declaratively build, install, and run operators...  no
kuttl                           Declaratively run and test operators                no
match-name                      Match names of pods and other API objects           no
modify-secret                   modify secret with implicit base64 translations     no
mtail                           Tail logs from multiple pods matching label sel...  no
neat                            Remove clutter from Kubernetes manifests to mak...  no
net-forward                     Proxy to arbitrary TCP services on a cluster ne...  no
node-admin                      List nodes and run privileged pod with chroot       no
node-restart                    Restart cluster nodes sequentially and gracefully   no
node-shell                      Spawn a root shell on a node via kubectl            no
ns                              Switch between Kubernetes namespaces                no
oidc-login                      Log in to the OpenID Connect provider               no
open-svc                        Open the Kubernetes URL(s) for the specified se...  no
outdated                        Finds outdated container images running in a cl...  no
passman                         Store kubeconfig credentials in keychains or pa...  no
pod-dive                        Shows a pod's workload tree and info inside a node  no
pod-logs                        Display a list of pods to get logs from             no
pod-shell                       Display a list of pods to execute a shell in        no
podevents                       Show events for pods                                no
popeye                          Scans your clusters for potential resource issues   no
preflight                       Executes application preflight tests in a cluster   no
profefe                         Gather and manage pprof profiles from running pods  no
prompt                          Prompts for user confirmation when executing co...  no
prune-unused                    Prune unused resources                              no
rbac-lookup                     Reverse lookup for RBAC                             no
rbac-view                       A tool to visualize your RBAC permissions.          no
resource-capacity               Provides an overview of resource requests, limi...  no
resource-snapshot               Prints a snapshot of nodes, pods and HPAs resou...  no
restart                         Restarts a pod with the given name                  no
rm-standalone-pods              Remove all pods without owner references            no
rolesum                         Summarize RBAC roles for subjects                   no
roll                            Rolling restart of all persistent pods in a nam...  no
schemahero                      Declarative database schema migrations via YAML     no
score                           Kubernetes static code analysis.                    no
service-tree                    Status for ingresses, services, and their backends  no
sick-pods                       Find and debug Pods that are "Not Ready"            no
snap                            Delete half of the pods in a namespace or cluster   no
sniff                           Start a remote packet capture on pods using tcp...  no
sort-manifests                  Sort manifest files in a proper order by Kind       no
spy                             pod debugging tool for kubernetes clusters with...  no
sql                             Query the cluster via pseudo-SQL                    no
ssh-jump                        A kubectl plugin to SSH into Kubernetes nodes u...  no
sshd                            Run SSH server in a Pod                             no
ssm-secret                      Import/export secrets from/to AWS SSM param store   no
status                          Show status details of a given resource.            no
sudo                            Run Kubernetes commands impersonated as group s...  no
support-bundle                  Creates support bundles for off-cluster analysis    no
tail                            Stream logs from multiple pods and containers u...  no
tap                             Interactively proxy Kubernetes Services with ease   no
tmux-exec                       An exec multiplexer using Tmux                      no
topology                        Explore region topology for nodes or pods           no
tree                            Show a tree of object hierarchies through owner...  no
unused-volumes                  List unused PVCs                                    no
view-allocations                List allocations per resources, nodes, pods.        no
view-secret                     Decode Kubernetes secrets                           no
view-serviceaccount-kubeconfig  Show a kubeconfig setting to access the apiserv...  no
view-utilization                Shows cluster cpu and memory utilization            no
virt                            Control KubeVirt virtual machines using virtctl     no
warp                            Sync and execute local files in Pod                 no
who-can                         Shows who has RBAC permissions to access Kubern...  no
whoami                          Show the subject that's currently authenticated...  no
```

## 3. 安装 kubectl tree
```shell
master $ kubectl krew install tree
+ kubectl krew install tree
Updated the local copy of plugin index.
Installing plugin: tree
Installed plugin: tree
\
 | Use this plugin:
 |      kubectl tree
 | Documentation:
 |      https://github.com/ahmetb/kubectl-tree
 | Caveats:
 | \
 |  | * For resources that are not in default namespace, currently you must
 |  |   specify -n/--namespace explicitly (the current namespace setting is not
 |  |   yet used).
 | /
/
WARNING: You installed plugin "tree" from the krew-index plugin repository.
   These plugins are not audited for security by the Krew maintainers.
   Run them at your own risk.
```

### 3.1 利用 kubectl tree 查看
```shell
master $ kubectl tree deployment coredns -n kube-system
+ kubectl tree deployment coredns -n kube-system
NAMESPACE    NAME                              READY  REASON  AGE
kube-system  Deployment/coredns                -              44m
kube-system  └─ReplicaSet/coredns-66bff467f8   -              43m
kube-system    ├─Pod/coredns-66bff467f8-vqpss  True           43m
kube-system    └─Pod/coredns-66bff467f8-z8fg4  True           43m
```
