## 定位任务

你经常需要在构建文件里找到你定义的 tasks
**
每一个任务都必须是一个 project 的有效属性, 并使用任务名来作为属性名**

声明任务的时候是可以,只声明任务名字的

```
task hello

hello <<{
    println '自定义的任务'
}

println '我在hello任务的下面'

```

执行 `gradle hello` 的结果

```
我在hello任务的下面

自定义的任务

```

可以看到 会先执行 println 方法 在执行任务hello


### 通过属性获取tasks

> build.gradle

```
task hello

println hello.name
println project.hello.name

```

### Tasks 也可以通过 tasks collection 来获取

> build.gradle

```
task hello

println tasks.hello.name
println tasks['hello'].name

```

你也可以使用 `tasks.getByPath()` 方法通过任务的路径来使用任何 **project** 里的任务. 你可以通过使用任务的名字, 任务的相对路径或者绝对路径作为 `getByPath()` 方法的输入.


### 根据路径获取 tasks

> build.gradle

```
project(':projectA') {
    task hello
}

task hello

println tasks.getByPath('hello').path
println tasks.getByPath(':hello').path
println tasks.getByPath('projectA:hello').path
println tasks.getByPath(':projectA:hello').path

```

`gralde hello` 的输出

```
> gradle -q hello
:hello
:hello
:projectA:hello
:projectA:hello

```

参考 [TaskContainer](https://docs.gradle.org/current/javadoc/org/gradle/api/tasks/TaskContainer.html) 可以知道跟多关于定位 tasks 的选项.
