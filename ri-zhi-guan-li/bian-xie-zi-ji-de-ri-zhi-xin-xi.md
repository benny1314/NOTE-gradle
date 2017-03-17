## 编写自己的日志信息

用于记录你的构建文件的简单办法就是将消息些出入标准输入输出

Gradle 重定向任何东西写入到标准输入输出到它的log系统作为 `quite` 级别的log

### 使用标准输入输出吸入log信息

> build.gradle

    println 'A message which is logged at QUIET level'

Gradle 提供了一个 logger 属性来构建脚本，这是**Logger** 的一个示例,这个接口继承自`Slf4j`接口并且加入了一些Gradle的具体方法

### 写入自己的 log 信息

> build.gradle

```
logger.quiet('An info log message which is always logged.')
logger.error('An error log message.')
logger.warn('A warning log message.')
logger.lifecycle('A lifecycle info log message.')
logger.info('An info log message.')
logger.debug('A debug log message.')
logger.trace('A trace log message.')

```

### 使用 Slf4j 写入log信息

> build.gradle

```
import org.slf4j.Logger
import org.slf4j.LoggerFactory

Logger slf4jLogger = LoggerFactory.getLogger('some-logger')
slf4jLogger.info('An info log message logged using SLF4j')

```

