微信公账号开发

* [官方文档] (https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1445241432)
* [公众号测试账号申请] (https://mp.weixin.qq.com/debug/cgi-bin/sandboxinfo?action=showinfo&t=sandbox/index)



智能互联技术方案

* 申请测试公众号
* 用户点击账号绑定
* 车机申请二维码: 参数：device_id，home&work
* 服务器存储device_id, home&work
* 服务器向微信请求'带参数的二维码'，参数：device_id即scene_id
* 车机展示二维码
6. 用户扫码关注公众号
7. 服务器收到微信接口通知，获得device_id,openid
8. 服务器存储 device_id和openid，完成设备和用户的关联
9. 服务器通知车机已经完成关联 （socket？还是轮询？）
9. 车机显示已经绑定
10. 用户更新home_work, device_id, home&work
11. 服务器存储新的home&work
10. 服务器定时器触发
11. 服务器计算ETA
12. 服务器给用户发送模板消息



``` sequence
title: 关注公众号时序图
用户 -> 车机: click binding
车机 -> 后台: applyQRCode(VIN, home/work address)
后台 -> 后台: updateDB(VIN, home/work address)
后台 -> 微信: getAccessToken(appid,appsecret)
微信 --> 后台: accessToken
后台 -> 微信: createQRCode(accessToken, scene_id=VIN)
微信 --> 后台: url
后台 --> 车机: url
车机 -> 车机: showQRCode(url)
用户 -> 车机: scan QR code
微信 -> 后台: SCAN event (openid, scene_id)
后台 -> 后台: updateDB(VIN, openid)
后台 -> 车机: binding successfully
车机 -> 车机: show message



```





服务器搭建  

* 用自己的电脑，结合内网穿透工具，用作搭建测试服务器。http://www.ngrok.cc/user.html，  wjun8452, 623521  
* 用腾讯云等商用云 
