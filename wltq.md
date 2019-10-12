物理弹球游戏

### 开发日志

* 5/1, 本地路径：~/git/wltq, 用Cocos Creator开发游戏逻辑，打包成微信小游戏，可行。遇到一个小问题，project.config.json被微信认作为小程序了，用微信默认生成的覆盖即可。

* 10/7, 先不管构建微信小游戏的细节（譬如屏幕适配），重点放在游戏逻辑的开发上，在Mac上调试完善之后再考虑导出为微信小游戏的事情。

* 时序图

  ``` sequence
  System --> Game : onLoad
  Game --> Game : createWall()
Game --> Game : createBalls
  Game --> Ball: creat(x, y)
  Game --> System : onLoad
  System --> Game: onTouchStart()
  Game --> Game: createForceLine()
  Game --> System: 
  System --> Game: onTouchEnd()
  Game --> Game: disableTouch()
  Game --> Game: destroyForceLine()
  Game --> Game: pushBall(force)
  Game --> System: 
  System --> Game : onBallCollected()
  Game --> Game: createNewBlockLine()
  Game --> Game: keepBallOrDestoryBall()
  Game --> Game: enableTouch()
  Game --> System: 
  System --> Game : onGameOver()
  
  Game --> System :
  
  
  
  ```
  
  

### 需求

* 圆形，三角形，正方形







###参考资料

* [微信小游戏开发文档](https://developers.weixin.qq.com/minigame/dev/guide/)
* [Cocos Creator文档](http://docs.cocos.com/creator/manual/zh/)
* 小程序账号，wjun8452@163.com, wjun_8452。邮箱密码相同。这个不是小游戏账号呢。。。
* Cocos 账号 wjun_8452@163.com, 623521
* [21点卡牌游戏Github](https://github.com/cocos-creator/tutorial-blackjack)
* [cocos2d-x源码](https://github.com/cocos2d/cocos2d-x)
* [cocos2d-x文档](https://docs.cocos2d-x.org/cocos2d-x/zh/)
* [cocos2d-api文档]([http://docs.cocos.com/creator/api/zh/](http://docs.cocos.com/creator/api/zh/))

