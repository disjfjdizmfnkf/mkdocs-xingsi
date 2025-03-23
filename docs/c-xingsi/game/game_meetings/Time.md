## 零、前言

本文主要内容为对Unity Time类的讲解，包括Time.deltaTime、Time.fixedDeltaTime等，同时讲解了Unityd的时间逻辑，以及Time.timeScale的影响

## 一、Time.deltaTime

首先是最常用的Time.deltaTime
### 为什么要用
想要理解什么是TIme.deltaTime，就要先理解为什么要用它,
如果有以下代码

<img src='../../../../assets/xingsi/game/meeting/Time/image_1.png' loading='lazy'>

我们并没有给speed*Time.deltaTime,会有什么结果呢?

由于**Unity调用Update是根据帧率调用的**，也就是说，如果一个可以运行120fps游戏的电脑，1秒可以执行120次Update，而一个可以60fps运行游戏的电脑，1秒钟只能执行60次Update，结果就是帧率越高跑的越快，帧率越低跑的越慢，这并不是我们期望的，因为这不公平

### 是什么

Time.deltaTime就是用来解决这个问题的

Time.deltaTime是当前帧与上一帧两帧之间的间隔时间，由于场景变化等原因，每两帧之间的时间可能不同，deltaTime的值也会不同

<img src='../../../../assets/xingsi/game/meeting/Time/image_2.png' loading='lazy'>

 >注意：Time.deltaTime只是获取帧与帧之间的时间，改变Time.deltaTime的值并不能改变帧之间的时间，帧之间的时间是由硬件等多种因素决定的

### 如何起作用

我们考虑下图两种情况


<img src='../../../../assets/xingsi/game/meeting/Time/image_3.png' loading='lazy'>

假设一个3fps(上轴)，另一个为4fps(下轴)，那么就有其中dn为上轴的deltaTime，tn为下轴的deltaTime。

所以有d1+d2+d3=t1+t2+t3+t4=1秒，此时两边同时乘以speed，

就变为了(d1+d2+d3)speed=(t1+t2+t3+t4)speed

也就是说在相同的时间下，无论帧率多少，使用一个speed乘以deltaTime得到的结果相同

所以当我们乘以deltaTime之后，无论一秒内执行了多少次Update，得到的结果都相同(暂时这样理解)

<img src='../../../../assets/xingsi/game/meeting/Time/image_4.png' loading='lazy'>

## 二、Time.fixedDeltaTime

接下来是Time.fixedDeltaTime,该值可以在Editor->Project Setting->Time->Fixed Timestep设置

<img src='../../../../assets/xingsi/game/meeting/Time/image_5.png' loading='lazy'>

### 为什么要用

我们知道Update的更新是根据帧率进行调用的，但有时难免会出现帧率很低的情况，而物理模拟的更新又不能有太大的波动（例如：如果物理更新也是随帧率的话，会导致物理模拟的精确度随帧率波动而波动），所以物理模拟需要不随帧率影响的按照固定步长进行更新，因此有了Time.fixedDeltaTime和FixedUpdate

## 三、Time.time与Time.fixedTime

这两个API可以获取从游戏开始到现在的时间，Time.time是Time.deltaTime的累加，Time.fixedTime是Time.fixedDeltaTime的累加。

## 四、Time.maxinumDeltaTime

这个API可能几乎不会在脚本用到（我是没用过）。但它却是Unity时间逻辑的重要组成部分。

maxinumDeltaTime的作用是限制了Time.deltaTime的最大值。也就是说，如果某个时刻帧率很低（即两帧之间的间隔很长），Time.deltaTime的值相应的也会变得很大，其造成的结果如果用移动举例，就是人物会“闪现”移动。因为我们的逻辑一般为speed*Time.deltaTime来表示移动距离，这就有可能导致穿墙问题的发生。

所以为了限制Time.deltaTime的值，就有了maxinumDeltaTime,一般该值为0.3333，即一旦Time.deltaTime超过0.3333那么就会等于0.3333.

<img src='../../../../assets/xingsi/game/meeting/Time/image_6.png' loading='lazy'>


>再次声明：改变Time.deltaTime并不会改变两帧之间的实际时间，假设两帧之间本来为1秒，Time.deltaTime被改为为0.333秒，而实际上的时间为1秒

