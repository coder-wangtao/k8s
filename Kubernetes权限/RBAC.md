RBAC：基于角色（Role）和角色绑定（RoleBinding/ClusterRoleBinding）

| 名称                   | 作用                                                                  |
| ---------------------- | --------------------------------------------------------------------- |
| **Role**               | 定义某个 Namespace 内的权限规则（资源 + 操作）                        |
| **ClusterRole**        | 定义集群级别的权限规则，可以跨 Namespace 使用                         |
| **RoleBinding**        | 将一个 **Role** 绑定给用户/组/ServiceAccount，只在某个 Namespace 生效 |
| **ClusterRoleBinding** | 将 **ClusterRole** 绑定给用户/组/ServiceAccount，作用于整个集群       |
