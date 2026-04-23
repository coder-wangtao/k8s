kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml

支持 kubeadm 集群
YAML 文件会部署 DaemonSet，在每个 Node 上运行 flannel agent
自动为每个 Node 分配子网，并配置路由表
