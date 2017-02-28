## 多任务调用

你可以以列表的形式在命令行中一次调用多个任务
`gradle compile test` 命令会依次调用 `compile` 和 `test` 任务, 它们所依赖的任务也会被调用. 

**这些任务只会被调用一次**, 无论它们是否被包含在脚本中:即无论是以命令行的形式定义的任务还是依赖于其它任务都会被调用执行.

### 多任务调用

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

输出结果

```
> gradle dist test
:compile
compiling source
:compileTest
compiling unit tests
:test
running unit tests
:dist
building the distribution

```

由于**每个任务仅会被调用一次**,所以调用`gradle test test`与调用gradle test效果是相同的.

当任务依赖**多个**任务的时候，`depedsOn:[]` 后面要跟的是数组

