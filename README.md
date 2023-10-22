# InterestingFunctions（有趣的轮子）


##### 1.MultiWindows是类似那种窗口切换的游戏demo（自己想的，可能不太对），不过unity的导包有时候会丢失tag和layer的信息，所以下次要用还得重新调参。。 
###### 原理：1.相机的ViewPort到Scene的映射，相机的拖拽（select+记录刚开始的偏移量），相机被拖拽时更改覆盖关系（改depth），Player碰到某个相机的collider就改变player的碰撞layer（详情看package）
##### 2.RandomlySpawnEnemyOnThePlatform在横版平台正上方上随机生成敌人，也可以用于像是Terraria那种传送的暗黑法师也行。
###### 原理：在player的一定范围向下发出射线。把hit.point向上偏移epsilon，再判断是否还在hit.collider里来决定是否生成Enemy（因为可能会Random到collider里面）
##### 3.IsBehindShadowCheck判断玩家是否在阴影下，在伏击类和躲避类的游戏中较为常见
###### 原理：在一个点向以player.transform.position为圆心的圆形上投射等角射线（射线数量决定检测精度），首尾两条射线跟圆相切，判断射线跟player的collider是否有碰撞即可，难点是计算角度和旋转向量，还有各种小细节。
