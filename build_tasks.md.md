## 定义任务

任务名字可以使用简单任务的形式，在表达式中简单任务的形式是不起作用的，要使用带括号的形式

### 定义 tasks

> build.gradle

```
# 简单任务的形式
task hello <<{
    println "hello"
}

task(hello) <<{
   println "hello"
}

task(copy, type: Copy) {
    from(file('srcDir'))
    into(buildDir)
}

```

