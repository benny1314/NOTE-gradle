## 指定一组输入文件

在 Gradle 中有一些对象的某些属性可以接收一组输入文件.例如,**JavaComplile **任务有一个 **source **属性,它定义了编译的源文件,你可以设置这个属性的值,只要 files() 方法支持. 

这意味着你可以使用 **File **, **String **, **collection **, **FileCollection **甚至是使用一个闭合去设置属性的值.

### 指定文件

> build.gradle

```
//使用一个 File 对象设置源目录
compile {
    source = file('src/main/java')
}

//使用一个字符路径设置源目录
compile {
    source = 'src/main/java'
}

// 使用一个集合设置多个源目录
compile {
    source = ['src/main/java', '../shared/java']
}

// 使用 FileCollection 或者 FileTree 设置源目录
compile {
    source = fileTree(dir: 'src/main/java').matching { include 'org/gradle/api/**' }
}

// 使用一个闭合设置源目录
compile {
    source = {
        // Use the contents of each zip file in the src dir
        file('src').listFiles().findAll {it.name.endsWith('.zip')}.collect { zipTree(it) }
    }
}

```