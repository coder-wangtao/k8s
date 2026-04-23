kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

会创建 DaemonSet，在每个 Node 上运行 Calico agent (calico-node)
自动为 Pod 配置路由
支持 BGP 或 VXLAN，根据配置选择
