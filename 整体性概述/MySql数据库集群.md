### MySql数据库集群

1. 首先对于想要实现Mysql数据库集群，有两种实现的方法：**PXC**，**Replication**。这里选择性能更好的**PXC**来搭建数据库集群。
2. 创建五个节点来作为数据库集群的数据库存储。
3. 使用**Haproxy**来对**MySql**数据库集群实现负载均衡处理。就可以使用到Haproxy来实现一个端口映射到后端的数据库集群上，防止所有的数据都打在同一个数据库上出现宕机的情况。
4. 但是对于仅有的一个**Haproxy**，若是出现了问题，就会导致功亏一篑，因为此时就不可能再对数据库集群进行访问，所以就需要设置两个Haproxy，来实现双机热备。
5. 使用到**Keepalived**技术，在两个Haproxy容器内部安装**Keepalived**，实现两个Haproxy争抢一个虚拟ip。
6. 然后再在宿主机上安装keepalived，实现双机热备。

以上就是对于使用Docker配置MySql数据库集群的整体框架，具体的文章参见[搭建Mysql数据库集群](https://blog.csdn.net/weixin_44015043/article/details/105801682)，
具体的配置文件参见[具体配置文件](https://github.com/maycope/Docker-front-and-back-project-deployment-/tree/master/PXC集群)。其中的**h1** 表示*Haproxy1*，**h2**表示*Haproxy2*。宿主机表示在主机上的**keepalived**配置，实现双机热备。

