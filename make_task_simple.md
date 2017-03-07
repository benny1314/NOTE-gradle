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

你也可以用在驼峰命名方式 (通俗的说就是每个单词的第一个字母大写,除了第一个单词) 的任务中每个单词的首字母进行调用

>  可以执行 gradle compTest 或者 gradle cT 来调用 compileTest 任务

###  简化驼峰方式的任务名

```
> gradle cT
:compile
compiling source
:compileTest
compiling unit tests

BUILD SUCCESSFUL

Total time: 1 secs

```

简化后你仍然可以使用 `-x` 参数.



