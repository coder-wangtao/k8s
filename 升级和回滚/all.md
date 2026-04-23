在 Kubernetes 中，Pod 通常不直接更新，而是通过 控制器（Deployment、StatefulSet、DaemonSet 等）管理，来实现升级和回滚。原因：
Pod 是不可变的对象，一旦创建就不会直接修改镜像或配置
更新 Pod 的方式是 新建副本、替换旧 Pod
所以 升级和回滚操作通常在 Deployment 上进行。
