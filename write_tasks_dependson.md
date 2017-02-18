## 任务依赖

### 声明任务之间的依赖关系

> build.gradle

```
task cook << {
    println "开始做饭🍚"
}

task eat(dependsOn: cook) << {
    print "正在吃做好的饭🍚"
}

```


