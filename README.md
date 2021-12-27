##  ZOOKEEPER

### IMAGE目录
```
1.  IMAGE/ZOOKEEPER理论.jpg
2.  IMAGE/ZOOKEEPER理论.pos
3.  主要是跟着视频推理分布式中的难点概念
```
### 周边知识点
```
1.  CAP定理
2.  BASE定理
3.  PAXOS论文
4.  分布式锁
```

原语：一般是指由若干条指令组成的程序段，用来实现某个特定功能，在执行过程中不可被中断
     原语是操作系统核心
     原语一旦开始执行，就要连续执行完，不允许中断

        组成：若干条指令 
        属性：一个过程
        作用：实现进程的通信和控制

zookeeper中有2中状态：
    可用
    不可用

每个客户端连接zk的时候，都会生成一个session来代表client


zk端口：
    2181： zk client 连接server
    2888:  对等server用于互相通信
    3888： 用于leader选举


zookeeper 集群分布式存在的问题解决方案    ： -s


zookeeper 安装：
 node01~node04
 
    1. 安装jdk，并设置javahome*, node01:
    2. 下载zookeeper    zookeeper.apache.org
    3. tar xf zookeeper.*.tar.gz
    4. mkdir /opt/mashibing
    5. mv  zookeeper  /opt/mashibing
    6. vi /etc/profile       export ZOOKEEPER_HOME=/opt/mashibing/zookeeper-3.4.6       export PATH=$PATH:$ZOOKEEPER_HOME/bin
    7. cd zookeeper/conf
    8. cp zoo.sem*.cfg   zoo.cfg
    9. vi zoo.cfg     dataDir=     server.1=node01:2888:3888
    10. mkdir -p /var/mashibing/zk
    11. echo 1 >  /var/mashibing/zk/myid
    12. cd /opt  &&  scp -r ./mashibing/  node02:`pwd`
    13. node02~node04   创建 myid
    14. 启动顺序  1，2，3，4
    15. zkServer.sh   start-foregroundzkCli.sh   help
        ls /
        create  /ooxx  ""
        create -s /abc/aaa
        create -e /ooxx/xxoo
        create -s -e /ooxx/xoxo
        get /ooxxnetstat -natp | egrep  '(2888|3888)' 


   角色：
     leader
     follower
     observer

   攘其外必先安内

  Paxos ： 基于消息传递的一致性算法
  ZAB
     Zookeeper 客户端会随机的链接到 zookeeper 集群中的一个节点
     如果是读请求，就直接从当前节点中读取数据；
     如果是写请求，那么节点就会向 Leader 提交事务，Leader 接收到事务提交，会广播该事务，只要超过半数节点写入成功，该事务就会被提交
     
     
     1. leader将client 的request转化为proposal
     2. leader通过队列给follower发送proposal消息
     3. leader收到follower的半数以上ACK反馈
     4. leader向所有follower发送commit
     
  watch
  API
  callback