## 五、Unity的时间逻辑

### 总览

<img src='../../../../assets/xingsi/game/meeting/Time/image_7.png' loading='lazy'>

上图就为Unity的时间逻辑，我们将其拆分为上下两部分

### 上半部分

<img src='../../../../assets/xingsi/game/meeting/Time/image_8.png' loading='lazy'>

上半部分主要是如何计算Time.time，对deltaTime使用maxinumDeltaTime进行限制

### 下半部分

<img src='../../../../assets/xingsi/game/meeting/Time/image_9.png' loading='lazy'>

下半部分的重点在于中间的循环，即Time.fixedTime对Time.time的追赶。

由上图我们就可以知道为什么有时会说执行一次Update()时可能会执行多次FixedUpdate()

原因就是deltaTime大于fixedDeltaTime,即帧率很低的时候，可能增加多次fixedDeltaTime,执行多次FixedUpdate(),才能走出循环执行一次Update()

但是，我们都知道，由于maxinumDeltaTime的限制，导致deltaTime会舍弃掉大于maxinumDeltaTime的部分。

由于这个机制导致了FixedUpdate()的执行次数并不会过多，因为间接舍弃了大于maxinumDeltaTime的部分的物理更新

## 六、Time.timeScale

如果大家要实现一些与时间有关的玩法，那么Time.scale是一个十分重要的工具，但是Time.scale并不会影响所有的时间。

哪些部分是受到Time.scale的影响，哪些不受其影响？这是我们接下来要讨论的话题

### Time.timeScale影响的

Time.timeScale直接影响Time.deltaTime，它们之间的关系为 Time.deltaTime = 实际时间间隔 × Time.timeScale

根据前面的介绍，我们可以知道，如果Time.deltaTime受到影响

- Time.time由于是Time.deltaTime的累加结果，也会受到Time.timeScale影响

- Time.fixedTime由于循环的存在，间接受到Time.deltaTime的影响，就也会受到Time.timeScale的影响

- FixedUpdate()的执行,与Time.fixedTIme相同，都是循环体内的部分


>也就是说，当我们让Time.timeScale=0，Time.time不再累加，Time.fixedTime不再累加，FixedUpdate()不再执行

 
### 不受Time.timeScale影响的


- Update():Update()的执行与帧率相关，与Time.timeScale无关


- Time.unscaledDeltaTime:与Time.deltaTime类似，区别如下

    1. Time.unscaledDeltaTime不受Time.timeScale的影响
  
    2. Time.unscaledDeltaTime不受Time.maxinumDeltaTime的限制


- Time.unscaledTime：Time.unscaledTime由Time.unscaledDeltaTime累加而来，不受TIme.timeScale的影响


>Time.unscaledTime与Time.time的比较建议看  [Important Classes - Time - Unity 手册](https://docs.unity.cn/cn/2023.2/Manual/TimeFrameManagement.html)的，有图有表比较清晰

## 七、FixedUpdate()、Update()、LateUpdate()

- FixedUpdate：调用 FixedUpdate 的频度常常超过 Update。如果帧率很低，可以每帧调用该函数多次；如果帧率很高，可能在帧之间完全不调用该函数。在 FixedUpdate 之后将立即进行所有物理计算和更新。在 FixedUpdate 内应用运动计算时，无需将值乘以 Time.deltaTime。这是因为 FixedUpdate 的调用基于可靠的计时器（独立于帧率）。


- Update：每帧调用一次 Update。这是用于帧更新的主要函数。


- LateUpdate：每帧调用一次 LateUpdate__（在 Update__ 完成后）。LateUpdate 开始时，在 Update 中执行的所有计算便已完成。LateUpdate 的常见用途是跟随第三人称摄像机。如果在 Update 内让角色移动和转向，可以在 LateUpdate 中执行所有摄像机移动和旋转计算。这样可以确保角色在摄像机跟踪其位置之前已完全移动。

## 引用与参考

  [Important Classes - Time - Unity 手册](https://docs.unity.cn/cn/2023.2/Manual/TimeFrameManagement.html)

  [详解Unity中Time类的用法与深入探究_unity time-CSDN博客](https://blog.csdn.net/weixin_43147385/article/details/127537231)