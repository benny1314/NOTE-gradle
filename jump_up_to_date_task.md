## 跳过 up-to-date 的任务

如果你正在使用一些附加的任务, 比如通过 Java 插件加入的任务, 你可能会注意到 Gradle 会跳过一些任务, 这些任务后面会标注 up-to-date. 

代表这个任务已经运行过了或者说是最新的状态, 不再需要产生一次相同的输出.

不仅仅是这些内建任务, 其实你在运行自己的任务时, 也会碰到这种情况.

### 声明一个任务的输入和输出

> A generator task

> build.gradle

```
task transform {
    ext.srcFile = file('mountains.xml')
    ext.destDir = new File(buildDir, 'generated')
    doLast {
        println "Transforming source file."
        destDir.mkdirs()
        def mountains = new XmlParser().parse(srcFile)
        mountains.mountain.each { mountain ->
            def name = mountain.name[0].text()
            def height = mountain.height[0].text()
            def destFile = new File(destDir, "${name}.txt")
            destFile.text = "$name -> ${height}\n"
        }
    }
}

```

`gradle transform` 的输出

```
> gradle transform
:transform
Transforming source file

```
`gradle transform` 的输出

```
> gradle transform
:transform
Transforming source file.

```

**这里 Gradle 执行了这个任务两次, 即使什么都没有改变, 它也没有跳过这个任务. **

**它的行为是通过闭包定义的. Gradle 并不知道闭包会做什么, 也并不能自动指出是否这个任务是 up-to-date**. 为了使用 Gradle 的 up-to-date 检测, 你需要**定义任务的输入和输出**.

> 每个任务都有输入和输出属性, 你需要使用这些属性来声明任务的输入和输出. 下面的例子中, 我们将声明 XML 文件作为输入, 并且把输出放在一个指定的目录. 让我们运行这个任务 2 次.

### 声明任务的输入和输出

> build.gradle

```
task transform {
    ext.srcFile = file('mountains.xml')
    ext.destDir = new File(buildDir, 'generated')
    
    ### 定义任务的输入和输出
    inputs.file srcFile
    outputs.dir destDir
    
    doLast {
        println "Transforming source file."
        destDir.mkdirs()
        def mountains = new XmlParser().parse(srcFile)
        mountains.mountain.each { mountain ->
            def name = mountain.name[0].text()
            def height = mountain.height[0].text()
            def destFile = new File(destDir, "${name}.txt")
            destFile.text = "$name -> ${height}\n"
        }
    }
}

```

> gradle transform 的输出

```
> gradle transform
:transform
Transforming source file.

```

> gradle transform 的输出

```
> gradle transform
:transform UP-TO-DATE

```

**现在, Gradle 就能够检测出任务是否是 up-to-date 状态.**

任务的输入属性是 [TaskInputs](https://docs.gradle.org/current/javadoc/org/gradle/api/tasks/TaskInputs.html#gsc.tab=0)类型. 任务的输出属性是 [TaskOutputs](https://docs.gradle.org/current/javadoc/org/gradle/api/tasks/TaskOutputs.html#upToDateWhen(groovy.lang.Closure)类型.

##### 使用规则

如果   













