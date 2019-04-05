#### 如何理解Model层包含数据，状态和业务逻辑？
如果整个应用程序只有3层，MVP或者MVVM，Model层是最复杂、最厚的一层。它包含业务数据，状态，业务逻辑。View层只负责如何展示数据。V或者VM只做胶水的工作。在VM中还存在一种跟UI状态紧密相关的数据，譬如“是否显示进度条“，这类数据跟核心业务数据不同。

#### Presenter中包含业务逻辑吗？
不包含。它只包含UI Flow。UI Flow定义了户点击屏幕之后系统会有什么反馈，哪些界面随之更新。如果你要把用户体验也称作业务逻辑的话，那也可以说包含。

#### MVP组件图和依赖关系

![Alt text](https://g.gravizo.com/source/svg?https://raw.githubusercontent.com/wjun8452/blog/master/mvp.plantuml)

View和Presenter相互依赖，通常不是依赖具体的类，而是View和Presenter的接口。
Presenter依赖Model，但是反过来Model不能依赖Presenter。

#### MVVM组件图和依赖关系
![Alt text](https://g.gravizo.com/source/svg?https://raw.githubusercontent.com/wjun8452/blog/master/mvvm.plantuml)

跟MVP不同的是，VM不再依赖View，可完全独立测试。View的刷新是由[databinding] (https://developer.android.com/topic/libraries/data-binding)来完成的。

#### Google Architecture Component
* [Samples](https://github.com/googlesamples/android-architecture-components)



