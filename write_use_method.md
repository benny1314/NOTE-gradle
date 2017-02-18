## 使用方法

### 提取一个方法

> build.gradle

```
task checkSum << {
    
}

task loadfile << {

}

File[] fileList(String dir) {
    file(dir).listFiles({file -> file.isFile()} as FileFileter).sort()
}

```

