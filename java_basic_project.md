## 1.基础的 Java 项目

### 使用 Java 插件

> build.gradle

    apply plugin: 'java'

## 2.建立项目

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


                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        