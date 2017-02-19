## 1. 多项目的 Java 构建

### 多项目构建 - 分层布局

```
multiproject/
  api/
  services/webservice/
  shared/
  
```



注意: 这个例子的代码可以在 **samples/java/multiproject** 里找到. **要注意看**‘


## 定义一个多项目构建

为了定义一个多项目构建, 你需要创建一个设置文件 ( settings.file). 设置文件放在源代码的根目录, 它指定要包含哪个项目. 

**它的名字必须叫做 _settings.gradle_**


### 多项目构建 - settings.gradle file

> settings.gradle

  include "shared","api","services:webservice","services:shared"

## 通用配置

对于绝大多数多项目构建, 有一些配置对所有项目都是常见的或者说是通用的. 

根项目就像一个容器, **subprojects** 方法遍历这个容器的所有元素并且注入指定的配置 . 通过这种方法, 我们可以很容易的定义所有项目和通用依赖的内容清单

### 多项目构建 - 通用配置

> build.gradle

```
subprojects {
    apply plugin: 'java'
    apply plugin: 'eclipse-wtp'

    repositories {
       mavenCentral()
    }

    dependencies {
        testCompile 'junit:junit:4.11'
    }

    version = '1.0'

    jar {
        manifest.attributes provider: 'gradle'
    }
}

```

在上面的例子中，Java插件被应用到每一个子项目中 plugin to each ，这意味着我们前几章看到的任务和属性都可以在子项目里被调用

## 项目之间的依赖

你可以在同一个构建里加入项目之间的依赖

一个项目的 JAR 文件被用来编译另外一个项目. 在 api 构建文件里我们将加入一个由 shared 项目产生的 JAR 文件的依赖. 由于这个依赖, Gradle 将确保 shared 项目总是在 api 之前被构建.

###  多项目构建 - 项目之间的依赖

> api/build.gradle

```
dependencies {
    compile project(':shared')
}

```

















未完待续   ❌ ❌ ❌ ❌ ❌ ❌ ❌


shell 文件夹 /Users/benny/myapplication/gradle_user_guide





