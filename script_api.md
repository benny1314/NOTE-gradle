## 脚本 API

当 Gradle 执行一个脚本时，它会将这个脚本编译为实现了 **Script** 的类，也就是所有的**属性**和**方法**都是再 Script接口中生命的，由于你的脚本实现了 Script 接口，所以你可以再自己的脚本中使用他们

## 声明变量

在 Gradle 构建脚本中有两种类型的变量可以声明：**局部变量** ( local ) 和 **扩展属性** ( extra ) 

## 局部变量

局部变量使用关键字 **def** 来声明，其只在声明它的地方可见。局部变量是 Groovy 语言的有个基本特性

### 使用局部变量

```
def dest = "dest"

task copy(type: Copy){
    from "source"
    into dest
}

```