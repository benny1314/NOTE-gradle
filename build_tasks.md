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

### 使用 字符串 来定义任务的名字

> build.gradle

```
task('hello') <<{
    println "hello"
}

task('copy', type: Copy) {
    from(file('srcDir'))
    into(buildDir)
}

```

### 更加直观声明任务的形式

> build.gradle

```
tasks.create(name: 'hello') <<{
    println "hello"
}

tasks.create(name: 'copy', type: Copy) {
    from(file('srcDir'))
    into(buildDir)
}

```

[更多 Task 的信息请参考官网](https://docs.gradle.org/current/javadoc/org/gradle/api/tasks/TaskContainer.html)


