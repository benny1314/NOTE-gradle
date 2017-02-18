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
Default Cleaning!
Default Running!

```



