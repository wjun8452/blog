iVolleyball
##版本历史
* 2019/3/31
 * v3.3 大记分牌增加帮助页面。 (v4.0联网版本始终没有很好的设计，无法开发下去。决定基于v3.2上重新思考改进计划。）
 * v3.4 转位和分数独立设计，以便快速调整场上位置和比分。从技术统计页面快速切换到记分牌页面，方便公布分数。记分牌页面的操作也会影响技术统计页面的转位。减分操作视为回退。
 * v3.5 改进技术统计页面UI设计，弃用平铺式按钮，采用渐进引导式菜单。增加统计项目，完善统计报表页面。



##开发日志
* 2019/3/31
 *  make a release branch based on v3.2 production version. 
 *  make master as the same as v3.2.
 *  make a feature branch to develop v4.0.
 *  add project.config.json to be compatable with current wx SDK. 
* 2019/4/22 ~ 23
 * v3.4 体验版提交
* 2019/4/27 v3.4 提交审核
* 2019/4/28 统计项目的添加要再整理一下

##遇到的问题
 *  <template is="block" data="{{court_data.players, wxml报错。
 
 > 改为 data="{{court_data}}"，在block模板里边提取court\_data.players。  
 *  小程序的model和各个page的data之间的关系，如何做到不冗余？
 >  整个应用只有一个数据data, data包括court核心数据和page显示数据， 都从storage读出来，供page使用，page退出时存入storage。领域模型court.js只提供操作数据的方法，不存储数据。
 *  上下滑动调整分数时，整个记分牌在滚动
 > 重写catchtouchmove阻止事件传递即可解。


##技术设计



##资料备忘
* [小程序后台管理登录官网](https://www.baidu.com/link?url=DuxXY5RsJFcLbBph98MrzsMQGqSuMHZONFA5u7NQQErQ2R_WfdlQEXtmmkVbE5Pd&wd=&eqid=d016a72500127c27000000035ca0c74d)
* [小程序API文档](https://developers.weixin.qq.com/miniprogram/dev/api/)
* [颜色表](http://www.w3school.com.cn/cssref/css_colors.asp)
* wjun_8452@163.com wjun8452 又注册了一个账号为将来开发小游戏用