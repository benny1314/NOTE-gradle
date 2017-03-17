## 从外部工具和库记录日志

在内部, Gradle 使用 Ant 和 lvy , 都有自己的 log 系统, Gradle 重定向他们的日志输出到 Gradle 日志系统. 除了Ant/lvy的TRACE级别的日志, 映射到Gradle的DEBUG级别, 其余的都会有一个1:1的映射从 Ant/lvy 的日志等级到 Gradle 的日志等级. 这意味着默认的 Gradle 日志级别将不会显示任何的 Ant /lvy 的输出, 除非它是一个错误或警告.

有许多工具仍然使用标准输出记录,默认的,Gradle将标准输出重定向到QUIET的日志级别和标准错误的ERROR级别.该行为是可配置的.该项目对象提供了一个[LoggerManager](https://docs.gradle.org/current/javadoc/org/gradle/api/logging/LoggingManager.html),当你构建脚本进行评估的时候,允许你改变标准输出或错误重定向的日志级别。

### 配置标准输出捕获

```
logging.captureStandardOutput LogLevel.INFO
println 'A message which is logged at INFO level'

```

任务同样提供了LoggingManager去更改任务执行过程中的标准输出或错误日志级别。

### 为任务配置标准输出捕获

> build.gradle

```
task logInfo {
    logging.captureStandardOutput LogLevel.INFO
    doFirst {
        println 'A task message which is logged at INFO level'
    }
}

```

Gradle同样提供了 `Java Util Logging,Jakarta Commons Logging` 和Log4j logging的集成工具.
使用这些工具包编写的构建的类的记录的任何日志消息都将被重定向到Gradle的日志记录系统。