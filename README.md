<img src="assets/logo/horizontal/color/krew-horizontal-color.png" width="480"
  alt="Krew logo"/>

Krew 是一个用来管理 Kubectl 插件的工具，名字大概来自于 OS X 下著名的软件包管理器 Homebrew，使用 Krew 能够方便的查找、安装和使用 Kubectl 插件。

## 1 通过 krew 安装 kubectl 插件
### 1.1 选择 Kubernetes 集群
如果没有现成的 Kubernetes 集群，可以选择网上免费的 Kubernetes 集群资源：

#### 1.1.1 在 kata 中利用 Ubuntu 安装指定版本的 Kubernetes 集群
具体方式可以见：[ubuntu-Kubernetes](https://github.com/yu3peng/ubuntu-Kubernetes)

#### 1.1.2 在 kata 中直接使用 Kubernetes Playgroud
登录 [Kubernetes Playgroud](https://katacoda.com/courses/kubernetes/playground) 使用，本实践采用此种方式进行。

### 1.2 安装 krew

#### 1.2.1 在终端上运行以下命令安装 krew
```shell
set -x; cd "$(mktemp -d)" &&
curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/krew.{tar.gz,yaml}" &&
tar zxvf krew.tar.gz &&
KREW=./krew-"$(uname | tr '[:upper:]' '[:lower:]')_amd64" &&
"$KREW" install --manifest=krew.yaml --archive=krew.tar.gz &&
"$KREW" update
```

#### 1.2.2 将 $HOME/.krew/bin 加入到环境变量
```shell
export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
```

#### 1.2.3 查询可以安装的 kubectl 插件
```shell
master $ kubectl krew search
+ kubectl krew search
NAME                            DESCRIPTION                                         INSTALLED
access-matrix                   Show an RBAC access matrix for server resources     no
。。。
whoami                          Show the subject that's currently authenticated...  no
```

### 1.3 安装 kubectl 插件
这里以 kubectl tree 举例说明，其他插件安装方式相同：

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

## 2 查看 kubectl 插件

### 2.1 kubectl tree
```shell
master $ kubectl tree deployment coredns -n kube-system
+ kubectl tree deployment coredns -n kube-system
NAMESPACE    NAME                              READY  REASON  AGE
kube-system  Deployment/coredns                -              44m
kube-system  └─ReplicaSet/coredns-66bff467f8   -              43m
kube-system    ├─Pod/coredns-66bff467f8-vqpss  True           43m
kube-system    └─Pod/coredns-66bff467f8-z8fg4  True           43m
```

### 2.2 kubectl access-matrix
```shell
master $ kubectl access-matrix
+ kubectl access-matrix
NAME                                                          LIST  CREATE  UPDATE  DELETE
apiservices.apiregistration.k8s.io                            ✔     ✔       ✔       ✔
bindings                                                            ✔
certificatesigningrequests.certificates.k8s.io                ✔     ✔       ✔       ✔
clusterrolebindings.rbac.authorization.k8s.io                 ✔     ✔       ✔       ✔
clusterroles.rbac.authorization.k8s.io                        ✔     ✔       ✔       ✔
componentstatuses                                             ✔
configmaps                                                    ✔     ✔       ✔       ✔
controllerrevisions.apps                                      ✔     ✔       ✔       ✔
cronjobs.batch                                                ✔     ✔       ✔       ✔
csidrivers.storage.k8s.io                                     ✔     ✔       ✔       ✔
csinodes.storage.k8s.io                                       ✔     ✔       ✔       ✔
customresourcedefinitions.apiextensions.k8s.io                ✔     ✔       ✔       ✔
daemonsets.apps                                               ✔     ✔       ✔       ✔
deployments.apps                                              ✔     ✔       ✔       ✔
endpoints                                                     ✔     ✔       ✔       ✔
endpointslices.discovery.k8s.io                               ✔     ✔       ✔       ✔
events                                                        ✔     ✔       ✔       ✔
events.events.k8s.io                                          ✔     ✔       ✔       ✔
horizontalpodautoscalers.autoscaling                          ✔     ✔       ✔       ✔
ingressclasses.networking.k8s.io                              ✔     ✔       ✔       ✔
ingresses.extensions                                          ✔     ✔       ✔       ✔
ingresses.networking.k8s.io                                   ✔     ✔       ✔       ✔
jobs.batch                                                    ✔     ✔       ✔       ✔
leases.coordination.k8s.io                                    ✔     ✔       ✔       ✔
limitranges                                                   ✔     ✔       ✔       ✔
localsubjectaccessreviews.authorization.k8s.io                      ✔
mutatingwebhookconfigurations.admissionregistration.k8s.io    ✔     ✔       ✔       ✔
namespaces                                                    ✔     ✔       ✔       ✔
networkpolicies.networking.k8s.io                             ✔     ✔       ✔       ✔
nodes                                                         ✔     ✔       ✔       ✔
persistentvolumeclaims                                        ✔     ✔       ✔       ✔
persistentvolumes                                             ✔     ✔       ✔       ✔
poddisruptionbudgets.policy                                   ✔     ✔       ✔       ✔
pods                                                          ✔     ✔       ✔       ✔
podsecuritypolicies.policy                                    ✔     ✔       ✔       ✔
podtemplates                                                  ✔     ✔       ✔       ✔
priorityclasses.scheduling.k8s.io                             ✔     ✔       ✔       ✔
replicasets.apps                                              ✔     ✔       ✔       ✔
replicationcontrollers                                        ✔     ✔       ✔       ✔
resourcequotas                                                ✔     ✔       ✔       ✔
rolebindings.rbac.authorization.k8s.io                        ✔     ✔       ✔       ✔
roles.rbac.authorization.k8s.io                               ✔     ✔       ✔       ✔
runtimeclasses.node.k8s.io                                    ✔     ✔       ✔       ✔
secrets                                                       ✔     ✔       ✔       ✔
selfsubjectaccessreviews.authorization.k8s.io                       ✔
selfsubjectrulesreviews.authorization.k8s.io                        ✔
serviceaccounts                                               ✔     ✔       ✔       ✔
services                                                      ✔     ✔       ✔       ✔
statefulsets.apps                                             ✔     ✔       ✔       ✔
storageclasses.storage.k8s.io                                 ✔     ✔       ✔       ✔
subjectaccessreviews.authorization.k8s.io                           ✔
tokenreviews.authentication.k8s.io                                  ✔
validatingwebhookconfigurations.admissionregistration.k8s.io  ✔     ✔       ✔       ✔
volumeattachments.storage.k8s.io                              ✔     ✔       ✔       ✔
No namespace given, this implies cluster scope (try -n if this is not intended)
```

### 2.3 kubectl advise-psp
关于 PSP，可以参考：[Kubernetes 中的 Pod 安全策略](https://blog.fleeto.us/post/psp-in-kubernetes/)

```shell
master $ kubectl advise-psp inspect
+ kubectl advise-psp inspect
apiVersion: policy/v1beta1
kind: PodSecurityPolicy
metadata:
  creationTimestamp: null
  name: pod-security-policy-all-20200604023350
spec:
  allowedCapabilities:
  - NET_ADMIN
  allowedHostPaths:
  - pathPrefix: /etc/ssl/certs
    readOnly: true
  - pathPrefix: /run/flannel
    readOnly: true
  - pathPrefix: /etc/cni/net.d
    readOnly: true
  - pathPrefix: /lib/modules
    readOnly: true
  - pathPrefix: /dev
    readOnly: true
  - pathPrefix: /run/xtables.lock
    readOnly: true
  fsGroup:
    rule: RunAsAny
  hostNetwork: true
  hostPorts:
  - max: 0
    min: 0
  privileged: true
  runAsUser:
    rule: RunAsAny
  seLinux:
    rule: RunAsAny
  supplementalGroups:
    rule: RunAsAny
  volumes:
  - hostPath
  - configMap
  - secret
```

## 3 利用 krew 新建 kubectl 插件 
Krew 除了落在客户端的可执行文件之外，和其它软件包管理系统一样，也同样需要有一个索引系统，并根据索引进行软件查询和下载，下载之后的软件保存在本地，供 kubectl 调用。

### 3.1 索引
Krew 的索引保存在一个名为 [krew-index](https://github.com/kubernetes-sigs/krew-index) 的代码库中。其中的 plugins 目录保存了一组 yaml 文件，就是插件的目录。

#### 3.1.1 YAML 清单
随意打开一个清单文件，我们以 [tree](https://github.com/kubernetes-sigs/krew-index/blob/master/plugins/tree.yaml) 为例，可以看到这样的内容：
```yaml
apiVersion: krew.googlecontainertools.github.com/v1alpha2
kind: Plugin
metadata:
  name: tree
spec:
  version: v0.4.0
  homepage: https://github.com/ahmetb/kubectl-tree
  shortDescription: Show a tree of object hierarchies through ownerReferences
  description: |
    This plugin shows sub-resources of a specified Kubernetes API object in a
    tree view in the command-line. The parent-child relationship is discovered
    using ownerReferences on the child object.
  caveats: |
    * For resources that are not in default namespace, currently you must
      specify -n/--namespace explicitly (the current namespace setting is not
      yet used).
  platforms:
  - selector:
      matchLabels:
        os: darwin
        arch: amd64
    uri: https://github.com/ahmetb/kubectl-tree/releases/download/v0.4.0/kubectl-tree_v0.4.0_darwin_amd64.tar.gz
    sha256: c90dd260212b7da7163f12a27269923dedaeb17667616d990aa7ddbee31d2364
    files:
    - from: "*"
      to: "."
    bin: kubectl-tree
  - selector:
      matchLabels:
        os: linux
        arch: amd64
    uri: https://github.com/ahmetb/kubectl-tree/releases/download/v0.4.0/kubectl-tree_v0.4.0_linux_amd64.tar.gz
    sha256: 3253a981099abceb41f2ea32c89489fd1ba459d950becef2e302f79a8b2f0507
    files:
    - from: "*"
      to: "."
    bin: kubectl-tree
  - selector:
      matchLabels:
        os: windows
        arch: amd64
    uri: https://github.com/ahmetb/kubectl-tree/releases/download/v0.4.0/kubectl-tree_v0.4.0_windows_amd64.tar.gz
    sha256: 8fe0fefe22816c3c34116f7b2e236bc351db053a839f7e2f396c7eaaf88e612c
    files:
    - from: "*"
      to: "."
    bin: kubectl-tree.exe
```
其中 ***apiVersion*** 和 ***kind*** 是固定内容。***platforms*** 是一个数组，指定不同平台下的不同用法。下一级的 ***bin*** 表明了执行命令；***uri*** 和 ***sha256*** 分别指的是下载位置以及压缩包的校验码；接下来的 ***files*** 是一个拷贝命令——从解压后的文件夹中拷贝文件；最后的 ***selector*** 则是针对不同平台的选择标准。

所以要编写一个能够通过 Krew 进行管理的 kubectl 插件，需要以下几个步骤：

* 编写插件代码
* 制作清单和调试
* 上传到 krew-index

下面用一个实际的例子来说明一下这个过程。

### 3.2 编写插件代码
插件代码本身的编写非常简单和随意，可以用你喜欢的任何语言，例如 golang、python 或者 shell。只有一个推荐的命名规则：kubectl-rm，在 kubectl 中调用时就可以使用 kubectl rm 了。例如我要编写一个对输出 JSON 进行过滤的插件，代码如下：

```shell
#!/bin/sh

METADATA=${JSON_METADATA-".metadata.resourceVersion, .metadata.selfLink, .metadata.managedFields, .metadata.generation, .metadata.uid, .metadata.creationTimestamp"}
STATUS=${JSON_STATUS-".status"}
ANNOTATION=${JSON_ANNOTATION-".metadata.annotations.\"kubectl.kubernetes.io/last-applied-configuration\", .metadata.annotations.\"deployment.kubernetes.io/revision\""}
SPEC=${JSON_SPEC-".spec.template.metadata.creationTimestamp, .spec.revisionHistoryLimit, .spec.templateGeneration"}

if ! [ -x "$(command -v jq)" ]; then
  echo 'Error: jq is not installed.' >&2
  exit 1
fi

if [ $# -lt 2 ]
  then
    echo "Usage: $0 [workload-type] [object-name] [other parameters for kubectl]"
    echo "Workload types: 'deployment', 'daemonset', 'configmap', 'statefulset', 'secret'"
    echo "Example: $0 deploy coredns -n kube-system"
    exit 1
fi

TYPE=$1
NAME=$2
OTHER=$*

kubectl get ${OTHER} -ojson | jq -S "del(${METADATA}, ${STATUS}, ${ANNOTATION}, ${SPEC})"
```

想法很简单，获取运行中的对象描述，使用 JQ 对数据进行清理和排序，输出一个相对标准的结果，便于不同环境间的比较和部署的导出。
> 虽然最后是通过 kubectl std-json 的方式调用，这里的 $0 指的仍然是脚本自身。

### 3.3 制作清单和测试
照猫画虎，按照上面的 YAML 代码，编写自己的清单。

清单要求，需要打一个压缩包便于下载，我们把可执行文件和 LICENSE 文件放置到单独的目录 kubectl-std-json-v0.1.0 中，压缩生成一个 .tar.gz 文件，部分清单如下
```yaml
    uri: https://github.com/fleeto/kubectl-std-json/releases/download/v0.1.0/kubectl-std-json-v0.1.0.tar.gz
    sha256: e1ad2398eaed5442042da134fb046fa8276042dd4122da4d872a8e91aeb2a339
    bin: kubectl-std-json
    files:
    - from: kubectl-std-json-*/kubectl-std-json
      to: .
    - from: kubectl-std-json-*/LICENSE
      to: .
```

平台选择方面，我们只支持 OSX 和 Linux，因此只要一个平台元素即可。

压缩包的校验码可以使用 shasum -a 256 命令生成。

上传压缩包之后，可以使用 kubectl krew install --manifest 命令来测试安装。如果一切顺利，在本地就可以使用了。


### krew-index
接下来的操作很常规：fork krew-index，把你的清单写入 plugins 目录，提交 PR 即可。
