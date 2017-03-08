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

此处可以直接查询  Dash 