## 网页应用快速入门

Gradle 提供了两个插件用来支持网页应用: 

+ War 插件
 + War 插件是在 Java 插件的基础上扩充的用来构建 WAR 文件.
+ Jetty 插件 
 + Jetty 插件是在 War 插件的基础上扩充的, 允许用户将网页应用发布到一个介入的 Jetty 容器里.

## 构建一个 WAR 文件

为了构建一个 WAR 文件, 需要在项目中加入 War 插件:

### War 插件

> build.gradle

 apply plugin: 'war'

这个插件也会在你的项目里加入 Java 插件. 运行 gradle build 将会编译, 测试和创建项目的 WAR 文件. Gradle 将会把源文件包含在 WAR 文件的 `src/main/webapp` 目录里. 编译后的 classe , 和它们运行所需要的依赖也会被包含在 WAR 文件里.

## 运行你的web项目

要启动Web工程,在项目中加入Jetty plugin即可

### 采用Jetty plugin启动web工程

> build.gradle

```
apply plugin: 'war'
apply plugin: 'jetty'

repositories {
    mavenCentral()
}

dependencies {
    compile group: 'commons-io', name: 'commons-io', version: '1.4'
    compile group: 'log4j', name: 'log4j', version: '1.2.15', ext: 'jar'
}

jettyRun {
  reload ="automatic" // jetty 热部署
  scanIntervalSeconds = 1 // 扫描文件
}


httpPort = 8080
stopPort = 9451
stopKey = 'foo'

```

由于Jetty plugin继承自War plugin.使用 gradle jettyRun 命令将会把你的工程启动部署到jetty容器中. 调用 gradle jettyRunWar 命令会打包并启动部署到jetty容器中.

> Groovy web applications 你可以结合多个插件在一个项目中,所以你可以一起使用War 和 Groovy插件构建一个 Groovy 基础 web 应用.合适的 Groovy 类库会添加到你的 WAR 文件中.

|属性名称	类型|	默认值|	描述  |
|----------|---------|------|
|contextPath|	String|	WAR 文件的base name	在 Jetty 容器里面的应用程序部署位置。
|httpPort|	Integer|	8080	Jetty 监听 HTTP 请求的 TCP 端口。
|stopPort|	Integer|	null	Jetty 监听 admin 请求的 TCP 端口。
|stopKey|	String|	null	当需要请求停止时，传递给 Jetty 的key。
