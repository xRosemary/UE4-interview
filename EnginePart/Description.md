### UE中行为树的节点有哪些？
  Selector、Sequence和SimpleParallel
  简单地说Selector就像if-else if语句，从左往右执行一系列节点，有一个节点执行成功就不往下执行，
  而Sequence是在有节点执行失败时就不往下执行了。
  Selector、Sequence和SimpleParallel属于Composites，类似于编程中的流程控制语句，还有一类节点属于Tasks，是实际执行的动作。
  |  节点类型   | 说明  |
  |  ----  | ----  |
  | 合成节点  | 此类节点定义分支的根以及执行该分支的基本规则。 |
  | 任务节点  | 此类节点是行为树的叶。它们是可执行的操作，没有输出连接。 |
  | 装饰器节点  | 也称为条件。它们连接到另一节点，并决定树中的分支、甚至单个节点能否被执行。 |
  | 服务节点  | 此类节点附接至合成节点，而且只要其分支正在执行，它们就会按照定义的频率执行。它们通常用于检查和更新黑板。它们取代了其他行为树系统中的传统并行节点。 |
  
  https://docs.unrealengine.com/4.27/zh-CN/InteractiveExperiences/ArtificialIntelligence/
 
### UE的网络同步怎么实现的？
### 移动同步如果想尽可能降低流量，该怎么做？
### 场景中有许多物体，如何判断玩家与他们的碰撞？
### 给定两个球的位置和速度，判断他们是否会碰撞？
### 有没有了解过MVC模式？
### 一个8 × 8km的地图，用ue的level streaming加载，有没有什么优化？
### ActorComponent、SensingComponent、PrimitiveComponent在成员方面有什么区别？
### 属性同步和RPC的区别、速度比较

### UE网络同步用什么协议？

  TCP连接的优点是可靠稳定，但速度慢这个缺点导致它并不适合网游。
  但UE也并未照搬UDP连接方案，而是在这个基础上融合了TCP的优点，例如加入了乱序处理，以及对reliable的包丢失重传。
  可谓是各取所优，既保证了连接速度，也保证了可靠性。
### TCP比UDP慢在哪里？
### UE对static_cast的修改是什么？为什么这么修改？
