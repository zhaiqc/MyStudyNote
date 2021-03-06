## #寻宝项目架构

*   索引
    *   [一. 前言](#1)
    *   [二. 为什么要有架构](#2)
    *   [三. 怎么实现架构](#3)
    *   [四. 我们将使用的架构](#4)

## 一. 前言

在设计中，会存在一些险恶的问题，就是那种只有通过解决或部分解决才能被明确的问题（也就是做了，出现了问题，才发现的问题）；

最引人注目的例子就是塔科马海峡吊桥（Tacoma Narrows Bridge）的设计问题。

设计这座桥梁时考虑的主要问题是它是否足够结实，而一场狂风最终使得大桥最终坍塌；

![](http://7xsct4.com1.z0.glb.clouddn.com/16-4-15/1295659.jpg)

这就是一个险恶问题的例子，因为直到这座桥的坍塌，才使得工程师们知道还应该充分考虑空气动力学的问题；

在软件设计过程中，你会有很多错误的步骤，你会犯很多的错误，但是犯错也是设计的关键所在；

## 二. 为什么要有架构

我们举一个例子来说，如下图中，把一个系统划分成六个子系统。

![](http://7xsct4.com1.z0.glb.clouddn.com/16-4-15/14890479.jpg)

在没有定义任何规则时，没有对子系统间的通信加入任何限制，那第它们之间的通信就会肆意地发生；

导致的结果，如下图：

![](http://7xsct4.com1.z0.glb.clouddn.com/16-4-15/53825081.jpg)

在加入若干通信规则后，子系统之间的交互得以显著地简化，结构也明显更清晰

![](http://7xsct4.com1.z0.glb.clouddn.com/16-4-15/75321341.jpg)

为了让整个系统的各子系统，及之间连接更简单易懂且易于扩展维护，就要尽量简化、统一子系统之间的交互关系。当然这也就是软件开发中我们要去做的架构设计。

## 三. 怎么实现架构

### 1\. 架构的总体质量

*   架构是否解决了全部需求？
*   有没有哪个部分是过度架构或欠架构
*   顶层设计是否独立于所用的平台？
*   作为一个用该系统的程序员，使用这个架构感觉是否良好？

### 2\. 时间安排

花费在问题定义、需求分析、软件架构上的时间，依据项目的需要而变化。一般来说，这些前期计划方面投入10%~20%的工作量和20%~30%的时间。当然，这些数字不包括详细设计的时间（那是构建活动的一部分）。

> 题外话：
> 
> 中小型公司很有可能需要你自己解决需求对接方面的问题，你应该要预留足够的时间，将需求定义足够清晰，让需求的不稳定性对构建活动（详细设计实现）的负面影响降至最低。
> 
> 一定避免出现类似这种问题：
> 
> 老板或客户要你给做一个门。
> 
> 你按一般门的规格要求，报价，做好了你的产品。
> 
> 老板或客户验收说：“为什么不要黄花梨材质的？为什么不带感应系统，自开自关？
> 
> 你："我去！"
> 
> 如果有人请你建一栋房子。客户问你：“完成这项工作要花多少钱？” 你会合理地询问：“你想要我做什么？” 客户说：“我不能告诉你，不过我想知道要花多少钱？” 你该明智地感谢他学浪费了你的时间，然后转身回家。

### 3\. 架构构建实现

好的设计具有很多常见的特征，如下：

#### 易于维护

设计时为维护工作着想，时刻想着运维人员可能会就你的软件而提出的问题。

#### 松散耦合

设计时让程序的各个组成部分之间关联最小。通过合理抽象、封装等原则设计出相互关联尽可能最少的类。减少关联也就减少了集成、测试和维护时的工作量

#### 可扩展性

设计时要考虑到当要增强系统功能时，无须破坏其底层结构。你可以改到系统的某一部分而不会影响到其他部分。越是可能发生的改动，越不会给系统造成破坏。

#### 可重用性

所设计的系统的组成部分能在其他系统中重复使用

#### 可移植性

所设计的系统能很方便的移植到其他的环境中

#### 标准技术

尽量用标准化的、常用的方法 ，让整个系统给人一种熟悉的感觉。一个系统依赖的外来的、古怪的东西越多，别人在第一次想要理解使用它时就越头疼。

#### 层次性

尽量保持系统各个分解层的层次性，全你能在任意的层面上观察系统，并得到一致性的看法。设计出来的系统应该能在任意层次上观察而不需要进入其他层次

需要在一个软件系统中的若干不同细节层次上进行设计，可参考以下方案：

![](http://7xsct4.com1.z0.glb.clouddn.com/16-4-15/54246749.jpg)

## 四. 我们将使用的架构

### 1\. 为什么我们要架构？

> 题外话：（摘自“代码大全）
> 
> 避免创建无所不知，无所不能的上帝类、神类。
> 
> 如果一个类需要花费时间从其他类中通过Get()和Set()检索数据（也就是说，需要深入业务并且告诉它们如何去做），所以是否应该把这些功能函数更好的组织到其它类而不是上帝类中。

上帝类的维护成本很高，你很难理解正在进行的操作，并且难以测试和扩展，这就是为什么要避免创建上帝类的黄金法则。

然而！ 大家想想在Android开发中，如果你不考虑架构的话，你的Activity类！！！。

在Android中，允许View和其它线程共存于Activity内，还有更大的问题莫过于在Activity中同时存在业务逻辑和UI逻辑。这将会增加测试和维护的成本。

Activity是上帝类（没有架构时）！这是为什么我们需要一个清晰架构的重要原因！MVP架构模式将是一个很好的选择！

> 题外话：
> 
> MVC，MVP 哪一个才是最好的呢？哪一个比其他的更优秀呢？只能选择一个？
> 
> 不是！没有万能药！
> 
> 架构模式有很多，MVP也只是架构模式之一，它们也可以协同使用，同样，也可以有选择的用于不同项目。
> 
> 这些架构模式只是方法、手段而不是目的、目标。
> 
> MVC，MVP架构模式的动机都是一样的：如何使得层次结构清晰全理，避免复杂混乱的代码，让执行单元测试变得容易，创造高质量应用程序。

### 2\. 我们将使用的架构 - MVP

MVP架构模式是一种进化版本的MVC，MVP代表Model，View和Presenter。

![](http://7xsct4.com1.z0.glb.clouddn.com/16-4-26/97198422.jpg)

MVP架构模式中,View接收事件,根据需要调用Presenter做业务逻辑, Presenter再负责更新视图及数据模型。

*   View层负责处理用户事件和视图展示 （Activity或者Fragment）
*   Presenter层负责做业务逻辑和上下层(V和M)的协作、适配，主要起到了解耦作用
*   Model层是数据的接口负责数据模型

![](http://7xsct4.com1.z0.glb.clouddn.com/16-4-27/3193338.jpg)

![](http://7xsct4.com1.z0.glb.clouddn.com/16-5-15/23544518.jpg)

> 题外话：
> 
> 使用MVP架构简单，但要自己做一个真正的MVP架构还是有一定难度的；关键是，高层接口不知道底层接口的细节，或者更准确地说，高层接口不能，不应该，并且必须不了解底层接口的细节，是（面向）抽象的，并且是细节隐藏的。
> 
> 而我们的目标是：理解架构，掌握MVP架构的使用，了解MVP架构的实现原理