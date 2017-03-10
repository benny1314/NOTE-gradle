## 给 task 添加依赖

有许多种加入依赖的方式。任务名称可以指向同一个项目里的任务, 或者其他项目里的任务,**为了指向其他项目, 你必须在任务的名称前加入项目的路径**

> build.gradle

### 从另外一个项目给任务加入依赖

```
project('projectA') {
    task taskX(dependsOn: ':projectB:taskY') << {
        println 'taskX'
    }
}

project('projectB') {
    task taskY << {
        println 'taskY'
    }
}

```

`gradle -q taskX` 的输出

```
> gradle -q taskX
taskY
taskX

```


