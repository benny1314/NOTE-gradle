Log 是构建的主要"UI"工具. 如果日志太过冗长, 那么真正的警告和问题会隐藏其中, 另一方面, 如果你出错了,你又需要搞清楚相关错误信息. 

**Gradle 提供了6个等级的 log**

### 日志级别


|Level |    用途|
|-------|-------|
|ERROR	|错误信息
|QUIET	|重要消息信息
|WARNING|	警告信息
|LIFECYCLE|	进度消息信息
|INFO	|信息消息
|EBUG	|调试信息

### 选择日志级别

#### Log 等级命令行选项

|选项	|     输出日志等级|
|-------|---------------|
|no logging options|	LIFECYCLE及更高
|-q or --quiet	|QUIET及更高
|-i or --info	|INFO及更高
|-d or --debug	|DEBUG及更高(所有日志信息)

#### 堆栈信息选项

|选项    |	含义|
|--------|---------|
|No stacktrace options|	无堆栈踪迹输出到控制台的情况下生成错误信息(如编译错误) ,仅在内部异常时打印堆栈信息.如果选择DEBUG日志等级,总会打印截断堆栈信|息
|-s or --stacktrace|	打印截断堆栈信息,我们推荐这个而不是full stacktrace ,Groovy的full |stacktrace|非常详细.(由于底层的动态调用机制。然而，他们通常不包含你的代码出了什么错的相关信息)
-S or --full-stacktrace |	打印全部堆栈信息







