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




