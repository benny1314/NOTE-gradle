Project 对象提供了一些标准的属性，您可以在构建脚本中很方便的使用它们

> 常用属性

| 属性名 |  类型 |默认值
|--------|-------|-----
|project|Project|Project实例对象
|name|String|项目目录的名称|
|path|String|项目的绝对路径|
|description|String|项目描述|
|projectDir|File|包含构建脚本的目录|
|build|File|projectDir/build
|group|Object|未具体说明
|version|Object|未具体说明|
|ant|AntBuilder|Ant实例对象|

> 建议：

不要忘记我们的构建脚本只是个很简单的 Groovy 代码 ，不过它会再调用 Gradle API，Project 接口通过调用 Gradle API 让我们可以操作任何事情，因此如果你想知道哪个标签('tags') 可以在构建脚本种使用，您可以查询  **Dash** 翻阅 Project 接口的的说明文档.

## 脚本 API

当 Gradle 执行一个脚本时，它会将这个脚本编译为实现了 **Script** 的类，也就是所有的**属性**和**方法**都是再 Script接口中生命的，由于你的脚本实现了 Script 接口，所以你可以再自己的脚本中使用他们

