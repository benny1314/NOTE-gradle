## Groovy 基础

Groovy 提供了大量的特性用来创建 DSL. Gradle 构建语言知道 Groovy 语言的工作原理，并利用这些特性帮助您编写构建脚本，特别是您在编写 plugin 或者 task 的时候，你会觉得很方便

## Groovy JDK

Groovy 在 Java 基础上添加了很多有用的方法. 例如，Iterable 有一个 each 方法， 通过使用 each 方法,我们可以迭代出 Iterable 中的每一个元素:

### Groovy JDK 方法

> build.gradle

    configuration.runtime.each { File f -> println f }

## 属性存取器

Groovy 自动将一个属性的引用转换为相应的 **getter**或 **setter**方法

> 属性存取器

```
// 使用 getter 方法
println project.buildDir
println getProject().getBuildDir()

// 使用 setter 方法
project.buildDir = 'target'
getProject().setBuildDir('target')

```

## 可有可无的`()`

在调用方法时，`()`~~可有可无~~，是可选的

> build.gradle

```
test.systemProperty 'some.prop', 'value'
test.systemProperty('some.prop', 'value')

```

## List 和 Map 集合

Groovy 为预定义的 List 和 Map 集合提供了一些操作捷径，这两个字面值都比较简单易懂，但是 Map 会有一些不同

 > build.gradle
 
 ``` 
 // List 集合
test.includes = ['org/gradle/api/**', 'org/gradle/internal/**']

List<String> list = new ArraryList<String>()
list.add('org/gradle/api/**')
list.add('org/gradle/internal/**')
test.includes = list

// Map 集合
Map<String,String> map = [key1:'value1', key2:'valu2']

// Groovy 会强制将Map的键值对转换为只有value的映射
apply plugin: 'java'
 
 ```

## 闭包作为方法的最后一个参数

Gradle DSL 在很多地方使用闭包，这里我们将讨论更多关于闭包的使用. 当一个方法的最后一个参数是一个闭包时，您可以在方法调用后放置一个闭包

### 闭包作为方法的参数

> build.gradle

```
repositories {
    println "in a closure"
}
repositories() { println "in a closure" }
repositories({println "in a closure" })

```

## 闭包委托对象

每个闭包都有一个委托对象，当闭包既不是局部变量也不是作为方法参数时，Groovy 使用委托对象查找变量和方法引用. 当委托对象被用来管理时，Gradle 使用它来管理闭包

### 闭包引用

> build.gradle

```
dependencies {
    assert delegate == project.dependencies
    testCompile('junit:junit:4.11')
    delegate.testCompile('junit:junit:4.11')
}

```