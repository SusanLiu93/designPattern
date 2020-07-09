## 设计模式比较及练习
### 什么是设计模式及遵循的原则
- 设计模式：一种简单的解决方案；主要解决软件开发过程中遇到的问题。
- 遵循的原则：找出程序中变化的部分，然后将其封装起来。
#### 单例模式
- 概述：确保一个类只有一个实例，在JavaScript（ES5）中没有类这个说法，创建对象的方法很简单，即{}
- 惰性单例模式：在需要的时候创建单例（参照最后一个实现）
- 单例模式思想：创建对象和管理单例的实现分布在两个方法中
- 用到JavaScript特性：闭包和高阶函数
#### 策略模式
- 概述：定义一些算法，封装成策略类；当客户对context发起请求的时候，context总是将这些请求
  委托给这些策略对象中的某一个进行计算
- 优点：
    - 利用组合，委托，多态等思想，可以避免多重条件选择语句
    - 对开放-封闭规则的完美支持，将算法封装在策略类中，便于扩展和理解
    - 复用性
    - 利用组合和委托来让 Context 拥有执行算法的能力，这也是继承的一种更轻便的替代方案
- 缺点：
    - 会在程序中增加许多策略类或策略对象
    - 需要提前了解所有的策略
#### 迭代器模式
- 概述:提供一种顺序访问聚合对象的各个元素，同时又不需要暴露该对象的内部表示。
- 类别:内部迭代器和外部迭代器；
- 内部迭代器：已经定义好了迭代规则，只需要一次调用即可
- 外部迭代器：必须显示的请求下一个元素

#### 发布订阅模式（观察者模式）
- 概述：定义对象之间的一对多关系，当一个对象的状态发送改变，所有依赖它的对象都将得到通知；
- 优点:
    - 取代对象之间硬编码的通信机制；对象之间松耦合的联系在一起；
    - 应用于异步编程，替代传递回调函数的一种方案；
    - 时间和对象上的解耦；
- 缺点
    - 内存的消耗，首先创建订阅者需要内存，其次当订阅者订阅一个消息时，也许消息最后都未发生，订阅者一直存在
    - 发布订阅虽然弱化了对象之间的联系，如果过度，这样会导致对象之间的关系被深埋，导致程序难以跟踪
- 实现步骤：
    - 指定发布者
    - 给发布者添加缓存列表，用于存放回调函数以便通知订阅者
    - 最后发布消息的时候，发布者会遍历缓存列表，依次触发里面的订阅者回调函数
#### 命令模式
- 概述:执行某些特定事情的指令，以一种松耦合的方式消除请求接受者和请求发送者之间的关系；
- 命令模式将过程式的请求封装在command 对象的excuse里，通过封装方法调用，把运算块包装成形；
- command对象可以四处传递，不再关注过程。
- 命令模式的接受者被当做command的属性保存起来，同时约定执行命令的操作是调用command.excuse方法；

#### 组合模式
- 宏命令：包含一组子命令的对象，宏命令和子命令都有excuse属性
- 概述：将对象组合成树形结构，表示‘部分-整体’的层次结构；
- 优点：
    - 多态性，使得单个和组合对象的使用具有一致性，忽略组合对象和单个对象的不同；
    - 提供一种遍历树形结构的方案；组合对象的 execute 方法，程序会递归调用组合对象下 面的叶对象的 execute 方法。
请求遵循逻辑：请求从树最顶端的对象往下传递，如果当前处理请求的对象是叶对象(普通 子命令)，叶对象自身会对请求作出相应的处理（调用excuse）;如果当前处理请求的对象是组合对象(宏命令)， 组合对象则会遍历它属下的子节点，将请求继续传递给这些子节点
- 缺点：透明性带来的程序健壮性，误操作
- 注意事项：
    - 组合模式不是父子关系，组合对象和单个对象之间具有相同的接口（如excuse）
    - 叶对象除了具有相同的接口外，对叶对象的操作还具有一致性
    - 用职责链模式提高组合模式性能；（但在组合模式中，父对 象和子对象之间实际上形成了天然的职责链。让请求顺着链条从父对象往子对象传递，或者是反 过来从子对象往父对象传递，直到遇到可以处理该请求的对象为止，这也是职责链模式的经典运 用场景之一）
    - 双向映射关系（待补充）
- 组合模式使用场景：
    - 希望统一对待所有的对象；
    - 部分-整体层次结构（扫描文件夹）
#### 模板方法模式
- 概述：模板方法只需要使用继承便可实现（依赖抽象类）；
- 组成：
    - 抽象的父类：封装了一些子类的算法框架、指导子类以何种顺序去执行方法
    - 具体的子类：继承父类，也就拥有了父类定义的算法框架和公共方法等，同时也可以重写父类；
- 特点：
    - 子类实现中的相同部分上移到父类中，而不同部分留给子类实现，体现了泛化思想；
    - 好莱坞原则：高层调用底层组件，父类通知子类什么时候去调用，子类放弃控制权，作为子类，只提供设计上的细节；
        - 好莱坞原则应用：
            - 发布-订阅模式；
            - 回调
- 真的需要继承吗？不是，可以通过高阶函数实现
#### 享元模式
- 概述：运用共享技术来有效支持大量细粒度的对象，目标在于减少共享对象的数量；
- 内部状态和外部状态：对象的属性
    - 内部状态存储于对象内部，用于对象共享，经常改变，独立于场景
    - 外部状态取决于场景，不可以被共享，经常变换
- 通常来说，内部状态有多少种，就有多少个对象
- 适用性：
    - 很好的性能优化方案
    - 同时也会带来代码的复杂性问题
- 何时使用
    - 一个程序中使用了大量的类似对象
    - 对象的大多数状态可以变为外部状态
    - 剥离出大量的外部状态外，可以用较少的共享状态取代大量的对象
- 职责链模式:
    - 概述：使多个对象都有机会处理请求，避免了请求发送者和接受者之间的耦合关系；将这些对象连成一条链，沿着这条链传递请求，直到有一个对象可以处理。
    - 例子：公交车上传递车票，如果你上车位置不是紧挨着售票员，就得将车票从离你最近的开始传递，直到传给售票员
    - 优缺点：
        - 优点：
            - 解耦了请求发送者和处理者之间的关系
            - 可以手动指定起始节点，减少请求在链中传递次数
        - 缺点：
            - 不能保证请求被链中节点处理
            - 程序中多了许多节点，性能损耗


