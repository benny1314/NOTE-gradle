## 脚本 API

当 Gradle 执行一个脚本时，它会将这个脚本编译为实现了 **Script** 的类，也就是所有的**属性**和**方法**都是再 Script接口中生命的，由于你的脚本实现了 Script 接口，所以你可以再自己的脚本中使用他们

## 声明变量

在 Gradle 构建脚本中有两种类型的变量可以声明：**局部变量** ( local ) 和 **扩展属性** ( extra ) 

## 局部变量

局部变量使用关键字 **def** 来声明，其只在声明它的地方可见。局部变量是 Groovy 语言的有个基本特性

### 使用局部变量

```
def dest = "dest"

task copy(type: Copy){
    from "source"
    into dest
}

```

## 拓展属性

在 Gradle 领域模型中所有被增强的对象能够拥有自己定义的属性。这包括，但不仅限于 **projects**、**tasks** 还有 *sourceSets**。 **Porject **对象可以添加、读取、更改拓展的属性。

** 💔 使用 ext 拓展块可以一次添加多个属性**

### 使用拓展属性

> build.gradle

```
apply plugin: "java"

ext {
    springVersion = "4.2.4.RELEASE"
    emailNotification = "build@master.org"
}

sourceSets.all { ext.purpose = null }

sourceSets {
    main {
        purpose = "production"
    }
    test {
        purpose = "test"
        }
    plugin {
        purpose = "production"
    }

    }

    task printProperties << {
        println springVersion
        println emailNotification
        sourceSets.matching { it.purpose == "production" }.each { println it.name }
    }

```

```
> gradle -q printProperties
3.1.0.RELEASE
build@master.org
main
plugin

```

一个 **ext** 拓展块向 **Project** 对象添加了两个拓展属性。名为 **purpose** 的属性被添加到每个 **sourceSets**，然后 设置 `ext.purpose` 等于 `null` （null值是被允许的）。当这些属性被添加后，他们就像预定义的属性一样可以被读取，更改值。

我们通过一个特殊的语句添加拓展属性，当您试图设置一个预定义属性或者拓展属性，但是属性名拼写错误或者不存在时，操作就会失败。

Project 对象可以在任何地方使用其拓展属性，他们比局部变量有更大的作用域，**一个项目的拓展属性对其子项目也可见**

[关于ext详情ExtraPropertiesExtension 类的 API 文档说明](https://docs.gradle.org/current/dsl/org.gradle.api.plugins.ExtraPropertiesExtension.html)



