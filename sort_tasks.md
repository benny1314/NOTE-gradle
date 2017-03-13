## 给 tasks 排序

任务的排序功能正在测试和优化. 请注意, 这项功能在 Gradle 之后的版本里可能会改变.

### 有 2 种可用的排序规则: "must run after" 和 "should run after".

当你使用 “must run after” 时即意味着 taskB 必须总是在 taskA 之后运行, 无论 taskA 和 taskB 是否将要运行:
taskB.mustRunAfter(taskA)

### 加入 'must run after' 

> build.gradle

```
task taskX << {
    println 'taskX'
}
task taskY << {
    println 'taskY'
}
taskY.mustRunAfter taskX

```

`gradle -q taskY taskX` 的输出

```
> gradle -q taskY taskX
taskX
taskY

```

加入 'should run after'

> build.gradle

```
task taskX << {
    println 'taskX'
}
task taskY << {
    println 'taskY'
}
taskY.shouldRunAfter taskX

```

`gradle -q taskY taskX` 的输出

```
> gradle -q taskY taskX
taskX
taskY

```

### 任务排序不影响任务执行

taskY
为了在 2 个任务间定义 “must run after” 或者 “should run after” 排序, 我们需要使用 Task.mustRunAfter() 和 Task.shouldRunAfter() 方法. 这些方法接收一个任务的实例,　任务的名字或者任何 Task.dependsOn()可以接收的输入.

> 注意 

`B.mustRunAfter(A)` 或者 `B.shouldRunAfter(A)` 并不影响任何任务间的执行依赖:

+ tasks A 和 B 可以被独立的执行. 排序规则只有当 2 个任务同时执行时才会被应用.
+ 在运行时加上 --continue, 当 A 失败时 B 仍然会执行.

之前提到过, “should run after” 规则在一个执行循环中将被忽略:

`should run after` 任务的忽略

> build.gradle

```
task taskX << {
    println 'taskX'
}
task taskY << {
    println 'taskY'
}
task taskZ << {
    println 'taskZ'
}

```
taskX.dependsOn taskY
taskY.dependsOn taskZ
taskZ.shouldRunAfter taskX

```

`gradle -q taskX` 的输出

> gradle -q taskX
taskZ
taskY
taskX

```


