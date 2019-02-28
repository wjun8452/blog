#### 如何理解Model层包含数据，状态和业务逻辑？

#### Presenter中包含业务逻辑吗？

#### MVP组件图和依赖关系

![Alt text](https://g.gravizo.com/source/svg?https://raw.githubusercontent.com/wjun8452/blog/master/mvp.plantuml)

View和Presenter相互依赖，通常不是依赖具体的类，而是View和Presenter的接口。
Presenter依赖Model，但是反过来Model不能依赖Presenter。

#### MVVM组件图和依赖关系
![Alt text](https://g.gravizo.com/source/svg?https://raw.githubusercontent.com/wjun8452/blog/master/mvvm.plantuml)