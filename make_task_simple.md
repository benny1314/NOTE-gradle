## 简化任务名

当你试图调用某个任务的时候, 你并不需要输入任务的全名. 只需提供足够的可以唯一区分出该任务的字符即可

> build.gradle

```
task compile << {
    println 'compiling source'
}

task compileTest(dependsOn: compile) << {
    println 'compiling unit tests'
}

task test(dependsOn: [compile, compileTest]) << {
    println 'running unit tests'
}

task dist(dependsOn: [compile, test]) << {
    println 'building the distribution'
}

```

### 简化任务名

可以直接写 `gradle di` 来调用 dist 任务

```
> gradle di
:compile
compiling source
:compileTest
compiling unit tests
:test
running unit tests
:dist
building the distribution

BUILD SUCCESSFUL

Total time: 1 secs

```

