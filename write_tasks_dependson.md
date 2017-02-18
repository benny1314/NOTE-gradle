## 任务依赖

### 声明任务之间的依赖关系 【 dependsOn: ** 】

> build.gradle

```
task cook << {
    println "开始做饭🍚"
}

task eat(dependsOn: cook) << {
    print "正在吃做好的饭🍚"
}

```

`gradle eat` 的输出
 
```
MacBook-Pro:gradle_user_guide benny$ gradle eat
:cook
开始做饭🍚
:eat
正在吃做好的饭🍚
BUILD SUCCESSFUL

Total time: 0.813 secs
``` 

`gradle -q eat` 的输出

```
MacBook-Pro:gradle_user_guide benny$ gradle -q eat
开始做饭🍚
正在吃做好的饭🍚

```

eat 依赖于 cook，所以执行eat的时候，cook命令会被优先执行来作为启动 eat任务的条件

### Lazy dependsOn - 其他的任务还没有存在

> build.gradle

```
task taskX(dependsOn: 'taskY') << {
    println 'taskX'
}
task taskY << {
    println 'taskY'
}

```

`gradle -q taskX` 命令的输出

```
> gradle -q taskX
taskY
taskX

```

注意，**taskX 到 taskY 的依赖在 taskY 被定义之前就已经声明了**

**你不能使用快捷注释当所关联的任务还没有被定义.**


