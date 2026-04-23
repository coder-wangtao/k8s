Horizontal Pod Autoscaler (HPA) 根据 Pod 的资源使用情况（例如 CPU 或内存），动态调整 Pod 的副本数。它的工作原理是：
监控 Pod 的资源使用情况（CPU、内存等）
根据预设的目标指标，自动增加或减少 Pod 副本数量。
HPA 通过 Kubernetes 的 Metrics API 获取 Pod 的资源数据，而 metrics-server 是实现 Metrics API 的组件。

metrics-server 是一个轻量级的监控工具，它通过读取 kubelet 中的 cAdvisor 数据，收集集群内所有节点和 Pod 的资源使用情况（如 CPU 和内存的使用量）。
这些数据被 HPA、kubectl top 和其他组件用来进行资源管理。

kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
