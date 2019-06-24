iVolleyball

##总体规划
* 2018～2019， 微信小程序，吸引免费用户
 * v3 本地版，需求来自于排球爱好者。主打功能，全屏记分牌。设计原则是简单实用易操作。
 * v4 网络版，主打技术统计和个人成长陪同
   * v4.1 多人协作完成技术统计
   * v4.2 发布技术统计到公众号，推送订阅
* 2020，开发收费项目
 * v5 添加广告页面
 * v6 可添加视频

##需求细节
* v3
 * 计分牌，只需点击一个按钮就可以开始计分，避免复杂的UI设计，填写复杂的信息。
 * 计分达到25分会弹框显示保存页面，用户可以补填一些信息，譬如队名。
 * 如果没有网络，该记录会保存到本地，等到有网络的时候再上传。
 * 技术统计，排球爱好者通过技术统计积累经验，提高技术。
 * 易用性是最大的问题，一个人观看比赛同时统计是忙不过来的，有以下设计方式   
   1） 用户可以选择统计的项目和球员   
   2） 统计项目动态调整状态图，显示最可能需要统计的项目，隐藏其他项目？？
* v4
 * 分享，直播，用户可以点击一个分享按钮，分享计分牌给好友看，选择好友。好友微信收到一个邀请，点击链接进入该比赛的记分牌页面。好友无法更改比赛得分，但可以看到比赛得分的变化情况。
 * 好友打开链接之后，可以看到比赛的基本信息。好友可以在最近浏览中找到近期查看过的比赛信息。
比赛信息都是公开的
 * 小程序不提供查看所有比赛的功能。用户只能看到自己创建的比赛，和好友分享过来的比赛。
* 用户反馈机制
* 其他拾遗
 * 授权机制 

