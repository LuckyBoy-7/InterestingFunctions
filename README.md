# InterestingFunctions（有趣的轮子）


##### 1.MultiWindows是类似那种窗口切换的游戏demo（自己想的，可能不太对），不过unity的导包有时候会丢失tag和layer的信息，所以下次要用还得重新调参。。 
###### 原理：1.相机的ViewPort到Scene的映射，相机的拖拽（select+记录刚开始的偏移量），相机被拖拽时更改覆盖关系（改depth），Player碰到某个相机的collider就改变player的碰撞layer（详情看package）
##### 2.RandomlySpawnEnemyOnThePlatform在横版平台正上方上随机生成敌人，也可以用于像是Terraria那种传送的暗黑法师也行。
###### 原理：在player的一定范围向下发出射线。把hit.point向上偏移epsilon，再判断是否还在hit.collider里来决定是否生成Enemy（因为可能会Random到collider里面）
##### 3.IsBehindShadowCheck判断玩家是否在阴影下，在伏击类和躲避类的游戏中较为常见
###### 原理：在一个点向以player.transform.position为圆心的圆形上投射等角射线（射线数量决定检测精度），首尾两条射线跟圆相切，判断射线跟player的collider是否有碰撞即可，难点是计算角度和旋转向量，还有各种小细节（比如射线只有1条时，计算过程中是不能除以（射线数 - 1）的，又比如10条射线，但只有9个间距（植树问题）等小细节）。
##### 4.DialogueTextEffect单纯实现了对话的文本, 可修改字体大小, 颜色, 一段字的特效(如上下浮动等), 但同一段字不方便换行, (还有各种还不理解的知识点, 以后补, 比如TMP.ForceMeshUpdate()之类的)
###### 原理: 用VerticalLayout排版每一行,在每一行(Clip)中加入若干word(textElement), 这样就可以单独控制某些单词, 用TMP.textInfo.meshInfo[0].vertices来改变位移, 用TMP.textInfo.meshInfo[0].colors32来改变透明度, 颜色和大小可以用<color=><size=>改, 但还是很简陋, 还有优化空间, 尤其是我根据effectType来添加对应的特效组件, 但不知道怎样调试后来添加的组件的属性, 如果写在一起又会有属性的冗余
##### 5.MeshAdsorptionWithCharTwist, 详情看代码, 灵感来自https://ldjam.com/events/ludum-dare/54/hope-falters(PS: 音乐不错), 主要功能是网格吸附和选中移动时字符抖动
###### 原理, 刚开始移动字符时, 根据刚开始选中的pos和移动后鼠标的pos来判断移动方向, 并记录左右或上下的cellNumber(不然不知道几个移动的时候不好判断), 确定好方向后,写两个方向的移动函数, 大概是这样(但还是有细节的? 至少我感觉是屎山), 字符的抖动就是控制字符移到父物体周围的一个点, 到了之后再选点, 周而复始, 
