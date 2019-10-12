Responsive UI
## One Design for All Screens
实际渲染的像素长度 = 程序中的设计dp * (密度/160) 

假设设计尺寸为 768x1080px (高x宽），密度为160. (1:1)  
实际屏幕尺寸为1080x1920px, 密度为320.

程序布局尺寸按照设计尺寸来，为768x1080dp   

如果不改dpi，实际渲染的高度是 768dp * 2 = 1536 px，超过实际的屏幕高度。

程序运行时修改密度, density = 屏幕短边 / 768, 屏幕短边=屏幕实际高度和宽度中的较小者。

density-dpi=1080/768=1.406 * 160 = 224。

高度上实际渲染的像素为768 dp * 1.406 = 1080 px，正好撑满屏幕。在长边上，总长为1080*1.4 = 1512，没有填满整个屏幕。

该方案参考：

* [骚年你的屏幕适配方式该升级了!-今日头条适配方案](https://juejin.im/post/5b7a29736fb9a019d53e7ee2)
* https://www.jianshu.com/p/bf379f25616f

### activity的density会影响layout的选择吗？

答案是不会。选择layout还是根据系统默认的dp来计算的。

譬如有w1500dp的layout，和默认的layout。屏幕size = 2048*1536，density=2。程序将density改为3，屏幕的dp=2048/2=1048。加载默认的layout。如果此时用 adb shell wm density 208，屏幕的dp=2048/208x160=1537，则程序会加载w1500dp的layout。

### layout的尺寸计算公式是什么呢？

首先要看加载的layout中的尺寸dp，乘以activity的density就是物理尺寸。



假设屏幕默认density是2

###不适用情况1

长宽比不是设计尺寸，有可能出现按比例缩放不好看，自定义layout会体验会更好

###不适用情况2

因为屏幕比较宽，UX改变了设计，在宽上增加了一个按钮。怎么办？要重写所有的布局文件吗？

###不适用情况3

因为屏幕比较宽，UX觉得按钮可以宽一点。怎么办？要重写所有布局文件吗？



### 缺点

1、 第三方布局库， 未按项目效果图布局，全局修改 density 导致修改第三方布局，造成显示界面问题 2、与 smallestwith 适配方案不兼容，切换回来比较麻烦



注意点：

Activity onStop发现 this.getApplicationContext().getResources().getDisplayMetrics().densityDpi 被系统重置了！只在个别机型发现此问题，譬如三星S3手机。





# Constraintlayout

[官网阅读](https://developer.android.google.cn/training/constraint-layout?hl=en)笔记

* 没有嵌套的视图组
* 确定view的位置，必须至少给出横向和纵向的约束
* 使用前还需添加gradle的依赖，implementation 'com.android.support.constraint:constraint-layout:1.1.2'
* 有工具可将已有的其他类型的layout转换成constraintlayout
* 可以添加对用户不可见的guideline来约束其他视图，guideline的位置用dp或者百分比表示
* Barrier跟guideline作用类似，但是他没有自己的位置定义，他是随着被他约束的视图动态移动的
* 视图的大小可以指定为Fixed，或者warp content，或者match constraints。
* 视图的大小可以指定为 ratio比例
*  [8dp square grid recommendations](https://material.google.com/layout/metrics-keylines.html)
* 



