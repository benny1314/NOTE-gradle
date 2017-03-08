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

