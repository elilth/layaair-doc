## LayaAir的组件化开发

> Author: charley            updated date: 2020-11-17

其实LayaAir 2.0在发布的时候就讲过，相对于1.0引擎，对于组件化开发的支持，是2.0引擎与IDE非常重要的新特性之一。然而，直到今天，还是有一些开发者对LayaAir引擎的组件化开发不是太理解。本篇简单的对LayaAir组件化开发进行一些介绍。

### 一、什么是组件化开发

对于组件化开发，其实有很多不同的理解，这里我阐述一下我的理解，希望对大家有用。

只要是有一些工作经验的程序员，基本上都会遇到重构，或者接手维护他人的项目代码。碰到耦合度高的代码，将是一件非常痛苦的事，一旦产生重构需求，将会感到重构困难。并且在维护时，可能为了改某处的BUG，刚刚修复好，又激发了另一处新的BUG，导致各种维护困难。

而组件化开发，恰恰就能减轻以上种种痛苦。

因为，组件化开发的核心思想是解藕与**单一职责** 。

我们先从字面上去理解一下组件化，组是可组合，件是单体，即是可独立。所以，组件化的设计思想就是一定不能与其它模块耦合，因为耦合了就很难独立出来。

如果说解耦是组件化开发的核心设计思想，那单一职责就是为达到这个核心设计思想的指导性方法。

当一个类的职责多了，就难免会产生耦合的可能，所以，尽可能让每个类的职责清晰和单一，就会避免耦合性。

通过LayaAirIDE创建的2D示例项目（打方块游戏）。也是组件化开发设计思想的一个示例，充分考虑了解藕和单一职责。比如，子弹的脚本，只负责自己的移除，回收，完全不需要去考虑碰到盒子，盒子要怎么办。盒子会有自己的脚本，去处理被子弹碰到后，盒子的碰撞反弹，降级，死亡爆炸等等。所以，无论场景中有多少个子弹，有多少个盒子，每一个子弹或者盒子的脚本，只对自己的所属节点负责。

理解完基础的组件化开发概念，那么下一步就是使用LayaAir引擎按组件化的设计思想进行开发。

### 二、脚本组件与生命周期

LayaAir引擎本身就提供了大量组件，例如UI组件、物理组件，同时我们也允许开发者为节点添加脚本组件，实现对节点的单独控制。

为了更好让脚本类管理好自己的所属节点，引擎也提供了大量的生命周期方法。

> 生命周期，即为从出生到死亡的一系列重要节点，例如，节点的激活，添加到舞台，每帧的刷新，碰撞，销毁等等。生命周期方法内的逻辑，遇到对应的条件时，就会自动执行。

#### 主线生命周期方法：

| 生命周期方法 | 简要说明                                                     |
| ------------ | ------------------------------------------------------------ |
| onAwake      | 组件被激活后执行，此时所有节点和组件均已创建完毕，此方法只会执行一次 |
| onEnable     | 组件被启用后执行，比如，节点被添加到舞台后执行               |
| onStart      | 在第1次执行update之前执行，只会执行一次，                    |
| onUpdate     | 每帧更新时执行，尽量不要在这里写大循环逻辑或者使用getComponent方法 |
| onLateUpdate | 每帧更新之后执行，尽量不要在这里写大循环逻辑或者使用getComponent方法 |
| onDisable    | 组件被禁用时执行，比如从节点从舞台移除后                     |
| onDestroy    | 手动调用节点销毁时执行                                       |
| onReset      | 重置组件参数到默认值，如果重写了这个函数，则组件会被重置并且自动回收到对象池，方便下次复用，没有重置则不进行回收复用。 |

除了上面这些，还有物理事件的生命周期、点击事件的生命周期、键盘事件的生命周期等等。

大家可以查看具体的API

https://layaair2.ldc2.layabox.com/api2/Chinese/index.html?version=2.9.0beta&type=Core&category=Component&class=laya.components.Script

### 三、Runtime与脚本的使用区别

LayaAir的组件化开发，核心就是Runtime类与Script（脚本组件）类的合理运用，生命周期方法的使用。

有不少开发者对IDE中的Runtime类和脚本组件类的区别不是太理解。

Runtime类，其实就是UI继承类。

UI继承类又分成两大种，一种是场景继承类，另一种是UI组件继承类。

场景继承类，由于继承了整个场景，对于整个场景的节点查找与节点控制更为方便，所以，场景类通常的作用是管理者角色，负责当前场景的全局显示调控，不需要干具体游戏逻辑的活。

而场景的脚本，在分工方面，尽量不去处理显示相关，显示控制直接交给场景继承类去协调。场景的脚本主要是负责逻辑调控。是逻辑控制器的角色。具体干活的都是节点脚本。每一个节点脚本负责各自节点的行为控制，在这些节点脚本里，无需耦合，只管好自己，做好自己的业务逻辑处理就行了。完全是单一职能的设计思想。

组件继承类，通常是用于通用的组件显示效果。与负责真正项目业务逻辑的节点脚本不同，组件继承类是对UI组件本身能力的拓展补充，是通用的组件显示效果实现，例如，按钮在点击的时候，全都要实现一种点击缩放效果。那么就可以写一个继承了按钮的Runtime类，在这个类里去实现点击缩放。当绑定给按钮的Runtime上之后，那所有绑定了该继承类的节点，都会具有这个缩放效果。虽然他是给多个节点用的，但他继承于组件和对组件的扩展，本质上是对组件功能的丰富，脱离了产品具体的业务逻辑关联，也符合解耦与单一职责思想。

所以，只有清晰的了解引擎的功能，才能做到职责清晰。

##### 总结一下，

场景的Runtime类，职责是对于整个场景显示的全局控制，比如全局开始与结束的显示，全局积分的改变等等。

场景的脚本类，职责是场景中全部的逻辑控制，比如玩家点了开始，场景继承类中侦听这个点击操作，不是立即要开始游戏，而是要通知场景的脚本类，游戏开始了，场景的控制脚本才有权决定游戏要不要开始，什么逻辑下开始，下一步由谁出场、出场位置等等。

节点的脚本类，负责具体的逻辑执行，一旦游戏的角色和NPC在场景中出现后，具体的攻击与伤害等等，都是各自负责处理，不要都堆到场景类中。比如方块受重力掉落，什么情况下反弹，什么情况下碎裂，这是由方块的脚本根据自己的碰撞反馈进行处理的，场景控制脚本无需关心。只有方块的逻辑脚本里，判断自己碰到了地板，才需要通知场景控制脚本：游戏结束了。场景控制脚本再去通知场景继承类：游戏结束了，把结束面板弹出来吧。

所以，清楚了解各自的职能，分工明确，职责单一，就可以实现解耦的组件化开发。

用好LayaAir 2.0引擎组件化开发，开发效率与维护效率都会提升很多，代码结构也会变得更加清晰易懂。

如果大家看完本文，还是不太理解，

也欢迎阅读更加直观的视频教学视频

##### 组件化开发的入门基础讲解视频：

https://ke.qq.com/course/427324

##### 2D组件化实战课视频：

https://ke.qq.com/course/2646524


