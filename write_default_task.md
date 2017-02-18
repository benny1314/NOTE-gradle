## 默认任务

Gradle 允许在脚本中定义一个或多个默认任务

### 定义默认任务

> build.gradle

```
defaultTasks 'cook', 'eat'

task cook << {
    println 'Default cook!'
}

task eat << {
    println 'Default eat!'
}

task sleep << {
    println "I'm not a default task!"
}

```

`gradle -q` 输出

```
gradle -q 命令的输出
> gradle -q
Default cook!
Default eat!

```

上面的默认任务 `defaultTasks 'cook', 'eat'` 等价于 `gradle -q cook eat`.

在一个多项目构建中，每一个子项目都可以有它特别的默认任务，如果一个子项目没有特别的默认任务，父项目的默认任务将会被执行



