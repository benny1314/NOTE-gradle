## 给 task 添加依赖

有许多种加入依赖的方式。任务名称可以指向同一个项目里的任务, 或者其他项目里的任务,**为了指向其他项目, 你必须在任务的名称前加入项目的路径**

### 从另外一个项目给任务加入依赖

> build.gradle

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

### 除了使用任务名称, 你也可以定义一个依赖对象y:

#### 通过任务对象加入依赖

> build.gradle

```
task taskX <<{
    println 'taskX'
}

task taskY <<{
    println 'taskY'
}

taskX.dependsOn taskY

```

`gradle -q taskY` 的输出

```
> gradle -q taskX

taskY
taskX

```

**更加先进的用法, 你可以通过闭包定义一个任务依赖**. 闭包只能返回一个单独的 Task 或者 Task 对象的 collection, 这些返回的任务就将被当做依赖. 

接下来的例子给 taskX 加入了一个复杂的依赖, 所有以 lib 开头的任务都将在 taskX 之前执行:

### 通过比高加入依赖

> build.gradle

```
task taskX << {
    println 'taskX'
}

taskX.dependsOn {
    tasks.findAll{task -> task.name.startsWith('lib')}
}

task lib1 << {
    println 'lib1'
}

task lib2 << {
    println 'lib2'
}

task notALib<< {
    println 'notALib'
}

```

`gradle -q taskX` 的输出

```
> gradle -q taskX
lib1
lib2
taskX

```

`task.name.startsWith('lib')` 是 **startsWith** 不是 ~~startWith~~