##版本历史
* v3.3 (2019/3/31) 大记分牌增加帮助页面。 (v4.0联网版本始终没有很好的设计，无法开发下去。决定基于v3.2上重新思考改进计划。）
* v3.4 (2019/4) 转位和分数独立设计，以便快速调整场上位置和比分。从技术统计页面快速切换到记分牌页面，方便公布分数。记分牌页面的操作也会影响技术统计页面的转位。减分操作视为回退。
* v3.5 (2019/5) 改进技术统计页面UI设计，弃用平铺式按钮，采用渐进引导式菜单。增加统计项目，完善统计报表页面。
* v3.6 (2019/5) 可设置允许统计的项目，或者允许统计的队员。
* v3.7, v3.7.1 (2019/5) 云端存储，技术报告分享好友
* v3.7.2 增加邀请好友组队功能


##遇到的问题
 *  <template is="block" data="{{court_data.players, wxml报错。

 > 改为 data="{{court_data}}"，在block模板里边提取court\_data.players。  
 *  小程序的model和各个page的data之间的关系，如何做到不冗余？
 >  整个应用只有一个数据data, data包括court核心数据和page显示数据， 都从storage读出来，供page使用，page退出时存入storage。领域模型court.js只提供操作数据的方法，不存储数据。
 *  上下滑动调整分数时，整个记分牌在滚动
 > 重写catchtouchmove阻止事件传递即可解。
 * 微信的登陆流程以及用户的id使用？
 > 为什么需要业务服务器存储code --> sessionKey, openID？
 > https://developers.weixin.qq.com/miniprogram/dev/api/api- 
 >  login.html#wxloginobject
 > https://www.cnblogs.com/thinkingthigh/p/7094492.html
 > login --> skey --> openId --> getUserInfoByOpenID
 * 用什么工具看node.js的代码？
 > webstorm
 * 如何获取某人的好友关系，这样可以只显示好友的记分牌。
 > 不行，微信小游戏才可以。
 * issue：为什么client显示的时间与db中看到的不一致？
 > 差八个小时
 * 页面之间跳转如何传递复杂的object呢？ （http://www.cnblogs.com/sese/p/9469699.html）
 > object转成string，然后encode，放到页面的url中传过去
 > 本地存储( var username = wx.getStorageSync('username'))，按这个套路，页面依赖于本地存储，不是很stateless。
 > 全局对象（var app = getApp();）
 > onfire.js， 本人觉得后三种本质都一样，不太好。
* 下面的checkbox不是unchecked的，为啥？

 ```
 <checkbox value="abc" checked="false"> abcdfd </checkbox>

 ```
 > 要改成这样才可以！！

 ```
 <checkbox value="abc" checked="{{false}}"> abcdfd </checkbox>

 ```
* 在wxml文件中不能调用javascript的函数.  
 > WXML + WXS, 参考 [如何在{{}}中使用函数？WXML+WXS](https://blog.csdn.net/weixin_39015132/article/details/82767312)

##技术设计


##资料备忘
* [小程序后台管理登录官网](https://mp.weixin.qq.com)
* [小程序API文档](https://developers.weixin.qq.com/miniprogram/dev/api/)
* [颜色表](http://www.w3school.com.cn/cssref/css_colors.asp)
* wjun_8452@163.com wjun8452 又注册了一个账号为将来开发小游用
* [数据库管理页面] (https://console.cloud.tencent.com/la) 
* 小程序登陆账号：723889224@qq.com wjun8452 
* 小程序名称：爱打排球, appID: wx573d66c4ffa25272 appSecret: b5f2b9fda872279ade75ac8c46b78dac 
* [本程序git地址](https://github.com/wjun8452/iVolleyball)
* [Wafer腾讯云开发SDK](https://github.com/tencentyun/wafer2-quickstart)
* [腾讯云开发](https://console.qcloud.com/lav2/dev)
* [小程序初始化配置文档](https://github.com/tencentyun/weapp-doc)
* 购买了一个月主机+域名：ivolleyball.xyz，购买页面：https://cloud.tencent.com/act/weapp，管理页面：https://console.cloud.tencent.com/domain，实名认证后可免费领取试用套餐：https://console.cloud.tencent.com/developer/auth?authType=personal，生产环境初始化页面：https://console.cloud.tencent.com/lav2/production/initial?psource=2017-activity-Weapp&fromSource=&from=&pid=11847&tld=.xyz
* [图标资源](http://www.iconfont.cn/home/index?spm=a313x.7781069.1998910419.2)
* [腾讯地图api key 6MWBZ-XDZL6-FPOSU-MKDSZ-DANKF-EOBRN] (http://lbs.qq.com/qqmap_wx_jssdk/index.html)
* [域名] (https://638537841.ivolleyball.xyz)
* [koa框架](https://koa.bootcss.com)
* [knexjs框架](https://knexjs.org)
* [广告平台，注册一个用户，使用它的SDK] (http://www.joyingmobi.com) 



## 统计项目

 编号 1 2 3 4 5 6 7 8 9
一传 R- Reception Error接球失误 DoubleTouch二次触球 Carry连击 Unplayable无法挽救 Bad Dig鱼跃失败 Touch Net触网 Under Net下网 Other其他 
 R0 Reception Overpass（过网） Poor(不到位） Good（到位） Excellent（非常到位）    
二传 S0 Set（传） Unrated（不评级） Poor(不到位） Good（到位） Excellent（非常到位）    
发球S S+ Serve Ace发球得分        
 S- Serve Error（发球失误） Long出界 Right Left Short Foot Fault Other  
 S0 Serve 发球破坏一传 发球一般      
进攻A A+ Kill（扣） Tip（轻吊） Medium hit（中等力量） Hard hit（大力） Tooled Block（打手） Back and Out（拦回出界） High Hands（超手） Perfect Place（落点） Opponent Error（对方失误）
 A- Hit Error（进攻失误） Ball in Net下网 Blocked被拦死 Into Antenna打标志杆 Touch Net触网 Other其他   
 A0 Hit No Score（扣） Tip（轻吊） Medium hit（中等力量） Hard hit（大力） Block Back（被拦回） Partial Block（部分打手）   
拦网 B+ Block（拦）        
 B- Block Error（拦网失误） Touch Net（触网） Under Net（卧果） Over Net（过网击球） Illegal Block（非法拦网） Other（其他）   
 B0  有效拦网       

 

 

 iOS版
iOS开发资料
swift语言：http://www.runoob.com/swift/swift-tutorial.html
2017-8-25 了解苹果开发和发布流程
个人开发者每年也需要花六百多块钱的, 所以先不发布，先看看能否在自己的手机上安装调试。http://blog.csdn.net/brucecheng22/article/details/50032817
XCode单步调试iphone7程序。有AppleID，添加设备到apple网站，在手机上信任开发者，就可以了。
XCode， Swift， iOS开发视频：http://open.163.com/movie/2015/2/L/C/MAIKHN60A_MAIKILOLC.html
2018/2/10
Development cannot be enabled while your device is locked.
点击 设置 --> 通用 --> 重置  --> 重置位置和隐私，然后关闭xcode 8, 拔掉数据线，重启xocde 8开启项目， 重新插上数据线，此时手机上会显示mac与手机设备的连接访问权限，选择“信任”，
王军的 iPhone is busy: Preparing debugger support for 王军的 iPhone
解决方法： 尝试重新拔插测试设备。 如果不起作用，重启Xcode尝试。如果不起作用，重启手机，然后尝试。（解决）。
复习一下
swift中的optional，如果变量可能为nil，则声明为var text: String?，?表示这是一个optional枚举，可能为nil，可能有值。var text: String则表明它不可能为nil。var text: String!表明该变量在使用的时候不用解包了。
创建了一个static lib，想写一写c++代码，但是不知道怎么用swift加载到UI中？
TODO：增加local storage
2018


Android UI库
https://github.com/wasabeef/awesome-android-ui

Implementation Design
微信小程序2017/4/8可以接受个人主体了
https://mp.weixin.qq.com/debug/wxadoc/dev/framework/config.html
Android native app开发
使用fragment的灵活性来实现速记模式中的队员卡片
模块
队员管理
统计

Android版本实现细节
mvp架构：参考：https://github.com/googlesamples/android-architecture/tree/todo-mvp/
Activity可否成为MVP中的V？为何例子中始终用Fragment作为V?
数据流的走向可以是：view–>presenter–>model–>presenter–>view,这种数据流一般出现的场景是用户在界面触发了一个事件的情形下
数据流的走向也可以是：model–>presenter–>view，这种数据流一般出现于比如通过长链接接收消息的场景。
一个activity搭建界面的基本框架，content frame根据抽屉菜单进行切换
使用抽屉菜单：DrawerLayout:抽屉菜单
数据存储：
Fragment中的saved state是干什么用的？
BasePresenter在model层注册为listener，何时应该注销呢？model层常常生命周期比P长，P比view更长。一个activity对应一个p。
使用浮动按钮：Floating action button：显示6个球员，每个球员周围有+，-两个按钮，点击动态弹出技术项目，并进行记分。
https://github.com/futuresimple/android-floating-action-button


Android版开发日志
2017/1/29 mvp应用，done
2017/1/29 抽屉菜单，done
2017/1/30 
抽屉菜单
增加PrepareActivity。准备阶段—记分板—比赛结束— 详细统计。
2017/1/31
了解屏幕自适应，使用layout_weight来比例化界面。
了解activity栈的管理，fix跳转的问题。
完善StatsAcitiviy，引入Gson持久化court，删除court，查找court
2017/2/1
技术统计表格，done
看到一个开源库：HelloCharts。将来可用它来做时间轴上的图表
2017/2/2
基本功能完备。
上传至git:https://github.com/wjun8452/volleyball
接下来使用云存储
2017/2/3 - 2017/2/4
选用腾讯云cos服务
为了避免文件名冲突，采用UUID命名
不能有多人同时编辑同一个文件，文件的中间修改过程只在本地发生，一旦保存到云端，则无法再修改。
git提交 V1.0
2017/2/6
重构model repository
2017/2/7
重构完成，提交git
2017/2/8
增加所有场次的技术统计。修正一些同步和保存的问题。


* 数据库设计   
 * vmatch 表（所有用户可读，仅创建者和管理员可写）
 * uuid
 * create_time 记分创建时间
 * openid 创建者的微信账号id
 * score1 第一个队得分
 * score2 第二个队得分
 * team1 第一个队的uuid
 * team2 第二个队的uuid
 * front_back_mode 前后排站位模式 true/false
 * place 比赛地址
 * city 比赛的城市（用户同城索引）
 * lat 比赛地址纬度
 * lon 比赛地址经度
 * board_id 比赛得分历史情况记录id
 * vboard表（场上站位及得分情况表）
 * uuid
 * team1_players  当前比分状态下，场上team1队员uuid数组，从1号位到6号位顺序排列
 * team2_players 当前比分状态下，场上team2队员uuid数组，从1号位到6号位顺序排列
 * team1_stat_items 第一个队历史得失分统计项，可以从此推算出最开始的站位
 * team2_stat_items 第二个队历史得失分统计项
 * serve_player 当前发球球员的uuid
 * serve team 为1表示team1发球
 * vteam表
 * uuid
 * name 队名
 * openid 创建者id
 * create_time 创建时间
 * players 成员uuid数组 ([0dafsdf,0sdfsdf,0dfsdf])
 * vplayer表
 * uuid
 * name 名字
 * openid 微信账号id
 * position1 擅长的位置1
 * position2 擅长的位置2
 * vpermission表
 * item_uuid 被分享的数据的uuid
 * all_can_view 是否对所有人可见
 * all_can_edit 是否对所有人可修
 * some_can_view 可见好友的openid数组
 * some_can_edit 可修改的好友openid数组
 * vaccount表 （微信openid到用户详细信息的关联表）
 * openid
 * user_info
 * create_time
 * update_time 上次更新时间
 * vstat表 （技术统计的数据）

## v4.0  UI 设计
* L1 - 主页比赛   
显示比赛列表。顶部有“我的”和“附近”tab。
每个比赛显示如下内容  --> 比赛详情页面
创建者头像和昵称
比赛双方队名
比赛地点
比赛时间
底部浮动按钮，用户可以新建一个比赛 --> 比赛详情页面
底部广告条
功能性要求：
按时间最近排序
下拉到底继续加载
单次请求最多20个
* L1 - 球队管理页面：   
显示所有球队
底部浮动按钮，可以创建一个球队 --> 球队详情页面
有球员详情入口 --> 球员详情页面
* L1 - 数据统计页面：   
* L1 - 用户反馈页面：   
* L2 - 比赛详情页面：   
形象化的显示一个排球的比赛场地
顶端是比赛双方队伍 --> 队伍选择页面
双方当前比分 --> 大计分牌页面
双方场地，及12个位置 -- > 排兵布阵页面
能将球员微信头像显示在场上
技术统计入口 --> 技术统计页面
数据分析入口 --> 数据分析页面
权限控制入口 --> 权限控制页面
* L2 - 球队详情页面：   
可以通过微信邀请逐个添加好友为球队成员 --> 邀请入队页面
也可以命名的方式添加球员 --> 球员信息输入页面
* L2 - 球员详情入口：   
有数据统计入口 --> 球员数据统计页面
* L3 - 球员信息输入页面     
* L3 - 邀请入队页面  
显示队名，队长，现有成员
要求输入自己擅长的2个位置
点击同意或者拒绝
* L3 - 球员数据统计页面：
* L3 - 排兵布阵页面
* L3 - 大计分牌页面：
全屏，上下滑手势计分，滑动的时候页面不能出现滚动。
* L3 - 技术统计页面：
可以邀请好友做指定项目或人的技术统计
* L3 - 权限控制页面
