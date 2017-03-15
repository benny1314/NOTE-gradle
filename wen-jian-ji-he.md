文件集合表示一组文件，Gradle 使用 **FileCollection **接口表示文件集合, Gradle API 中的许多项目都实现了这个接口,例如 dependency configurations .

获取 FileCollection 实例的一种方法是使用 `Project.files()` 方法.

你可以传递任何数量的对象参数,这个方法能将你传递的对象集合转换为一组文件对象`.files()` 方法接收任何类型对象参数`.每一个 file()` 方法都依赖于项目目录(在第 15 章,第一小节中介绍)`.files()`方法也接收 **collections**, **iterables**, **maps **和 **arrays** 类型参数.这些参数的内容会被解析，然后被转换为文件对象.

### 创建文件集合

> build.gradle

```
FileCollection collection = files('src/file1.txt',
                                  new File('src/file2.txt'),
                                  ['src/file3.txt', 'src/file4.txt'])

```

文件集合可以被迭代器,使用迭代操作能够将其转换为其他的一些类型.你可以使用 `+` 操作将两个文件集合合并,使用 `-` 操作能够对一个文件集合做减法.

下面一些例子介绍如何操作文件集合.

### 使用文件集合

> build.gradle

```
// 对文件集合进行迭代
collection.each {File file ->
    println file.name
}

// 转换文件集合为其他类型
Set set = collection.files
Set set2 = collection as Set
List list = collection as List
String path = collection.asPath
File file = collection.singleFile
File file2 = collection as File

// 增加和减少文件集合
def union = collection + files('src/file3.txt')
def different = collection - files('src/file3.txt')

```

你也可以向 `files()` 方法专递一个闭合或者可回调的实例参数.当查询集合的内容时就会调用它,然后将返回值转换为一些文件实例.返回值可以是 `files()` 方法支持的任何类型的对象.下面有个简单的例子来演示实现 **FileCollection **接口

### 实现一个文件集合

> build.gradle

```
task list << {
    File srcDir

    // 使用闭合创建一个文件集合
    collection = files { srcDir.listFiles() }

    srcDir = file('src')
    println "Contents of $srcDir.name"
    collection.collect { relativePath(it) }.sort().each { println it }

    srcDir = file('src2')
    println "Contents of $srcDir.name"
    collection.collect { relativePath(it) }.sort().each { println it }
}

```







