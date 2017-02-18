## 构建脚本代码

Gradle 的构建脚本展示了 Groovy 的所有能力.

### 在 Gradle 任务里使用 Groovy

> build.gradle

```
task upper << {
    String someString = 'mY_nAmE'
    println "Original: " + someString
    println "Upper case: " + someString.toUpperCase()
}

```

`gradle -q upper` 命令的输出

```
> gradle -q upper
Original: mY_nAmE
Upper case: MY_NAME

```
