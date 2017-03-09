## 配置 tasks

Gradle 自带的 Copy task. 为了创建一个 Copy task, 你需要在你的构建脚本里先声明它:



[Gradle 中的 Task types，也就是 gradle 默认的 task](https://docs.gradle.org/current/dsl/org.gradle.api.tasks.Copy.html#org.gradle.api.tasks.Copy:source)

###  创建一个 copy task

> build.gradle

    task myCopy(type: Copy)

此处声明了一个没有方法体的 copy task 