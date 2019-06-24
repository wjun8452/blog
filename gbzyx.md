物理弹球游戏

### 开发日志

* 打包微信小游戏，project.config.json被微信认作为小程序了，用微信默认生成的覆盖即可。可以在mac上看到运行效果，但是点击手机预览出错。

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

