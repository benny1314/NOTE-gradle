## 多任务调用

你可以以列表的形式在命令行中一次调用多个任务
`gradle compile test` 命令会依次调用 `compile` 和 `test` 任务, 它们所依赖的任务也会被调用. 

**这些任务只会被调用一次**, 无论它们是否被包含在脚本中:即无论是以命令行的形式定义的任务还是依赖于其它任务都会被调用执行

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

## 排除任务

你可以使用命令行选项`-x`来排除某些任务

### 排除任务

    gradle dist -x test

```
> gradle dist -x test
:compile
compiling source
:dist
building the distribution

BUILD SUCCESSFUL

Total time: 1 secs

```

可以看到，**test任务并没有被调用，即使它是 dist 任务的依赖。**同时 test 任务的依赖任务 compileTest 也没有被调用，而像 compile 被 test 和其他任务同时依赖的任务仍然会被调用

## 失败后继续执行构建

默认情况下，只要有任务调用失败，Gradle就会中断执行，这可能会使调用过程更快，但那些后面隐藏的错误就没有办法发现了，所以你可以使用 `--continue` 选项在一次调用中尽可能多的发现所有问题

采用 `--continue` 选项，Gradle 会调用每一个任务以及它们依赖的任务。而不是一旦出现错误就会中断执行，所有错误信息都会被列出来

一旦某个任务执行失败，那么所有依赖该任务的子任务都不会被调用。例如由于 test 任务依赖于 compile 任务，所以如果 compile 调用出错，test便不会被直接或间接调用。








