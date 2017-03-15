## 文件树

文件树就是一个按照层次结构分布的文件集合,例如,一个文件树可以代表一个目录树结构或者一个 ZIP 压缩文件的内容.它被抽象为 **FileTree **结构,**FileTree **继承自 **FileCollection**,所以你可以像处理文件集合一样处理文件树, Gradle 有些对象实现了FileTree 接口

例如 [源集合](https://docs.gradle.org/current/userguide/java_plugin.html#sec:source_sets). 使用 Project.fileTree() 方法可以得到 FileTree 的实例,它会创建一个基于基准目录的对象,然后视需要使用一些 Ant-style 的包含和去除规则.