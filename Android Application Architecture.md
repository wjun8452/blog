##几个大的设计考量

* 业务逻辑应该模块化，譬如将渲染引擎做成单独的服务。
* 复杂的业务UI界面状态应该合理的细化管理，譬如利用Navigation组件。
* 考虑到UI会因项目而异，应合理使用UI框架（MVP, MVVM）使得UI层与业务逻辑隔离。
* 



## 几个具体的设计问题

* NavigationView与主应用有很相似的代码，



#### 如何理解Model层包含数据，状态和业务逻辑？

如果整个应用程序只有3层，MVP或者MVVM，Model层是最复杂、最厚的一层。它包含业务数据，状态，业务逻辑。View层只负责如何展示数据。V或者VM只做胶水的工作。在VM中还存在一种跟UI状态紧密相关的数据，譬如“是否显示进度条“，这类数据跟核心业务数据不同。

UI状态数据和业务状态数据应该合理的分开，便于维护。

UI状态数据和业务状态数据都应该被单元测试所覆盖。



#### Presenter中包含业务逻辑吗？
不包含。它只包含UI Flow。UI Flow定义了户点击屏幕之后系统会有什么反馈，哪些界面随之更新。如果你要把用户体验也称作业务逻辑的话，那也可以说包含。

#### MVP组件图和依赖关系

![Alt text](https://g.gravizo.com/source/svg?https://raw.githubusercontent.com/wjun8452/blog/master/mvp.plantuml)

View和Presenter相互依赖，通常不是依赖具体的类，而是View和Presenter的接口。
Presenter依赖Model，但是反过来Model不能依赖Presenter。

#### MVVM组件图和依赖关系
![Alt text](https://g.gravizo.com/source/svg?https://raw.githubusercontent.com/wjun8452/blog/master/mvvm.plantuml)

跟MVP不同的是，VM不再依赖View，可完全独立测试。View的刷新是由[databinding] (https://developer.android.com/topic/libraries/data-binding)来完成的。

ViewModel是为activity和fragment准备和提供数据的，是介于UI和业务逻辑之间的。他的生命周期长，直到activity的[finish](https://stackoverflow.com/questions/10847526/what-exactly-activity-finish-method-is-doing)才死掉。

ViewModel一般通过LiveData和Data Binding暴露数据。它从不引用任何View。

源码分析ViewModel相关类(https://www.jianshu.com/p/e8955f525f4c)

## #MVVM vs DataBinding

先说说两者的关系，DataBinding是一个实现数据和UI绑定的框架，而MVVM是一种架构模式，实现MVVM模式需要借助DataBinding来完成。

### Databinding

* [databinding实战](http://examplecode.cn/2018/07/20/android-databinding-01-introduction/)
* 在xml中指定的variable引用改变会自动更新UI，但是其子属性发生改变则不会哦。
* 在非主线程调用databinding的notifychange是安全的，类似于LiveData.postValue

#### Navigation
* Navigation: 单activity中fragment转场处理，从一个fragment转到另一个fragment，有可视化的转场图(Navigation Graph)，整个系统有哪些page一目了然。

  * onFragmentInteraction:

### Room

* 基于SQLite的健壮的数据访问抽象层

### Lifecycle-aware component

* 以前在activity的lifecycle callback中处理跟生命周期相关的动作，一个个调用子组件的onStart等生命周期处理方法，google说这样的代码难以维护~。

### LiveData
* 为什么需要LiveData？
  * 能够感知组件（Fragment、Activity、Service）的生命周期，只有在组件出于激活状态（[STARTED](https://developer.android.google.cn/reference/android/arch/lifecycle/Lifecycle.State.html#STARTED)、[RESUMED](https://developer.android.google.cn/reference/android/arch/lifecycle/Lifecycle.State.html#RESUMED)）才会通知观察者有数据更新。组件在前台的时候能够实时收到数据改变的通知，这是可以理解的。当组件从后台到前台来时，LiveData能够将最新的数据通知组件，这两点就保证了组件中和数据相关的内容能够实时更新。 [参考](https://blog.csdn.net/zhuzp_blog/article/details/78871527)
  * LiveData是T，T的属性发生改变之后，是否自动通知观察者呢？
  * [这篇文章比较详细](https://www.jianshu.com/p/867a7cf6b918)
  * 没有LiveData的话如何解决组件更新的问题？可以用
### LiveData vs DataBinding
  * LiveData的观察者是Activity，需要activity收到通知后刷新界面。DataBinding则可以在data改变后自动刷新界面。这两者冲突呀？(POJO是不会触发UI刷新的，databinding是通过在数据变化时给出相应的通知来告知Ui层进行更新的,共有三种数据变化的机制，[Observable objects](https://developer.android.com/topic/libraries/data-binding/index.html#observable_objects), [observable fields](https://developer.android.com/topic/libraries/data-binding/index.html#observablefields), and [observable collection](https://developer.android.com/topic/libraries/data-binding/index.html#observable_collections)s.当他们中的任何一个与UI进行绑定，并且其数据属性发生变化时，都会通知到UI进行更新。LiveData不属于以上三种机制，DataBinding增加了第四种机制来实现其与LiveData的集成。
    [文章](https://www.jianshu.com/p/0f425f9d641b)中指出了DataBinding可以绑定ViewModel，ViewModel中的LiveData发生变化会触发DataBinding刷新界面，[还可以参考这篇文章](https://majing.io/posts/10000004671195)
### ViewModel

  * 只是一个具有特殊生命周期的壳子？感觉没什么用处呢。。。仅有的用处就是保存UI数据，且生命周期跟UI一致。

* [Samples](https://github.com/googlesamples/android-architecture-components)



### Reactive Programming

反应式编程要解决的问题是：数据变化了，处理数据的方法要再调用一下以便产生新的结果。

反应式编程可以使用callback的方式来实现，缺点是可扩展性不好，代码中会有太多的callback？ （https://medium.com/swlh/reactive-programming-with-kotlin-for-android-9e20efa0c130）

所以就推荐使用RxJava。



### 综述

* https://android.jlelse.eu/android-app-architecture-ground-up-d634eda1f21d





### 练一练





