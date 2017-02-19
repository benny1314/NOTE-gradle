## 依赖配置

在 Gradle 里, 依赖可以组合成configurations(配置). 一个配置简单地说就是一系列的依赖，我们称它们为(dependency configuration)依赖配置

| 命令| 说明|
|----|----|
|compile|用来编译项目源代码的依赖.
|runtime|在运行时被生成的类使用的依赖. 默认的, 也包含了编译时的依赖.
|testCompile|编译测试代码的依赖. 默认的, 包含生成的类运行所需的依赖和编译源代码的依赖.
|testRuntime|运行测试所需要的依赖. 默认的, 包含上面三个依赖.

## 外部的依赖

你可以声明许多种依赖. 其中一种是external dependency(外部依赖). 这是一种在当前构建之外的一种依赖, 它被存放在远程或本地的仓库里, 比如 Maven 的库, 或者 Ivy 库, 甚至是一个本地的目录.

> 定义一个外部依赖

```
dependencies {
    compile group: 'org.hibernate', name: 'hibernate-core', version: '3.6.7.Final'
}

```

引用一个外部依赖需要使用 **group**, **name** 和 **version** 属性

#### 有一种简写形式, 只使用一串字符串 _"group:name:version"_

### 外部依赖的简写形式

> build.gradle

```
    dependencies {
        compile 'org.hibernate:hibernate-core:3.6.7.Final'
    }

```

## 仓库

Gradle 会在一个repository(仓库)里找这些文件. 仓库其实就是文件的集合, 通过 group, name 和 version 整理分类. Gradle 能解析好几种不同的仓库形式, 比如 Maven 和 Ivy, 同时可以理解各种进入仓库的方法, 比如使用本地文件系统或者 HTTP

**默认地, Gradle 不提前定义任何仓库**. 在使用外部依赖之前, 你需要自己至少定义一个库. 

### Maven central 仓库

> build.gradle

```
repositories {
    mavenCentral()
}

```

**一个项目可以有好几个库. Gradle 会根据依赖定义的顺序在各个库里寻找它们, 在第一个库里找到了就不会再在第二个库里找它了**.

































