Gradle常用知识点
###  Groovy is basic
* [What is Groovy] (https://blog.csdn.net/singwhatiwanna/article/details/76084580)
* [Groovy official API document] (http://docs.groovy-lang.org/latest/html/groovy-jdk/java/io/File.html)


### Gradle DSL

* [What is Gradle](https://blog.csdn.net/singwhatiwanna/article/details/78797506)  
* [What is Task](https://blog.csdn.net/singwhatiwanna/article/details/78898113)
* [Task official API document](https://docs.gradle.org/current/javadoc/org/gradle/api/Task.html)
* [Project official API document] (https://docs.gradle.org/current/javadoc/org/gradle/api/Project.html)
* [一句一句分析gradle语句背后的故事] (https://www.jianshu.com/p/822e44a5ea97)


###Dependencies
* [经验总结](http://leoray.leanote.com/post/gradle_dependencies)
* [官方文档](https://docs.gradle.org/current/javadoc/org/gradle/api/artifacts/dsl/DependencyHandler.html)


### Questions  
* what is the nature of 'compile', 'dependency' in a build.gradle file?
* apply plugin: 'com.android.application', what is behind?
* 点击sync project按钮背后做了什么？
* 点击make project按钮背后做了什么？
* How to publish to local repo?
* 如何打印任务的执行顺序?

 > 答：./gradlew task –m

* 下面的代码什么时候被执行? 

```
artifacts {
    archives jarNavigationView
}

```
 >答：

* 下面的错误？

```
What went wrong:   
Execution failed for task ':navigationView:checkstyle'   
> Unable to create a Checker: configLocation {/Users/junwang/git/hmi-common/        NavHome/Apps/Arp/quality/checkstyle/checkstyle.xml}, classpath {null}. 

```

 > 答：checkstyle.xml不存在

* 在执行每个task之前检查某一个文件是否存在，如何实现？    

 > 答：定义一个task检查文件是行不通的，因为一个task只能被加入到graph中一次。

