## 1. 基础的 Java 项目

### 使用 Java 插件

> build.gradle

    apply plugin: 'java'

## 2. 建立项目

Java 插件在你的项目里加入了许多任务. 然而, 你只会用到其中的一小部分任务. 最常用的任务是 build 任务, 它会建立你的项目. 当你运行 gradle build 命令时, Gradle 将会编译和测试你的代码, 并且创建一个包含类和资源的 JAR 文件:

### 建立一个 Java 项目

> gradle build

```
> gradle build
:compileJava
:processResources
:classes
:jar
:assemble
:compileTestJava
:processTestResources
:testClasses
:test
:check
:build

BUILD SUCCESSFUL

Total time: 1 secs

```

> gradle clean

**删除 build 生成的目录和所有生成的文件**

> gradle assemble

**编译并打包你的代码**, 但是并不运行单元测试. 其他插件会在这个任务里加入更多的东西. 举个例子, 如果你使用 War 插件, 这个任务将根据你的项目生成一个 WAR 文件.

> gradle check

**编译并测试你的代码**. 其他的插件会加入更多的检查步骤. 举个例子, 如果你使用 checkstyle 插件, 这个任务将会运行 Checkstyle 来检查你的代码.

## 3. 外部的依赖

通常, 一个 Java 项目有许多外部的依赖, 既是指外部的 JAR 文件. 为了在项目里引用这些 JAR 文件, 你需要告诉 Gradle 去哪里找它们. 在 Gradle 中, JAR 文件位于一个仓库中， 这里的仓库类似于 MAVEN 的仓库. 仓库可以被用来提取依赖, 或者放入一个依赖, 或者两者皆可. 举个例子, 我们将使用开放的 Maven 仓库:

### 加入 Maven 仓库

> bulid.gradle

```
repositories {
    mavenCentral()
}

```

### 加入依赖

> build.gradle

```
dependencies {
    compile group: 'commons-collections', name: 'commons-collections', version: '3.2'
    testCompile group: 'junit', name: 'junit', version: '4.+'
}

```

可以看到 commons-collections 被加入到了编译阶段, junit 也被加入到了测试编译阶段.

## 4. 定制项目 ❗️
**
Java 插件给项目加入了一些属性 (propertiy)**. 这些属性已经被赋予了默认的值, 已经足够来开始构建项目

### 定制 MANIFEST.MF 文件

> build.gradle

```
sourceCompatibility = 1.8
version = '1.0'
jar {
    manifest {
        attributes 'Implementation-Title': 'Gradle Quickstart', 'Implementation-Version': version
    }
}

```

Java 插件加入的任务是常规性的任务, 准确地说, 就如同它们在构建文件里声明地一样. 这意味着你可以使用任务之前的章节提到的方法来定制这些任务. 举个例子, 你可以设置一个任务的属性, 在任务里加入行为, 改变任务的依赖, 或者完全重写一个任务, 我们将配置一个测试任务, 当测试执行的时候它会加入一个系统属性:

### 测试阶段加入一个系统属性

> build.gradle

```
test {
    systemProperties 'property': 'value'
}

```

### 哪些属性是可用的? ❗️❗️❗️❗️❗️✡️

你可以使用 gradle properties 命令来列出项目的所有属性. 这样你就可以看到 Java 插件加入的属性以及它们的默认值.

你配置好的属性，此时 执行命令 `build gradle` 也会打印出来。


## 发布 JAR 文件

通常 JAR 文件需要在某个地方发布. 为了完成这一步, 你需要告诉 Gradle 哪里发布 JAR 文件. 在 Gradle 里, 生成的文件比如 JAR 文件将被发布到仓库里. 在我们的例子里, 我们将发布到一个本地的目录. 你也可以发布到一个或多个远程的地点.

###  发布 JAR 文件

> build.gradle

```
uploadArchives {
    repositories {
       flatDir {
           dirs 'repos'
       }
    }
}

```

运行 `gradle uploadArchives` 命令来发布 JAR 文件.






































                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        