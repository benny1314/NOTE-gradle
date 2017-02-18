## Hello world

你可以通过 gradle 命令运行一个 Gradle 构建.

**gradle** 命令会在当前目录中查找一个叫 **build.gradle** 的文件. 我们称这个 build.gradle 文件为一个**构建脚本** (build script)

严格来说它是一个**构建配置脚本** (build configuration script). 这个脚本定义了一个 **project** 和它的 **tasks**.

### 1. 第一个构建脚本

> build.gradle

```
task hello {
    doLast {
        println 'Hello world!'
    }
}

```

#### 使用 `-q`模式，构建tasks

进入脚本所在的文件夹然后输入 `gradle -q hello` 来执行构建脚本:

```
> gradle -q hello
Hello world!

```

需要注意的是：

1. `-q` 代表quite模式，不会生成Gradle的日志信息，只能看到tasks的输出，使输出更加清晰
2. **hello** 是 任务名


#### 如果不使用 `-q` 模式，构建tasks

    gradle hello

执行结果就会是这样 

```
:hello
Hello world

BUILD SUCCESSFUL

Total time: 0.9 secs

```

## 快捷的任务定义

定义 hello 任务，还可以使用更简明的方法

### 快捷的构建任务定义

> build.gradle

```
task hello << {
    println 'Hello world!'
}

```

它定义了一个叫做 hello 的任务, 这个任务是一个**可以执行的闭包**

与前面的例子比较，`doLast{...}` 被替换成了 `<<` ，它们有一样的功能，但是看上去更加简洁了。





