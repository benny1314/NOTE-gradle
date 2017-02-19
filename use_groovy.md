## 一个基本的 Groovy 项目

###  Groovy 插件

> build.gradle

    apply plugin: 'groovy'

**它也会同时把 Java 插件加入到你的项目里**. Groovy 插件扩展了编译任务, 这个任务会在 `src/main/groovy` 目录里寻找源代码文件, 并且加入了编译测试任务来寻找 `src/test/groovy` 目录里的测试源代码. 编译任务使用 联合编译 (joint compilation) 来编译这些目录, 这里的联合指的是它们混合有 **java** 和 **groovy** 的源文件.

#### 使用 groovy 编译任务, 你必须声明 Groovy 的版本和 Groovy 库的位置.
 
你可以在配置文件里加入依赖, 编译配置会继承这个依赖, 然后 groovy 库将
被包含在 classpath 里.

### Groovy 

>build.gradle

```
apply plugin: 'eclipse'
apply plugin: 'groovy'

repositories {
    mavenCentral()
}

dependencies {
    compile 'org.codehaus.groovy:groovy-all:2.3.3'
    testCompile 'junit:junit:4.11'
}

```

