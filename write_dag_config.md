## 通过 DAG 配置

Gradle 有一个配置阶段和执行阶段. 在配置阶段后, Gradle 将会知道应执行的所有任务. Gradle 为你提供一个"钩子", 以便利用这些信息. 

### 根据选择的任务产生不同的输出

> build.gradle

```
task distribution << {
    println "We build the zip with version=$version"
}

task release(dependsOn: 'distribution') << {
    println 'We release now'
}

gradle.taskGraph.whenReady {taskGraph ->
    if (taskGraph.hasTask(release)) {
        version = '1.0'
    } else {
        version = '1.0-SNAPSHOT'
    }
}

```

`gradle -q distribution` 命令的输出

```
> gradle -q distribution
We build the zip with version=1.0-SNAPSHOT
Output of gradle -q release
> gradle -q release
We build the zip with version=1.0
We release now

```


