它和 Deployment 最大的区别在于：StatefulSet 会保证 Pod 的稳定身份、稳定存储和有序部署。

1.Pod 名字是固定且有序的，例如：
my-app-0
my-app-1
my-app-2

2. 🌐 稳定的网络标识
   每个 Pod 都有固定 DNS：
   my-app-0.my-service.default.svc.cluster.local

3. 💾 独立持久存储
   每个 Pod 都绑定自己的 PVC（持久卷）：
   my-app-0 → volume-0
   my-app-1 → volume-1

4. 🔄 有序部署与扩缩容
   StatefulSet 是按顺序操作的：
   创建：0 → 1 → 2
   删除：2 → 1 → 0

5. ⬆️ 滚动更新有序执行
   更新时也是逐个 Pod 更新，保证系统稳定性。

StatefulSet 适合：
🗄️ 数据库：MySQL、PostgreSQL
🧠 分布式系统：Kafka、Zookeeper
🔍 搜索引擎：Elasticsearch
📊 需要持久状态的服务

1️⃣ StatefulSet 和 Headless Service + PVC 是怎么配合工作的?
StatefulSet：负责“管理 Pod 的顺序和身份”
它做三件关键事：
给 Pod 分配固定名字：app-0 / app-1 / app-2
控制 Pod 按顺序创建/删除
为每个 Pod 绑定专属存储（PVC）
👉 但它不负责服务发现（DNS）

2️⃣ Headless Service：负责“给每个 Pod 分配稳定网络身份”
Headless Service 的特点是：
clusterIP: None
它不会做负载均衡，而是：
👉 直接给每个 Pod 分配 DNS 记录
例如：
app-0.my-svc.default.svc.cluster.local
app-1.my-svc.default.svc.cluster.local
app-2.my-svc.default.svc.cluster.local
📌 作用：
让 Pod “互相找得到”
提供稳定网络身份

3️⃣ PVC（PersistentVolumeClaim）：负责“每个 Pod 的独立存储”
StatefulSet 会自动创建：
data-app-0
data-app-1
data-app-2
每个 Pod 对应一个 PVC：
Pod PVC
app-0 data-app-0
app-1 data-app-1
app-2 data-app-2
