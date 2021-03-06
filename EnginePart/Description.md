### UE中行为树的节点有哪些？
  ( https://docs.unrealengine.com/4.27/zh-CN/InteractiveExperiences/ArtificialIntelligence/)
  ```
  Selector、Sequence和SimpleParallel
  简单地说Selector就像if-else if语句，从左往右执行一系列节点，有一个节点执行成功就不往下执行，
  而Sequence是在有节点执行失败时就不往下执行了。
  Selector、Sequence和SimpleParallel属于Composites，类似于编程中的流程控制语句，还有一类节点属于Tasks，是实际执行的动作。
  ```
  |  节点类型   | 说明  |
  |  ----  | ----  |
  | 合成节点  | 此类节点定义分支的根以及执行该分支的基本规则。 |
  | 任务节点  | 此类节点是行为树的叶。它们是可执行的操作，没有输出连接。 |
  | 装饰器节点  | 也称为条件。它们连接到另一节点，并决定树中的分支、甚至单个节点能否被执行。 |
  | 服务节点  | 此类节点附接至合成节点，而且只要其分支正在执行，它们就会按照定义的频率执行。它们通常用于检查和更新黑板。它们取代了其他行为树系统中的传统并行节点。 |
  
### UE4多人联机模型
  ```
  虚幻引擎使用 客户端-服务器 模型。
  网络中的一台计算机作为 **服务器** 主持多人游戏会话，而所有其他玩家的计算机作为 **客户端** 连接到该服务器。
  然后，服务器与连接的客户端分享游戏状态信息，并提供一种客户端之间通信的方法。
  ```

### UE的网络同步怎么实现的？
  ```
  我们给一个Actor类的同步属性A做上标记Replicates（先不考虑其他的宏），
  然后UClass会将所有需要同步的属性保存到ClassReps列表里面，这样我们就
  可以通过这个Actor的UClass获取这个Actor上所有需要同步的属性，当这个
  Actor实例化一个可以同步的对象并开始创建对应的同步通道时，我们就需要准
  备属性同步了。

  1. 首先，我们要有一个同步属性列表来记录当前这个类有哪些属性需要同步（FRepLayout，每个对象有一个，从UClass里面初始化）；
  2. 其次，我们需要针对每个对象保存一个缓存数据，来及时的与发生改变的Actor属性作比较，从而判断与上一次同步前是否发生变化（FRepState，里面有一个Staticbuff来保存）；
  3. 然后，我们要有一个属性变化跟踪器记录所有发生改变同步属性的序号（可能是因为节省内存开销等原因所以不是保存这个属性），便于发送同步数据时处理（FRepChangedPropertyTracker，对各个Connection可见，被各个Connection的Repstate保存一个共享指针）。
  4. 最后，我们还需要针对每个连接的每个对象有一个控制前面这些数据的执行者（FObjectReplicator）。
  ```
  
### 移动同步如果想尽可能降低流量，该怎么做？

### 属性同步和RPC的区别、速度比较

### UE网络同步用什么协议？
  ```
  TCP连接的优点是可靠稳定，但速度慢这个缺点导致它并不适合网游。
  但UE也并未照搬UDP连接方案，而是在这个基础上融合了TCP的优点，例如加入了乱序处理，以及对reliable的包丢失重传。
  可谓是各取所优，既保证了连接速度，也保证了可靠性。
  ```
### TCP比UDP慢在哪里？
  ```
  UDP没有TCP的握手、确认、窗口、重传、拥塞控制等机制，UDP是一个无状态的传输协议，所以它在传递数据时非常快。
  1. 基于连接与无连接
  2. 对系统资源的要求（TCP较多，UDP少）
  3. UDP程序结构较简单
  4. 流模式与数据报模式
  5. TCP保证数据正确性，UDP可能丢包，TCP保证数据顺序，UDP不保证另外结合GPRS网络的情况具体的谈一下他们的区别：
  6. TCP传输存在一定的延时，大概是1600MS（移动提供），UDP响应速度稍微快一些。
  ```
  
### UE对static_cast的修改是什么？为什么这么修改？
### 场景中有许多物体，如何判断玩家与他们的碰撞？
### 给定两个球的位置和速度，判断他们是否会碰撞？
### 有没有了解过MVC模式？
### 一个8 × 8km的地图，用ue的level streaming加载，有没有什么优化？
### ActorComponent、SensingComponent、PrimitiveComponent在成员方面有什么区别？
