Gradle常用知识点
###  Groovy is basic
* [What is Groovy] (https://blog.csdn.net/singwhatiwanna/article/details/76084580)
* [Groovy official API document] (http://docs.groovy-lang.org/latest/html/groovy-jdk/java/io/File.html)


### Gradle DSL is the next

* [What is Gradle](https://blog.csdn.net/singwhatiwanna/article/details/78797506)  
* [What is Task](https://blog.csdn.net/singwhatiwanna/article/details/78898113)
* [Task official API document](https://docs.gradle.org/current/javadoc/org/gradle/api/Task.html)
* [Project official API document] (https://docs.gradle.org/current/javadoc/org/gradle/api/Project.html)
* [一句一句分析gradle语句背后的故事] (https://www.jianshu.com/p/822e44a5ea97)



### Questions  
* what is the nature of 'compile', 'dependency' in a build.gradle file?
* apply plugin: 'com.android.application', what is behind?
* 点击sync project按钮背后做了什么？
* 点击make project按钮背后做了什么？


``` groovy
task exportJar(type: Copy) {
	from('build/intermediates/bundles/release/')
	into('build/libs/')
	include('classes.jar')
	rename ('classes.jar', 'test.jar')
}
```