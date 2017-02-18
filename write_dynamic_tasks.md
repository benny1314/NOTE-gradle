## 动态任务

Groovy 不仅仅被用来定义一个任务可以做什么. 你可以使用它来动态的创建任务.

### 动态的创建一个任务

> build.gradle

```
4.times { counter ->
    task "task$counter" << {
        println "I'm task number $counter"
    }
}
    
```

这里动态的创建了 task0, task1, task2, task3

`gradle -q task1` 命令的输出

```
> gradle -q task1
I'm task number 1

```

## 使用已经存在的任务

当任务创建之后, 它可以通过API来访问,你可以创建额外的依赖.

### 通过API访问一个任务 - 加入一个依赖

> build.gradle

```
4.times { counter ->
    task "task$counter" << {
        println "I'm task number $counter"
    }
}
    
task0.dependsOn task2, task3 // 此处是重点
    
```

`gradle -q task0` 命令的输出

```
> gradle -q task0
I'm task number 2
I'm task number 3
I'm task number 0

```

### 通过API访问一个任务 - 加入行为

> build.gradle

```
task hello << {
    println 'Hello Earth'
}
hello.doFirst {
    println 'Hello Venus'
}
hello.doLast {
    println 'Hello Mars'
}
hello << {
    println 'Hello Jupiter'
}
    
```

`gradle -q hello` 命令的输出

```
> gradle -q hello
Hello Venus
Hello Earth
Hello Mars
Hello Jupiter

```

doFirst 和 doLast 可以被执行许多次. 他们分别可以在任务动作列表的开始和结束加入动作. 当任务执行的时候, 在动作列表里的动作将被按顺序执行. 

**这里第四个行为中 _<<_ 操作符是 _doLast_ 的简写.**

