## 跳过 tasks

### 使用判断条件

你可以使用 onlyIf() 方法来为一个任务加入判断条件. 就和 Java 里的 if 语句一样, 任务只有在条件判断为真时才会执行. 你通过一个闭包来实现判断条件. 闭包像变量一样传递任务, 如果任务应该被执行则返回真, 反之亦然.

**判断条件在任务执行之前进行判断**

#### 使用判断条件跳过一个任务

> build.gradle

```
task hello << {
    println "hello world"
}

hello.onlyIf {!project.hjasProperties('skipHello')}

```

`gradle hello -PskipHello` 的输出

```
> gradle hello -PskipHello
:hello SKIPPED
BUILD SUCCESSFUL

Total time: 1 secs

```

###  使用 StopExecutionException

如果想要跳过一个任务的逻辑并不能被判断条件通过表达式表达出来, 你可以使用 **StopExecutionException**. 

如果这个异常是被一个任务要执行的动作抛出的, 这个动作之后的执行以及所有紧跟它的动作都会被跳过. 构建将会继续执行下一个任务.






